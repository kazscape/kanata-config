# kanata-config

A macOS-focused Kanata keymap featuring:

- GACS home-row mods
- Hyper layer toggle via left Ctrl double-tap (left Ctrl stays normal Ctrl)
- Function layer on thumb key
- Tuned home-row timing for faster hold activation

## Files

- `kanata.kbd`: main portable template (device-agnostic)
- `kanata.kbd.example`: sample `defcfg` with `macos-dev-names-include`

## Quick Start (macOS)

1. Install Kanata (Homebrew):

   ```bash
   brew install kanata
   ```

2. Grant permissions in macOS:
   - Privacy & Security → Input Monitoring
   - Privacy & Security → Accessibility
   - Add `/opt/homebrew/bin/kanata`

3. Copy config:

   ```bash
   mkdir -p ~/.config/kanata
   cp kanata.kbd ~/.config/kanata/kanata.kbd
   ```

4. (Optional) Restrict to specific keyboards:
   - Run `kanata --list-devices`
   - Edit `defcfg` in `kanata.kbd`
   - Set `macos-dev-names-include (...)`

5. Run Kanata:

   ```bash
   sudo kanata --cfg ~/.config/kanata/kanata.kbd
   ```

## Tuning

Main timing vars in `kanata.kbd`:

- `tap-time`: tap threshold
- `hold-time`: global hold threshold (layer-taps)
- `hrm-hold-time`: home-row mod hold threshold

Recommended starting points:

- Faster hold: lower `hrm-hold-time` (e.g. 190-220)
- Fewer accidental holds: raise `hrm-hold-time`

## Notes

- This repo intentionally keeps the config standalone (no Ansible dependency).
- Device IDs are environment-specific; avoid committing your personal IDs.
