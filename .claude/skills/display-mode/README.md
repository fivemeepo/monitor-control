# display-mode skill

A [Claude Code](https://claude.com/claude-code) skill that sets an external monitor to **daytime** / **night** brightness presets via DDC/CI. The MacBook built-in display is left alone.

## Using it

This is a **project skill**, so it's picked up automatically:

- Open this repository in Claude Code and just say *"daytime mode"* or *"night mode"* — no install needed.

To use it from **any** directory, copy it into your global skills folder:

```bash
cp -R .claude/skills/display-mode ~/.claude/skills/
```

## Prerequisites

- macOS on Apple Silicon
- [`m1ddc`](https://github.com/waydabber/m1ddc) — `brew install m1ddc`
- An external display that supports **DDC/CI**

## First run (per machine)

The skill targets a monitor by a UUID unique to your machine, so set yours once:

```bash
m1ddc display list
```

Find your external display (not the built-in `Color LCD`), copy its UUID, and put it into `SKILL.md` in place of the example UUID. Details are in the **First-time setup** section of `SKILL.md`.
