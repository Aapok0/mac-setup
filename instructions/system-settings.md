# macOS System Settings

## Touch ID & Password

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

## General

- Search and install any software updates.
- Make sure Language & Region has all correct units.

## Appearance

- Switch to dark mode.
- Disable wallpaper tinting in windows.
  - To make sure accurate colors are used.
- Always show scrollbars.

## Displays

- Do not automatically adjust brightness.
  - To have brightness always be what you want.
- Disable true tone.
  - To make sure accurate colors are used.

## Battery

- From options, do not slightly dim the display on battery.
  - To have brightness always be what you want.

## Accessability

- From pointer control and trackpad options choose three-finger dragging style.

## Trackpad

- Make sure tap to click is enabled.

## Keyboard

- From text input click edit.
  - Disable spell check.
  - Disable capitalization.
  - Disable smart quotes and dashes.
    - So quotes are not changed to something that does not work in code or terminal.

## Lock Screen

- Change the display off settings to something reasonable.

## Control Centre

- Show bluetooth in menu bar.

## Desktop & Dock

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

## Screenshots

- Change screenshot default file type to jpg with the following command (default is png -> much bigger files):

```bash
defaults write com.apple.screencapture type jpg
```

- Change screenshot default location `$HOME/Pictures/Screenshots` with the following commands (default is Desktop):

```bash
mkdir $HOME/Pictures/Screenshots
```

```bash
defaults write com.apple.screencapture location "$HOME/Pictures/Screenshots"
```

## iCloud

- Disable anything related to iCloud, if it's a requirement from e.g. work.
