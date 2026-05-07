# Manual Setup

If the setup script doesn't work, follow these steps manually.

## 1. Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
eval "$(/opt/homebrew/bin/brew shellenv)"
```

## 2. Install Prerequisites

```bash
brew install stow just
```

## 3. Clone Dotfiles

```bash
mkdir -p $HOME/Workspace
git clone https://github.com/Aapok0/dotfiles.git $HOME/Workspace/dotfiles
```

Convert to SSH remote (optional, requires SSH key):

```bash
cd $HOME/Workspace/dotfiles
git remote set-url origin git@github.com:Aapok0/dotfiles.git
```

## 4. Run Dotfiles Setup

```bash
cd $HOME/Workspace/dotfiles
just install
```

This installs all core CLI tools (via Brewfile), stows configs, installs JetBrainsMono Nerd Font, clones ZSH plugins and TPM, sets up shell, and more.

If `just install` fails, run the recipes individually:

```bash
just brew-install       # install packages from Brewfile
just font-install       # install JetBrainsMono Nerd Font
just stow-all           # symlink all configs
just zsh-plugins        # clone ZSH plugins
just tpm-install        # clone tmux plugin manager
just set-shell          # change default shell to zsh
just yazi-theme         # install yazi Catppuccin theme
just atuin-import       # import shell history into atuin
just check              # verify core tools are installed
```

## 5. Git User Configuration

Create `~/.config/git/config.local`:

```bash
mkdir -p $HOME/.config/git
cat > $HOME/.config/git/config.local << EOF
[user]
    name = Your Name
    email = your@email.com
EOF
```

## 6. Install macOS Apps

### Raycast

```bash
brew install --cask raycast
```

### Rectangle

```bash
brew install --cask rectangle
```

### Menu Bar Apps

```bash
brew install --cask hiddenbar stats itsycal
```

### Password Manager

```bash
# Bitwarden
brew install --cask bitwarden

# KeePassXC
brew install --cask keepassxc
```

### Firefox

```bash
# Regular
brew install --cask firefox

# Developer Edition
brew install --cask firefox@developer-edition
```

### Docker Desktop

```bash
brew install --cask docker
```

### Kubelogin

```bash
brew install Azure/kubelogin/kubelogin
```

### Wireshark

```bash
brew install --cask wireshark
```

### Media Apps

```bash
brew install --cask vlc spotify
```

### Android File Transfer

```bash
brew install --cask android-file-transfer
```

## 7. Post-Setup

1. Configure system settings (see [system-settings.md](system-settings.md)).
2. Configure Finder (see [finder.md](finder.md)).
3. Configure apps (see [app-configuration.md](app-configuration.md)).
4. Log out and back in (or run `exec zsh`) to use zsh.
5. Open Neovim and install Mason tools:
   ```bash
   nvim
   # Let lazy.nvim install plugins, then run:
   # :MasonInstall shellcheck shfmt stylua prettier ruff hadolint tflint ansible-lint
   ```
6. Open tmux and install plugins: `tmux` then `ctrl+space I`.
