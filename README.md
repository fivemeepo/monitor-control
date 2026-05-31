# display-mode

A [Claude Code](https://claude.com/claude-code) **skill** that switches an external monitor between **daytime** and **night** brightness presets over DDC/CI. The MacBook built-in display is left untouched (it has its own ambient sensor).

This repository exists solely to package and share that one skill.

## What's here

The skill lives at `.claude/skills/display-mode/SKILL.md`

## Use it

- **In this repo:** open the folder in Claude Code and say *"daytime mode"* or *"night mode"* — project skills under `.claude/skills/` load automatically, no install step.
- **Anywhere:** copy the skill into your global skills directory:
  ```bash
  cp -R .claude/skills/display-mode ~/.claude/skills/
  ```

## Requirements

- macOS on Apple Silicon
- [`m1ddc`](https://github.com/waydabber/m1ddc) — `brew install m1ddc`
- An external display that supports DDC/CI

## Per-machine setup

Each monitor has a unique DDC UUID, so set yours once: run `m1ddc display list`, pick your external display, and put its UUID into the daytime/night commands in `.claude/skills/display-mode/SKILL.md`
