# Mac setup

I've compiled here all the settings, configurations and apps I use with Mac. I can use these instructions to get the setup I want without forgetting anything.

## Contents

1. [System Settings](#system-settings)
2. [Finder](#finder)
3. [Homebrew - Package manager](#homebrew---package-manager)
4. [Raycast - Replacemement for Spotlight](#raycast---replacemement-for-spotlight)
5. [Window management](#window-management)
6. [Terminal and tools](#terminal-and-tools)
7. [Apps](#apps)

## System Settings

### Touch ID & Password

- Add at least the main fingerprint used twice.
- Add at least one additional finger.
- Name the fingerprints accordingly.
- Add touch id as a method to authorize sudo with the following commands:

```bash
# Copy the sudo_local file template to a sudo_local file.
sudo cp /etc/pam.d/sudo_local.template /etc/pam.d/sudo_local
```

```bash
# Open the file with vim (or your choice of editor) and uncomment the last line.
sudo vim /etc/pam.d/sudo_local
```

### General

- Search and install any software updates.
- Make sure Language & Region has all correct units.

### Appearance

- Switch to dark mode.
- Disable wallpaper tinting in windows.
  - To make sure accurate colors are used.
- Always show scrollbars.

### Displays

- Do not automatically adjust brightness.
  - To have brightness always be what you want.
- Disable true tone.
  - To make sure accurate colors are used.

### Battery

- From options, do not slightly dim the display on battery.
  - To have brightness always be what you want.

### Accessability

- From pointer control and trackpad options choose three-finger dragging style.

### Trackpad

- Make sure tap to click is enabled.

### Keyboard

- From text input click edit.
  - Disable spell check.
  - Disable capitalization.
  - Disable smart quotes and dashes.
    - So quotes are not changed to something that does not work in code or terminal.

### Lock Screen

- Change the display off settings to something reasonable.

### Control Centre

- Show bluetooth in menu bar.

### Desktop & Dock

- Remove all apps that you don't use from the dock.
- Make dock smaller and add magnification.
- Minimize windows using scale effect.
  - Faster and more minimal.
- Automatically hide and show the dock.
- Do not show suggested and recent apps in dock.
- Click wallpaper to reveal desktop only in stage manager.
- Disable widgets.
- Do not automatically rearrange spaces based on most recent use.
- Disable hot corners.
- Hide and reveal dock faster using the following commands (defaults are 0.5):

```bash
defaults write com.apple.dock autohide-delay -float 0.2;killall Dock
```

```bash
defaults write com.apple.dock autohide-time-modifier -int 0.2;killall Dock
```

- Add dock spacers with the following commands (first one is full app width and second is half):

```bash
defaults write com.apple.dock persistent-apps -array-add '{tile-data={}; tile-type="spacer-tile";}' && killall Dock
```

```bash
defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="small-spacer-tile";}' && killall Dock
```

- Make hidden apps transparent with the following command:

```bash
defaults write com.apple.Dock showhidden -bool TRUE && killall Dock
```

### Screenshots

- Change screenshot default file type to jpg with the following command (default is png -> much bigger files):

```bash
defaults write com.apple.screencapture type jpg
```

- Change screenshot default location `~/Pictures/Screenshots` with the following commands (default is Desktop):

```bash
mkdir ~/Pictures/Screenshots
```

```bash
defaults write com.apple.screencapture location "~/Pictures/Screenshots"
```

### iCloud

- Disable anything related to iCloud, if it's a requirement from e.g. work.

## Finder

### View

- View as list or sort by snap to grid.
- Show tab bar, path bar and status bar.

### Settings

#### General

- Show no items on desktop.
- Have new finder windows show home directory.
- Open folders in tabs instead of windows.

#### Tags

- Disable all tags.

#### General

- Remove everything you don't need from the sidebar.

#### Advanced

- Show all filename extensions.
- Search the current folder.

## Homebrew - Package manager

- Install homebrew with this script provided by them:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- Add a cask that adds alternative versions of apps to be searched (don't show up in Raycast):

```bash
brew tap homebrew/cask-versions
```

## Raycast - Replacemement for Spotlight

- Install Raycast with homebrew:

```bash
brew install --cask raycast
```

- Do not choose clipboard or window management features.
- Disable spotlight shortcut from system settings -> keyboard -> shortcuts.
- Set command + space as the shortcut for Raycast.
- Install homebrew, Google Translate, Search Word, Phind Search and YouTube extension:
  - command + , to open settings -> extensions -> +-sign -> install from store.

## Window management

### Yabai - Tiling window manager

- Had some issues using this with a dock so need to figure things out or reconsider using this.
- Install Yabai with homebrew:

```bash
brew install koekeishiya/formulae/yabai
```

- Clone Yabai configuration to `~/.config` from [here](https://github.com/Aapok0/yabai):

```bash
git clone https://github.com/Aapok0/yabai.git
```

- To set shortcuts for Yabai, install skhd with homebrew:

```bash
brew install koekeishiya/formulae/skhd
```

- Clone skhd configuration to `~/.config` from [here]():

```bash
TBD
```

- Start skhd service with the following command (and give permissions, if needed):

```bash
skhd --start-service
```

- Start skhd service with the following command (and give permissions, if needed):

```bash
yabai --start-service
```

### Rectangle - Window snapping tool

- Install Rectangle with homebrew:

```bash
brew install --cask rectangle
```

- Make sure it starts at login.

## Terminal and tools

### Kitty - Terminal emulator

- Install kitty with homebrew.

```bash
brew install kitty
```

- Clone kitty configuration to `~/.config` from [here](https://github.com/Aapok0/kitty):

```bash
git clone https://github.com/Aapok0/kitty.git ~/.config/kitty
```

- The configuration uses Fira Code Nerd Font. You can install it with homebrew:

```bash
brew tap homebrew/cask-fonts
```

```bash
brew install --cask font-fira-code-nerd-font
```

- Some extra steps are required to make kitty draggable. Add or modify the following in the configuration and then run the following command:

```
hide_window_decorations titlebar-only
```

```bash
defaults write -g NSWindowShouldDragOnGesture YES
```

### ZSH

- Clone ZSH configuration to `~/.config` from [here](https://github.com/Aapok0/zsh):

```bash
git clone https://github.com/Aapok0/zsh.git ~/.config/zsh
```

- Add the following line to `~/.config/zsh/.zshrc` to get homebrew and the installed apps to work (after DEFAULT EDITOR):

```bash
### HOMEBREW
eval "$(/opt/homebrew/bin/brew shellenv)"
```

- Install coreutils with homebrew to to get dircolors:

```bash
brew install coreutils
```

- Add the following line to `~/.config/zsh/.zshrc` to add coreutils to PATH (add before COMPLETIONS):

```bash
### COREUTILS FOR DIRCOLOR
PATH="/opt/homebrew/opt/coreutils/libexec/gnubin:$PATH"
```

- Install Spaceship prompt theme or PowerLevel10k theme:
  - PowerLevel10k currently in use.

```bash
git clone https://github.com/spaceship-prompt/spaceship-prompt.git ~/.config/zsh/themes/spaceship-prompt
```

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.config/zsh/themes/powerlevel10k
```

- Install Fast-Syntax-Highlighting plugin:

```bash
git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git ~/.config/zsh/plugins/fast-syntax-highlighting
```

- Install ZSH-Autosuggestions plugin:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions.git ~/.config/zsh/plugins/zsh-autosuggestions
```

- Install ZSH-Completions plugin:

```bash
git clone https://github.com/zsh-users/zsh-completions.git ~/.config/zsh/plugins/zsh-completions
```

- Install wget python3, neovim, tmux, eza, batcat, htop, ripgrep, xclip, zoxide, fzf, fd, tfswitch, telnet, azure cli, github cli, ffmpeg, tldr and thefuck with homebrew:

```bash
brew install wget python3 node neovim tmux eza bat htop ripgrep xclip zoxide fzf fd warrensbox/tap/tfswitch telnet azure-cli gh ffmpeg tlrc thefuck
```

- Install fzf-git from source:

```bash
git clone https://github.com/junegunn/fzf-git.sh.git ~/.config/zsh/tools/fzf-git.sh
```

- Change fzf tool init to `eval "$(fzf --zsh)"`
- Change `fdfind` to `fd` in the custom fzf commands.
- Install Catppuccin Mocha theme for batcat:

```bash
mkdir -p "$(bat --config-dir)/themes" && \
wget -P "$(bat --config-dir)/themes" https://github.com/catppuccin/bat/raw/main/themes/Catppuccin%20Mocha.tmTheme && \
bat cache --build
```
- Change tfswitch path to the current computer's home.
- Create a Python virtual environment and install ansible:

```bash
mdkir ~/Python
```

```bash
python3.12 -m venv ~/Python/python3.12
```

- Install ansible to the virtual environment:

```bash
pip install ansible
```

- Remove unnecessary tools from the end of `~/.config/zsh/.zshrc`.

- Create symlink of .zshenv to home directory have zsh use `~/.config/zsh` as the directory for zsh files (replace the beginning of the paths with the absolute path):

```bash
ln -s /absolute/path/to/home/.config/zsh/.zshenv /absolute/path/to/home/.zshenv
```

- Source .zshenv and .zshrc:

```bash
source ~/.zshenv && source ~/.config/zsh/.zshrc
```

### Neovim

- Clone configuration to `~/.config` from [here](https://github.com/Aapok0/nvim):

```bash
git clone https://github.com/Aapok0/nvim.git ~/.config/nvim
```
- Some of the plugins and features require npm, xclip and ripgrep, but those have been installed earlier.
- Neovim will install all the plugins and lsp servers, when you first open it.
  - Some issues may arise, from outdated configurations etc.

### tmux

- Clone configuration to `~/config` from [here](https://github.com/Aapok0/tmux):

```bash
git clone https://github.com/Aapok0/tmux.git ~/.config/tmux
```

- Install tmux package manager with the following command:

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

- Open tmux session and press `prefix + I` to install the plugins defined in the configuration.

#### tmux tools

- Requires tmux, zoxide and fzf, which were installed earlier.
- Clone the tools to `~/.config/tmux` from [here](https://github.com/Aapok0/tmux-tools):

```bash
git clone https://github.com/Aapok0/tmux-tools.git ~/.config/tmux/tmux-tools
```

- Make symbolic links of the tools to a bin in path (make sure to replace with the absolute path of the tool):

```bash
sudo ln -s /absolute/path/to/home/.config/tmux/tmux-tools/tmuxz /usr/local/bin/tmuxz
```

```bash
sudo ln -s /absolute/path/to/home/.config/tmux/tmux-tools/tmuxf /usr/local/bin/tmuxf
```

### Gitconfig

- Clone configuration to `~/.config/gitconfig` from [here](https://github.com/Aapok0/gitconfig):

```bash
git clone https://github.com/Aapok0/gitconfig.git ~/.config/gitconfig
```

- Install git-delta with homebrew:

```bash
brew install git-delta
```

- Make symbolic link of the gitconfig to home (replace absolute path with the actual path:

```bash
sudo ln -s /absolute/path/to/home/.config/gitconfig/.gitconfig /absolute/path/to/home/.gitconfig
```

### SSH key

- Create ssh key with following command (if default key name is fine, remove -f option):

```bash
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/your_key_name
```

- Start an SSH Agent for the current shell:

```bash
ssh-agent -s
```

- Add key to agent with the following command:

```bash
ssh-add ~/.ssh/your_key_name
```

## Apps

### Menu bar apps

#### Hiddenbar

- Install hiddenbar with homebrew:

```bash
brew install --cask hiddenbar
```

- Open app.
  - There might be difficulties with this -> find the app in finder and open from there by clicking with control and choosing open.
- Make sure it's set to open, when logging in.
  - Preferences can be later opened by pressing the vertical bar in menu bar.
- Open the hiddenbar and drag apps (while pressing command) you don't need always visible in the menu bar to the left of the vertical bar.
  - Disclaimer: on the laptop display, the camera notch prevents you from seeing all the apps, if there's too many of them. They can however be seen in an external display.

#### Stats

- Install stats with homebrew:

```bash
brew install --cask stats
```

- Make sure it starts at login.
- Show SSD, RAM, CPU, network, battery and clock.
  - Change network widget pictogram to arrows.
  - Make system's clock and date (will add calendar with next app) as minimal as possible.
    - From system settings -> control centre -> menu bar only -> clock -> clock options, show date never andmake time style analogue.
      - Might need restart to change.

#### Itsycal

- Install itsycal with homebrew:

```bash
brew install --cask itsycal
```

- Make sure it starts at login.
- Show month and day of week.

### Alt-tab

- Install Alt-tab with homebrew:

```bash
brew install --cask alt-tab
```

- Open app and give permissions, when prompted.
- Make sure it starts at login.
- Change shortcut to command + tab.

### Password manager

- Bitwarden for personal:

```bash
brew install --cask bitwarden
```

- Usually KeepassXC for work:

```bash
brew install --cask keepassxc
```

- Install Raycast extension/s.
  - command + , to open settings -> extensions -> +-sign -> install from store.

### Firefox

- Install regular firefox or developer edition using homebrew:

```bash
brew install --cask firefox
```

```bash
brew install --cask homebrew/cask-versions/firefox-developer-edition
```

- Open and make default browser, when prompted.

#### Settings

##### General

- Open previous windows and tabs.
- Change to dark theme.
- Use your operating system setting for "English (Finland)" to format dates, times, numbers, and measurements.
- Always ask you where to save files.

##### Home

- Blank page as home, new window and new tab (will install add-on for this later).
- Remove all home content.

##### Search

- DuckDuckGo as default search engine.
- Remove Google and Bing as search shortcuts (can still use !g as google etc.).

##### Privacy & Security

- Tell websites not to sell or share my data.
- Send websites a "Do Not Track" request.
- Do not ask to save passwords.
- No data collection.

#### Add-ons

- Tabliss
  - Have it be default, when prompted.
- OneTab
  - Pin to toolbar.
- Tab Session Manager
  - Pin to toolbar.
- Dark Reader
  - Pin to toolbar.
  - Inverted list only -> add sites when needed.
- uBlock Origin
  - Pin to toolbar.
- Privacy Badger
  - Pin to toolbar.
- Decentraleyes
- Add-on for the password manager/s you use.
  - Pin to toolbar.

#### Toolbar and UI

- Show bookmarks bar.
- Remove Firefox View on the left side.
- Remove flex space, pocket and other not needed things from toolbar and organize add-ons according to usage.

### VS Code

#### Settings

- TBD

#### Extensions

- TBD

### Docker Desktop and Kubernetes

- Install Docker Desktop with homebrew (kubectl comes with it):

```bash
brew install --cask docker
```

- Choose dark theme.
- At least 4 cores, 8GB momery and 64GB disk.
- Need to enable Kubernetes to use it.
- Install helm with homebrew:

```bash
brew install helm
```

### Wireshark

- Install Wireshark with homebrew:

```bash
brew install --cask wireshark
```

### Media apps

- Install VLC Player and Spotify with homebrew:

```bash
brew install --cask vlc spotify
```

### Android file transfer

- Install Android file transfer with homebrew:

```bash
brew install --cask android-file-transfer
```

### Future considerations

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
- ATA (ChatGPT in terminal)
- ImageMagick (image conversion/resizing/etc in terminal)
