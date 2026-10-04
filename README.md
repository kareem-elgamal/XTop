<div align="center">

<img src="https://xtop-app.pages.dev/logo.png" width="96" alt="XTop" />

# XTop

**One island, your whole workspace.**

A floating launcher for developers — search your projects, open them in the
right IDE and the right shell, and keep notes, requests, git, meetings and
reminders one keystroke away. Ask X, the built-in assistant, about any window —
it uses the AI tool you already have, with no API key.

[![Download](https://img.shields.io/github/v/release/kareem-elgamal/XTop?style=for-the-badge&color=0b6fc4&label=download)](https://github.com/kareem-elgamal/XTop/releases/latest)
[![Documentation](https://img.shields.io/badge/docs-xtop--app.pages.dev-6b3fb0?style=for-the-badge)](https://xtop-app.pages.dev)
[![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-555?style=for-the-badge)](https://xtop-app.pages.dev/guide/download)

[العربية](README.ar.md) · [Documentation](https://xtop-app.pages.dev) · [Download](https://github.com/kareem-elgamal/XTop/releases/latest)



<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/island-chat-en-dark.png">
  <img src="https://xtop-app.pages.dev/shots/island-chat-en-light.png" width="560" alt="X, the built-in assistant, answering in the island with the files it changed.">
</picture>

</div>

## Download

**[⭳ Download XTop →](https://github.com/kareem-elgamal/XTop/releases/latest)**

| File | What it is |
| --- | --- |
| **`XTop Setup <version>.exe`** | The installer. Adds a Start-menu entry, a desktop shortcut, and an uninstaller. Take this one. |
| **`XTop-portable-<version>.exe`** | A single file that runs as-is. Good for a USB stick or a machine you cannot install on. |

Both are the same application. Neither needs Node.js or anything else installed
first.

> [!WARNING]
> The app is not code-signed, so Windows SmartScreen says the publisher is
> unknown. Choose **More info → Run anyway**.

XTop is a **Windows** application. It opens your IDE, drives Windows Terminal
and WSL, and needs a Windows desktop session for the tray icon and the
island.

## After it starts

XTop does not open a window of its own — it goes to the **tray**, and puts a
small capsule — the island — on the edge of your screen. Press <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Space</kbd>,
click the island, or click the tray icon to open the panel — with the search box
already focused.

Carry on with **[Getting started →](https://xtop-app.pages.dev/guide/getting-started)**

## A quick tour

<table>
<tr>
<td align="center" width="50%">
<a href="https://xtop-app.pages.dev/services/panel">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/panel-en-dark.png">
  <img src="https://xtop-app.pages.dev/shots/panel-en-light.png" width="380" alt="The panel — projects, collections, search">
</picture>
</a><br>
<sub><b>The panel — projects, collections, search</b></sub>
</td>
<td align="center" width="50%">
<a href="https://xtop-app.pages.dev/services/commands-terminal">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/terminal-en-dark.png">
  <img src="https://xtop-app.pages.dev/shots/terminal-en-light.png" width="380" alt="The terminal — tabs, shells, suggestions">
</picture>
</a><br>
<sub><b>The terminal — tabs, shells, suggestions</b></sub>
</td>
</tr>
<tr>
<td align="center" width="50%">
<a href="https://xtop-app.pages.dev/services/api">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/api-response-en-dark.png">
  <img src="https://xtop-app.pages.dev/shots/api-response-en-light.png" width="380" alt="The API tester — your project's own base URL">
</picture>
</a><br>
<sub><b>The API tester — your project's own base URL</b></sub>
</td>
<td align="center" width="50%">
<a href="https://xtop-app.pages.dev/services/meetings">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/meetings-transcript-en-dark.png">
  <img src="https://xtop-app.pages.dev/shots/meetings-transcript-en-light.png" width="380" alt="Meetings — transcript and summary">
</picture>
</a><br>
<sub><b>Meetings — transcript and summary</b></sub>
</td>
</tr>
<tr>
<td align="center" colspan="2">
<a href="https://xtop-app.pages.dev/services/notes">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/notes-en-dark.png">
  <img src="https://xtop-app.pages.dev/shots/notes-en-light.png" width="380" alt="Notes — Markdown files on disk">
</picture>
</a><br>
<sub><b>Notes — Markdown files on disk</b></sub>
</td>
</tr>
</table>

## What is inside

| | |
| --- | --- |
| **[The island](https://xtop-app.pages.dev/services/island)** | A capsule pinned to the edge of your screen. Point at it for the four services, click it for your projects, drop files on it, or drag X onto any window. |
| **[X Agent](https://xtop-app.pages.dev/services/x-agent)** | Ask about your project or any window. It runs the AI tool you already have — Claude, ChatGPT, Gemini or OpenCode — on your own subscription, with no API key. |
| **[Projects, found by any name](https://xtop-app.pages.dev/services/panel)** | Collections, aliases and fuzzy search. `Enter` opens the IDE, `Shift+Enter` opens a terminal — in Windows or in WSL, whichever the project uses. |
| **[Quick commands in a real terminal](https://xtop-app.pages.dev/services/commands-terminal)** | Per-project, per-collection and global commands, run in a tabbed pty session that keeps its scrollback. |
| **[An API tester that knows your project](https://xtop-app.pages.dev/services/api)** | The base URL comes from the project's own `.env`, saved requests live in the repo, and `Ctrl+Shift+A` opens a scratch tab from your clipboard. |
| **[Meetings, transcribed locally](https://xtop-app.pages.dev/services/meetings)** | Microphone plus system audio, transcribed on your own machine by Whisper, then summarised into decisions and action items. |
| **[Markdown notes on disk](https://xtop-app.pages.dev/services/notes)** | A global notebook plus per-project notes, stored as `.md` files you can commit, sync or grep. |
| **[Git info](https://xtop-app.pages.dev/services/git)** | Branch, ahead/behind, working-tree status, branch switching and the commit graph, per project. |
| **[Prayer times and أذكار](https://xtop-app.pages.dev/services/islamic)** | Alerts a few minutes after the adhan, a snooze button that runs away from your pointer, and the morning and evening أذكار with counters. |
| **[Reminders](https://xtop-app.pages.dev/services/reminders)** | One-off or repeating, with snooze — and they survive the app being closed. |
| **[Backup & restore](https://xtop-app.pages.dev/services/backup)** | One-click or scheduled `.zip` backups of everything, to any folder — including a cloud-synced one. |
| **[Startup projects](https://xtop-app.pages.dev/services/startup)** | Projects that open themselves, in the IDE or a terminal, when the app launches. |

Arabic and English throughout, English by default, RTL when Arabic is on.
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/island-demo-en-dark.gif?v=1">
  <img src="https://xtop-app.pages.dev/island-demo-en-light.gif?v=1" width="720" alt="The XTop island on a Windows desktop: drag X onto VS Code, a web page or Figma, and ask about it or link it to a project.">
</picture>
## Documentation

Everything lives on **[xtop-app.pages.dev](https://xtop-app.pages.dev)**, in
English and Arabic:

- [Getting started](https://xtop-app.pages.dev/guide/getting-started) — the first ten minutes
- [Keyboard shortcuts](https://xtop-app.pages.dev/guide/shortcuts) — every one of them
- [Settings](https://xtop-app.pages.dev/reference/settings) · [Where data lives](https://xtop-app.pages.dev/reference/data)
- [Troubleshooting](https://xtop-app.pages.dev/reference/troubleshooting)

## About this repository

This repository is the **download and documentation home** for XTop. The
application source is not published here.

Found a bug or want a feature? Open an
[issue](https://github.com/kareem-elgamal/XTop/issues).

---

<div align="center">

Made by [Karim Elgamal](https://github.com/kareem-elgamal)

</div>
