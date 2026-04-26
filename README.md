# Oracle Quick Open (OQO)

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-support-yellow?style=flat-square&logo=buy-me-a-coffee)](https://buymeacoffee.com/bowang168)
[![Sponsor](https://img.shields.io/badge/GitHub%20Sponsors-sponsor-ea4aaa?style=flat-square&logo=github-sponsors)](https://github.com/sponsors/bowang168)

Quickly open Oracle SR / KM docs / Bug / JIRA / Schedule / Directory links from selected text. Falls back to Google search when no known pattern is matched.

Supports **macOS** and **Linux** (Oracle Linux 9 / GNOME).

## Supported Patterns

| Type | Pattern | Example | Opens |
|------|---------|---------|-------|
| SR | `3-xxxxxxxxx` | `3-1234567890` | My Oracle Support |
| Cloud SR | `4-xxxxxxxxx` | `4-1234567890` | Cloud Support UI |
| Doc/KB | `xxxxx.x` | `99999.9` | MOS Knowledge Base |
| Bug | `xxxxxxx` | `1234567` | Bug DB |
| JIRA | `PROJ-xxxx` | `PROJ-12345` | JIRA |
| Directory | `@username` | `@john` | Directory |
| Email | `user@example.com` | — | Schedule |
| URL | `https://...` | — | Direct open (allowed domains only) |

When no pattern matches, the selected text is sent to **Google** scoped to Oracle documentation sites.

## Usage

```bash
# Default: detect selected text, open matching links in Chrome
oqo.py

# Extract URLs to clipboard without opening browser
oqo.py --no-open

# Show raw captured values (SR numbers, doc IDs, etc.)
oqo.py --raw-capture

# Copy only the first matched value to clipboard
oqo.py --one-value

# Debug mode
oqo.py --debug
```

## Installation

```bash
git clone https://github.com/bowang168/oracle-quick-open.git ~/g/oracle-quick-open
cd ~/g/oracle-quick-open

# Decrypt oqo.py (requires git-crypt key)
git-crypt unlock ~/.ssh/github-crypt-key

# Symlink to PATH
mkdir -p ~/.local/bin
ln -sf ~/g/oracle-quick-open/oqo.py ~/.local/bin/oqo.py
chmod +x ~/g/oracle-quick-open/oqo.py
```

### Without git-crypt key

If you don't have the key, copy the example and fill in your own URLs:

```bash
cp oqo_example.py oqo.py
# Edit oqo.py — replace example.com URLs with your real private URLs
chmod +x oqo.py
```

### File structure

| File | Description |
|------|-------------|
| `oqo.py` | Real config with private URLs (git-crypt encrypted) |
| `oqo_example.py` | Safe template with placeholder URLs |

### Keyboard Shortcuts

Bind `oqo.py` to a hotkey for one-keystroke access:

**Linux (GNOME):** Settings > Keyboard > Custom Shortcuts

| Shortcut | Command | Description |
|----------|---------|-------------|
| `Super+j` | `oqo.py` | Open matched links |
| `Super+u` | `oqo.py --no-open` | Extract URLs only |
| `Super+y` | `oqo.py --one-value` | Copy first value |
| `Super+o` | `oqo.py --raw-capture` | Raw capture mode |

**macOS:** System Settings > Keyboard > Shortcuts > App Shortcuts, or use Automator / Raycast.

## Requirements

- Python 3.6+
- Google Chrome
- **Linux:** `wl-clipboard` for Wayland clipboard access
  ```bash
  sudo dnf install wl-clipboard    # OL9 / Fedora
  ```
- **macOS:** Grant accessibility permissions to your terminal app in System Settings > Privacy & Security > Accessibility

### macOS Chrome Setup

Enable JavaScript from Apple Events: Chrome menu > View > Developer > Allow JavaScript from Apple Events

## Log

Logs are written to `~/.oqo/oqo.log`.

## License

[MIT](LICENSE)
