# kanata-config

A macOS-focused Kanata keymap featuring:

- GACS home-row mods
- Hyper layer via left Ctrl double-tap+hold (not sticky; left Ctrl stays normal Ctrl)
- Function layer on thumb key
- Tuned home-row timing for faster hold activation

## Files

- `kanata.kbd`: main portable template (device-agnostic)
- `kanata.kbd.example`: sample `defcfg` with `macos-dev-names-include`
- `kanata.local.kbd`: your personal config (gitignored)
- `bin/kanata-start`, `bin/kanata-stop`, `bin/kanata-status`: helper scripts

## Quick Start (macOS)

This repository is intended to be used by cloning and manually distributing the files.

1. Clone this repository:

   ```bash
   git clone <YOUR_REPO_URL> ~/src/kanata-config
   cd ~/src/kanata-config
   ```

2. Install Kanata (Homebrew):

   ```bash
   brew install kanata
   ```

3. Grant permissions in macOS:
   - Privacy & Security → Input Monitoring
   - Privacy & Security → Accessibility
   - Add `/opt/homebrew/bin/kanata`

4. Copy config:

   ```bash
   mkdir -p ~/.config/kanata
   cp ./kanata.kbd ~/.config/kanata/kanata.kbd
   ```

5. (Recommended) Keep personal device IDs out of Git:

   Create a local-only config file and edit it instead of modifying `kanata.kbd` directly:

   ```bash
   cp -n ./kanata.kbd ./kanata.local.kbd
   ${EDITOR:-vi} ./kanata.local.kbd
   ```

   - `kanata.local.kbd` is listed in `.gitignore`.
   - Enable `macos-dev-names-include` (get IDs with `kanata --list-devices`) if you want to restrict Kanata to specific keyboards.

   Then distribute it to the runtime path:

   ```bash
   cp -f ./kanata.local.kbd ~/.config/kanata/kanata.kbd
   ```

6. Run Kanata:

   ```bash
   sudo kanata --cfg ~/.config/kanata/kanata.kbd
   ```

## Helper scripts

This repo includes helper commands under `bin/`:

- `kanata-start`: start Kanata in background (sudo required)
- `kanata-stop`: stop Kanata
- `kanata-status`: show status and recent errors

Install them into your PATH (example):

```bash
mkdir -p ~/.local/bin
cp -f ./bin/kanata-start ./bin/kanata-stop ./bin/kanata-status ~/.local/bin/
chmod +x ~/.local/bin/kanata-start ~/.local/bin/kanata-stop ~/.local/bin/kanata-status
```

If you prefer to keep them linked to the cloned repo (so updates are automatic), use symlinks instead:

```bash
mkdir -p ~/.local/bin
ln -sf "${PWD}/bin/kanata-start" ~/.local/bin/kanata-start
ln -sf "${PWD}/bin/kanata-stop" ~/.local/bin/kanata-stop
ln -sf "${PWD}/bin/kanata-status" ~/.local/bin/kanata-status
chmod +x "${PWD}/bin/kanata-start" "${PWD}/bin/kanata-stop" "${PWD}/bin/kanata-status"
```

Environment overrides (optional):

- `KANATA_CONFIG_FILE` (default: `~/.config/kanata/kanata.kbd`)
- `KANATA_PID_FILE` (default: `/tmp/kanata.pid`)
- `KANATA_BIN` (default: `/opt/homebrew/bin/kanata` or `kanata` in PATH)
- `KANATA_OUT_LOG` (default: `<config-dir>/kanata.out.log`)
- `KANATA_ERR_LOG` (default: `<config-dir>/kanata.err.log`)

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
