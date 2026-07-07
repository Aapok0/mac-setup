# Mac Setup

Script to set up my preferred environment on macOS.

## What it does

The setup script:

1. Generates an ed25519 SSH key at `~/.ssh/id_ed25519` (if not already present)
2. Prompts for machine type (personal or work) to determine which apps to install
3. Installs [Homebrew](https://brew.sh/) if not already present, or updates it
4. Installs `stow` and `just` (prerequisites for dotfiles)
5. Creates `~/Workspace` and clones [dotfiles](https://github.com/Aapok0/dotfiles) (converted to SSH remote)
6. Runs dotfiles `justfile` (`just install`) which handles core CLI tools, shell setup (ZSH, plugins, starship), font installation, stowing configs, and more
7. Prompts for git user configuration (`~/.config/git/config.local`)
8. Installs macOS apps — common set plus machine-type-specific apps:

| App | Personal | Work |
|-----|:--------:|:----:|
| Raycast | ✓ | ✓ |
| Rectangle | ✓ | ✓ |
| Hiddenbar, Stats, Itsycal | ✓ | ✓ |
| Bitwarden | ✓ | |
| KeePassXC | | ✓ |
| Firefox (optional) | ✓ | ✓ |
| Docker Desktop | ✓ | ✓ |
| Wireshark | ✓ | ✓ |
| VLC, Spotify | ✓ | ✓ |
| NordVPN | ✓ | |
| Tailscale | ✓ | |
| Cursor | ✓ | |
| Visual Studio Code | | ✓ |

The setup script records errors in a counter (`SETUP_ERRORS`) and exits non-zero if any step failed. It is safe to re-run: Homebrew skips already-installed packages, and helpers guard against recreating keys or git configs that already exist.

Output is logged to `logs/<timestamp>_setup.log` (absolute path under repo root).

## Repository structure

```
├── setup                       # Entry point — installs everything
├── instructions/
│   ├── system-settings.md      # macOS system preferences
│   ├── finder.md               # Finder configuration
│   ├── app-configuration.md    # Per-app settings and add-ons
│   └── manual-setup.md         # Manual steps if the script fails
└── logs/                       # Created at runtime (gitignored)
```

## Prerequisites

- A working internet connection
- `git` available to clone this repo and dotfiles
- macOS (Apple Silicon assumed for Homebrew paths)

## Usage

1. Clone this repo:

```bash
git clone <repo-url> ~/Workspace/mac-setup
cd ~/Workspace/mac-setup
```

2. Make the script executable:

```bash
chmod u+x setup
```

3. Run:

```bash
./setup
```

The script will prompt for machine type, Firefox version, and git user config during execution.

## Linting locally

The same checks run in CI (`.github/workflows/lint.yml`, pinned `shellcheck`/`shfmt`).

```bash
bash -n setup                         # quick parse check, no tools needed
shellcheck -x setup                   # static analysis (reads .shellcheckrc)
shfmt -d -i 4 -ci setup              # formatting check
```

## Post-setup

These steps are also printed by the script on completion:

1. Configure system settings (see [instructions/system-settings.md](instructions/system-settings.md)).
2. Configure Finder (see [instructions/finder.md](instructions/finder.md)).
3. Configure apps (see [instructions/app-configuration.md](instructions/app-configuration.md)).
4. Log out and back in (or run `exec zsh`) to use zsh.
5. Open Neovim and install Mason tools:
   ```
   nvim
   :MasonInstall shellcheck shfmt stylua prettier ruff hadolint tflint ansible-lint
   ```
6. Open tmux and install plugins: `tmux` then `ctrl+space I`.

## Future Considerations

- Velja (choose which browser opens what link)
- Ejectify (USB control)
- MPV (VLC alternative)
- Cron (calendar)
- Spark (mail)
- TempBox or mailsy (temporary email addresses)
- Shotrr (screenshots)
- ImageOptim (strip image metadata and reduce quality to save space)
- OnyX (system/disk level stuff)
- MenubarX (browser in the menubar)
- Taskell (kanban board in terminal with vim motions)
- Python environment setup (pyenv)
- Configurable app selection (skip categories interactively)
