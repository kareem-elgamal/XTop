# Plan — "Ask AI" service

Status: proposal · Target: the private XTop application repository (this repo is
the download and documentation home; the code changes below land in the app repo,
the documentation changes land here and on the docs site).

## 1. What it is

A new service in the panel, alongside Notes, Git, API and Meetings: a chat box
that already knows which project you are on.

The selling point is not "a chat window in a launcher" — anyone can alt-tab to a
browser for that. It is that XTop already holds the context a developer would
otherwise paste by hand: the active project's path and `.env`, its git branch and
working-tree status, its notes, its saved API requests, the last meeting
transcript. "Ask AI" is the service that hands those to the model, on the user's
say-so, and can act back on them through the same services.

Shortcut: <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>K</kbd> opens the panel straight
into a new conversation scoped to the selected project. From the search box,
typing a question and pressing <kbd>Ctrl</kbd>+<kbd>Enter</kbd> sends it as the
first message rather than searching projects.

## 2. Where it sits in the process model

The Anthropic API key never reaches the renderer, and no renderer code talks to
the network directly.

```
renderer (panel)                    main process
─────────────────                   ────────────
AskAI view                          ai/provider.ts      ← the only network caller
  ├─ ipcRenderer.invoke('ai:send')  ai/context.ts       ← builds the context blocks
  ├─ on('ai:delta')      ◄────────  ai/tools.ts         ← tools that call back into services
  ├─ on('ai:tool-request')          ai/store.ts         ← conversations as .md on disk
  └─ on('ai:done'/'ai:error')       ai/keys.ts          ← safeStorage (DPAPI on Windows)
```

- **Key storage** — `safeStorage.encryptString()` at rest, written next to the
  other app data, never into the settings JSON that backup/restore zips in
  plaintext. Decrypt in main, hold in memory for the session. If
  `safeStorage.isEncryptionAvailable()` is false, refuse to store the key and say
  so rather than falling back to plaintext.
- **Streaming over IPC** — one `ai:delta` message per text delta on a
  per-conversation channel id. Cancel is a renderer→main `ai:abort` that aborts
  the request's `AbortController`; a half-streamed answer is kept, marked
  interrupted.
- **Backpressure** — coalesce deltas on a ~30 ms timer before sending. Per-token
  IPC to a transparent always-on-top window is a visible frame-rate cost.

## 3. Provider layer

Two providers behind one interface, because XTop is a local-first app (Whisper
already transcribes on the machine) and some users will not send project context
to a hosted service at all:

| Provider | Package | Use |
| --- | --- | --- |
| **Claude API** (default) | `@anthropic-ai/sdk` | The good answers. Needs a key. |
| **Local (Ollama)** | HTTP to `localhost:11434` | Offline, no key, nothing leaves the machine. Degraded: no tool use in phase 1. |

Interface:

```ts
interface AiProvider {
  send(req: AiRequest, signal: AbortSignal): AsyncIterable<AiEvent>;
  supportsTools: boolean;
}
```

Anything provider-specific (model ids, tool schemas, effort) stays inside the
implementation; the renderer only sees `AiEvent`.

### Models and what they cost

| Model | Model ID | Input $/1M | Output $/1M |
| --- | --- | --- | --- |
| Claude Opus 5 | `claude-opus-5` | $5.00 | $25.00 |
| Claude Sonnet 5 | `claude-sonnet-5` | $2.00 | $10.00 |
| Claude Haiku 4.5 | `claude-haiku-4-5` | $1.00 | $5.00 |

Default to `claude-opus-5`. Expose the choice in settings — it is the user's key
and the user's money — but do not silently downgrade to save cost.

### The request

