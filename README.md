# Lock Screen Button

A minimal GNOME Shell extension that adds a **padlock icon** to the top panel, next to the system menu. Click it to instantly lock your screen — the same lock action as the built-in system menu, just one click away.

![GNOME Shell](https://img.shields.io/badge/GNOME%20Shell-42%20|%2043%20|%2044-4A86CF)
![License](https://img.shields.io/badge/license-GPL--2.0--or--later-blue)

## Features

- Adds a padlock indicator in the top-right of the panel (the system / power area).
- A single click locks the session via the standard `SystemActions.activateLockScreen()` — identical behavior to the native lock button.
- No keyboard shortcuts hijacked, no D-Bus services, no settings to configure. It does one thing and cleans up fully when disabled.
- No `sudo` or system-wide changes required.

## Screenshot

<!-- Replace with your own screenshot -->
<!-- ![Padlock icon in the top panel](docs/screenshot.png) -->

## Compatibility

Tested on **GNOME Shell 42** (Ubuntu 22.04 LTS). Declared for GNOME **42, 43, and 44**, which all share the same extension APIs used here (`PanelMenu`, `SystemActions`, legacy GJS imports).

> GNOME 45 and later use ES modules and a different extension structure. This version is **not** compatible with GNOME 45+ without a rewrite.

## Installation

### From extensions.gnome.org (recommended)

Once the extension is published, install it in one click from its page on
[extensions.gnome.org](https://extensions.gnome.org/), using the browser
integration or the **Extensions** app.

### Manual installation

```bash
# Use your own UUID here (must match metadata.json and the folder name)
UUID="lockscreen-button@yourname.example.com"

mkdir -p ~/.local/share/gnome-shell/extensions/$UUID
cp metadata.json extension.js ~/.local/share/gnome-shell/extensions/$UUID/
```

Then reload GNOME Shell:

- **X11:** press `Alt+F2`, type `r`, press `Enter`.
- **Wayland** (Ubuntu's default): log out and log back in.

Enable it:

```bash
gnome-extensions enable "$UUID"
```

The padlock should appear in the top-right of the panel.

## Building the zip (for upload to extensions.gnome.org)

The archive must contain `metadata.json` at its **root** (not inside a subfolder):

```bash
zip -j lockscreen-button.zip metadata.json extension.js
```

Then upload `lockscreen-button.zip` at <https://extensions.gnome.org/upload/>.
Each submission goes through manual review before it goes live.

## Configuration

There are no settings. To change the icon, edit `icon_name` in `extension.js`:

- `changes-prevent-symbolic` — closed padlock (default)
- `system-lock-screen-symbolic` — a screen with a lock
- `channel-secure-symbolic` — a shield/lock

## Troubleshooting

Watch only this extension's log output:

```bash
journalctl -f -o cat /usr/bin/gnome-shell | grep -i lockscreen-button
```

Unrelated warnings (keysym binding messages, D-Bus search-provider errors from
Gnote or Seahorse, etc.) come from GNOME itself and are not caused by this
extension.

## Uninstall

```bash
gnome-extensions disable "$UUID"
rm -rf ~/.local/share/gnome-shell/extensions/$UUID
```

## License

Released under the **GNU General Public License v2.0 or later** (GPL-2.0-or-later),
consistent with GNOME Shell. See [LICENSE](LICENSE) for details.
