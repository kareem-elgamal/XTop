<div align="center">

<img src="https://xtop-app.pages.dev/logo.png" width="96" alt="XTop" />

# XTop

**One orb, your whole workspace.**

A floating launcher for developers — search your projects, open them in the
right IDE and the right shell, and keep notes, requests, git, meetings and
reminders one keystroke away.

[![Download](https://img.shields.io/github/v/release/kareem-elgamal/XTop?style=for-the-badge&color=0b6fc4&label=download)](https://github.com/kareem-elgamal/XTop/releases/latest)
[![Documentation](https://img.shields.io/badge/docs-xtop--app.pages.dev-6b3fb0?style=for-the-badge)](https://xtop-app.pages.dev)
[![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-555?style=for-the-badge)](https://xtop-app.pages.dev/guide/download)

[العربية](README.ar.md) · [Documentation](https://xtop-app.pages.dev) · [Download](https://github.com/kareem-elgamal/XTop/releases/latest)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/panel-en-dark.png">
  <img src="https://xtop-app.pages.dev/shots/panel-en-light.png" width="620" alt="The XTop panel: collections, projects and the service icons.">
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
always-on-top orb.

## After it starts

XTop does not open a window of its own — it goes to the **tray**, and puts a
small floating orb on your desktop. Press <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Space</kbd>,
click the orb, or click the tray icon to open the panel — with the search box
already focused.

Carry on with **[Getting started →](https://xtop-app.pages.dev/guide/getting-started)**

## What is inside

| | |
| --- | --- |
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

Made by [Karim Khaled](https://github.com/kareem-elgamal)

</div>
