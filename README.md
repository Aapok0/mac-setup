# Mac Setup

Script to set up my preferred environment on macOS.

## What it does

The setup script:

1. Installs [Homebrew](https://brew.sh/) if not already present
2. Installs `stow` and `just` (prerequisites for dotfiles)
3. Creates `~/Workspace` and clones [dotfiles](https://github.com/Aapok0/dotfiles) (converted to SSH remote)
4. Runs dotfiles `justfile` (`just install`) which handles core CLI tools, shell setup (ZSH, plugins, starship), font installation, stowing configs, and more
5. Prompts for git user configuration (`~/.config/git/config.local`)
6. Installs macOS apps (Raycast, Rectangle, menu bar apps, browsers, Docker, etc.)

Output is logged to `logs/<timestamp>_setup.log`.

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

The script will prompt for choices (password manager, Firefox version) during execution.

## Post-setup

These steps are also printed by the script on completion:

1. Configure system settings (see [instructions/system-settings.md](instructions/system-settings.md)).
2. Configure Finder (see [instructions/finder.md](instructions/finder.md)).
3. Configure apps (see [instructions/app-configuration.md](instructions/app-configuration.md)).
4. Log out and back in (or run `exec zsh`) to use zsh.
5. Open Neovim and install Mason tools:
   ```bash
   nvim
   # Let lazy.nvim install plugins, then run:
   # :MasonInstall shellcheck shfmt stylua prettier ruff hadolint tflint ansible-lint
   ```
6. Open tmux and install plugins: `tmux` then `ctrl+space I`.

## Unfinished / TODO

- Configurable app selection (skip categories interactively)
- SSH key creation prompt
- Python environment setup (pyenv)

## Future Considerations

- Velja (choose which browser opens what link)
- Ejectify (usb control)
- MPV (VLC alternative)
- Cron (calendar)
- Spark (mail)
- TempBox or mailsy (temporary email addresses)
- Shotrr (screenshots)
- ImageOptim (strip image metadata and reduce quality to save space)
- OnyX (system/disk level stuff)
- MenubarX (browser in the menubar)
- Taskell (kanban board in terminal with vim motions)