```ts
import Anthropic from "@anthropic-ai/sdk";

const client = new Anthropic({ apiKey });     // decrypted in main, never in the renderer

const stream = client.messages.stream({
  model: settings.ai.model,                   // "claude-opus-5"
  max_tokens: 64000,                          // streaming: give it room
  thinking: { type: "adaptive", display: "summarized" },
  output_config: { effort: "high" },          // "low" for the quick-answer path
  betas: ["server-side-fallback-2026-07-01"],
  fallbacks: "default",                       // route around a refusal instead of erroring
  system: [
    { type: "text", text: SYSTEM_PROMPT, cache_control: { type: "ephemeral" } },
    { type: "text", text: projectContext,  cache_control: { type: "ephemeral" } },
  ],
  messages: history,
}, { signal });

for await (const event of stream) {
  if (event.type === "content_block_delta" && event.delta.type === "text_delta") {
    push(event.delta.text);
  }
}
const final = await stream.finalMessage();    // final.usage → the cost meter
```

Notes that are easy to get wrong:

- `thinking.display` defaults to omitted on current models, so a streaming UI
  shows a long pause before the first token unless `"summarized"` is set.
- Don't lowball `max_tokens`; a truncated answer costs a full retry.
- `effort` is inside `output_config`, not top level.
- The refusal path returns HTTP 200 with `stop_reason: "refusal"` — check
  `stop_reason` before reading `content`.

## 4. Context — the part that makes it XTop's

Context is assembled in main from the services that already own the data. Each
source is a toggle in the composer, off by default except the first two, and the
composer shows exactly what will be sent with an approximate token count.

| Source | Comes from | Shape |
| --- | --- | --- |
| Project identity | panel selection | name, path, collection, aliases, IDE, WSL or Windows |
| Git state | Git service | branch, ahead/behind, `status --porcelain`, last 10 subjects |
| Notes | Notes service | the project's `.md` notes |
| API requests | API service | saved requests + resolved base URL from `.env` (**values redacted**) |
| Meeting | Meetings service | the most recent transcript summary |
| Terminal | Commands service | last N lines of the focused pty's scrollback |
| Selection | clipboard | `Ctrl+Shift+K` from a copied stack trace |

Rules:

- **Never send secrets.** `.env` contributes keys, not values. Redact anything
  matching the usual token shapes from terminal scrollback and git diffs before
  it leaves main. This is a filter in `ai/context.ts` with its own tests, not a
  best effort at the call site.
- **Order for cache hits.** Render order is `tools` → `system` → `messages`.
  Stable-first: system prompt, then project context, then the volatile question.
  A timestamp or a per-request id in the prefix silently voids the cache; verify
  with `usage.cache_read_input_tokens` on the second turn of a conversation.
- **Bound it.** Cap each source (notes to the most recent N KB, scrollback to N
  lines). Never truncate mid-way silently — tell the user in the composer that a
  source was trimmed.

## 5. Tool use — letting it act

Phase 2. The model gets a small set of tools that call back into services that
already exist, through the SDK's tool runner:

```ts
import { betaZodTool } from "@anthropic-ai/sdk/helpers/beta/zod";

const readNote = betaZodTool({
  name: "read_project_note",
  description: "Read a markdown note belonging to the active project.",
  inputSchema: z.object({ title: z.string() }),
  run: async ({ title }) => notes.read(activeProject, title),
});

const runner = client.beta.messages.toolRunner({
  model: settings.ai.model,
  max_tokens: 64000,
  tools: [readNote, gitStatus, listRequests, searchProjects, createReminder, sendRequest],
  messages: history,
  stream: true,
});

for await (const messageStream of runner) {
  for await (const event of messageStream) { /* same delta handling as above */ }
}
```

Split by blast radius:

- **Read tools** run unattended: `search_projects`, `git_status`, `git_log`,
  `read_project_note`, `list_api_requests`.
- **Write and side-effecting tools** stop for a confirmation card in the panel —
  `write_project_note`, `create_reminder`, `send_api_request` (it hits the user's
  own dev server), `run_command` (a saved quick command, never free-form shell).
  The tool runner's per-turn hook is where the gate goes.
- No arbitrary shell, no arbitrary filesystem write. XTop drives the user's real
  terminal and WSL; a model-authored command string is not something to run on a
  prompt-injected transcript. A meeting transcript or a fetched API response is
  untrusted input.

