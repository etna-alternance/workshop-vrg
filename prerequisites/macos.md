# Prerequisites — macOS

All tools are unsigned third-party binaries. macOS will block them on first launch — bypass Gatekeeper for each one:

**Option A (per app):** Right-click the app → **Open** → click **Open** in the dialog.

**Option B (system-wide, faster for a workshop):**
```bash
sudo spctl --master-disable
```
Re-enable after the workshop with `sudo spctl --master-enable`.

## TrenchBroom

Two builds are provided — use the one matching your Mac:
- `TrenchBroom-macOS-arm64-v2025.4-Release.zip` — Apple Silicon (M1/M2/M3/M4)
- `TrenchBroom-macOS-x86_64-v2025.4-Release.zip` — Intel

## ericw-tools

Extract `tools/map_editor/ericw-tools-v0.18.1-Darwin.zip`. If the binaries are blocked, run:
```bash
xattr -cr path/to/ericw-tools/
```

## Ironwail

Same Gatekeeper bypass applies. Right-click → Open on first launch.
