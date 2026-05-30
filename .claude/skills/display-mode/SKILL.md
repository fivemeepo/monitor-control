---
name: display-mode
description: Switch the external monitor between preset brightness levels for daytime and night work. Use this skill whenever the user says "daytime mode", "day mode", "night mode", "evening mode", asks to brighten or dim the external monitor to a preset, or otherwise indicates they want to change ambient screen brightness for time of day. Only the external display is adjusted — the built-in MacBook display is intentionally left alone (it has its own ambient sensor).
---

# Display Mode

Sets an external monitor to a preset brightness via DDC/CI (using `m1ddc`). Two presets:

| Mode | Brightness |
|------|-----------|
| Daytime | 95 |
| Night | 50 |

The MacBook built-in display is **not** touched — it auto-adjusts via True Tone / ambient light sensing, and the Apple Silicon brightness API isn't reliably writable from the CLI anyway.

## First-time setup (per machine)

DDC targets a monitor by a **display UUID that is unique to each Mac + monitor pairing**, so the UUID baked into the commands below will not match your hardware. On a new machine, list the displays:

```bash
m1ddc display list
```

Pick the entry that is **not** the built-in panel (the built-in usually shows as `Color LCD` / `Built-in`), copy its UUID, and replace the UUID in the two commands below. Tweak the `95` / `50` brightness values to taste.

## How to apply

Run the matching command exactly. The display UUID is pinned so the command targets the right monitor even if display order changes.

**Daytime mode:**
```bash
m1ddc display "EEE5CFDD-8922-4855-99E9-FA9E0BC9CB84" set luminance 95
```

**Night mode:**
```bash
m1ddc display "EEE5CFDD-8922-4855-99E9-FA9E0BC9CB84" set luminance 50
```

> The UUID above is the original author's Dell S2722QC. Replace it with your own — see **First-time setup** above.

After running, briefly confirm to the user (e.g. "External display set to 95 — daytime mode."). No need to read back the value; the monitor sometimes returns a stale luminance immediately after a write, which causes confusing output.

## If `m1ddc` says "display not found"

The monitor was replaced, its EDID changed, or you're on a different machine. Re-run `m1ddc display list`, pick the external display, and update the UUID in this file.

## Dependencies

- `m1ddc` (install with `brew install m1ddc`) — sends DDC/CI commands over USB-C/HDMI on Apple Silicon. **Required.**
- An external display that supports **DDC/CI** (most desktop monitors do; some USB-C hubs/adapters don't pass it through).