Return failures as `tool_result` with `is_error: true` rather than dropping them,
and parse tool inputs with `JSON.parse` — never string-match the serialized input.

## 6. Storage

Conversations are `.md` files on disk, following the Notes service's convention
so they can be committed, synced and grepped, and so backup/restore picks them up
with no new code:

```
<data>/ai/
  global/2026-09-05-1432-why-is-this-cors-failing.md
  projects/<project-id>/2026-09-05-1501-refactor-the-auth-guard.md
```

Front-matter carries `model`, `created`, `project`, `tokens_in`, `tokens_out`,
`cost_usd`, and which context sources were attached. The body is the transcript.
Tool calls render as fenced blocks. A conversation is resumable: reopening one
replays the messages array.

For long conversations, enable server-side compaction (beta `compact-2026-01-12`)
rather than dropping old turns — and append `response.content` back to `messages`
whole, not just the text, or the compaction state is lost silently.

## 7. Privacy, told plainly

- First run of the service shows one screen: what gets sent, to whom, that the
  key is stored encrypted on this machine, and the local-provider alternative.
  No dark pattern, no pre-ticked context toggles beyond project identity.
- A per-project **"never send this project"** flag, honoured in `ai/context.ts`.
- The composer's context preview is expandable to the literal text that will be
  sent. If a user cannot see what leaves their machine, the feature has not
  earned the context it is asking for.
- Nothing is sent on app start, on project selection, or on hover — only on an
  explicit send.

## 8. Cost control

- A running per-conversation and per-month token/cost meter, from
  `final.usage`, shown in settings.
- Prompt caching on the system prompt and the project context (breakpoints as in
  §3) — repeat turns in a conversation are the common case, and this is where the
  bill actually falls.
- Optional monthly soft cap that warns rather than blocks.
- `effort: "low"` for the one-shot "explain this error" path, `"high"` for chat.

## 9. Arabic and RTL

Everything the other services get: both locales, RTL layout when Arabic is on,
and a system-prompt line that tells the model to answer in the UI language unless
the user writes in the other one. Streamed text needs the same bidi handling as
notes — mixed Arabic prose and English identifiers in one paragraph.

## 10. Failure modes

| Case | Behaviour |
| --- | --- |
| No key configured | The service renders a setup card, not an error toast. |
| Offline / DNS failure | Offer the local provider if configured; keep the typed message. |
| 429 | Respect `retry-after`; show a countdown, don't spin silently. |
| Refusal (`stop_reason: "refusal"`) | Server-side fallback handles most; otherwise say what happened. |
| Stream interrupted | Keep the partial answer, mark it, offer retry. |
| `safeStorage` unavailable | Refuse to store the key; explain. Never write it in plaintext. |

## 11. Phases

1. **M1 — Ask.** Panel view, Claude provider, streaming over IPC, key storage,
   project + git context, conversations on disk, EN/AR. No tools.
2. **M2 — Act.** Tool runner, read tools unattended, write tools behind the
   confirmation card, usage meter.
3. **M3 — Reach.** Notes / API / meeting / terminal context sources, prompt
   caching, compaction for long chats.
4. **M4 — Local.** Ollama provider for offline and no-key use.

## 12. Settings added

`ai.enabled`, `ai.provider`, `ai.model`, `ai.effort`, `ai.contextDefaults`,
`ai.monthlyCapUsd`, `ai.localEndpoint`, and per-project `ai.excluded`.

## 13. Documentation work in this repository

Once M1 ships: a row in the "What is inside" table of `README.md` and
`README.ar.md` pointing at `/services/ask-ai`, the shortcut in the shortcuts
page, the new settings keys in the settings reference, and a line in the data
reference for `<data>/ai/`.

## 14. Open questions

- Should the orb itself accept a question without opening the panel?
- Bring-your-own-key only, or is a hosted XTop-brokered option ever on the table?
  (It changes the privacy story entirely and is worth deciding before M1 ships.)
- Do meeting transcripts get their own summarisation path through this service,
  replacing whatever summarises them today?
