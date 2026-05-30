---
name: display-mode
description: Switch the Dell external monitor between preset brightness levels for daytime and night work. Use this skill whenever the user says "daytime mode", "day mode", "night mode", "evening mode", asks to brighten or dim the Dell monitor to a preset, or otherwise indicates they want to change ambient screen brightness for time of day. Only the Dell S2722QC is adjusted — the built-in MacBook display is intentionally left alone (it has its own ambient sensor).
---

# Display Mode

Sets the Dell S2722QC external monitor to a preset brightness via DDC/CI. Two presets:

| Mode | Dell brightness |
|------|-----------------|
| Daytime | 95 |
| Night | 50 |

The MacBook built-in display is **not** touched — it auto-adjusts via True Tone / ambient light sensing, and the Apple Silicon brightness API isn't reliably writable from the CLI anyway.

## How to apply

Run the matching command exactly. The Dell's display UUID is hardcoded so the command targets the right monitor even if display order changes.

**Daytime mode:**
```bash
m1ddc display "EEE5CFDD-8922-4855-99E9-FA9E0BC9CB84" set luminance 95
```

**Night mode:**
```bash
m1ddc display "EEE5CFDD-8922-4855-99E9-FA9E0BC9CB84" set luminance 50
```

After running, briefly confirm to the user (e.g. "Dell set to 95 — daytime mode."). No need to read back the value; the monitor sometimes returns a stale luminance immediately after a write, which causes confusing output.

## Recovering if the Dell UUID changes

If `m1ddc` returns "display not found" (e.g. the monitor was replaced or its EDID changed), list displays and update the UUID in this file:

```bash
m1ddc display list
```

Pick the entry labeled `DELL S2722QC` (or whichever Dell is connected) and replace the UUID above.

## Dependencies

- `m1ddc` (install with `brew install m1ddc`) — sends DDC/CI commands over USB-C/HDMI on Apple Silicon.
