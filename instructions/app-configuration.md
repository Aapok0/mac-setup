# App Configuration

## Raycast

- Do not choose clipboard or window management features.
- Disable spotlight shortcut from system settings -> keyboard -> shortcuts.
- Set command + space as the shortcut for Raycast.
- Install homebrew, Google Translate, Search Word, Phind Search and YouTube extension:
  - command + , to open settings -> extensions -> +-sign -> install from store.

## Rectangle

- Make sure it starts at login.

## Menu Bar Apps

### Hiddenbar

- Open app.
  - There might be difficulties with this -> find the app in finder and open from there by clicking with control and choosing open.
- Make sure it's set to open, when logging in.
  - Preferences can be later opened by pressing the vertical bar in menu bar.
- Open the hiddenbar and drag apps (while pressing command) you don't need always visible in the menu bar to the left of the vertical bar.
  - Disclaimer: on the laptop display, the camera notch prevents you from seeing all the apps, if there's too many of them. They can however be seen in an external display.

### Stats

- Make sure it starts at login.
- Show SSD, RAM, CPU, network, battery and clock.
  - Change network widget pictogram to arrows.
  - Make system's clock and date (will add calendar with next app) as minimal as possible.
    - From system settings -> control centre -> menu bar only -> clock -> clock options, show date never and make time style analogue.
      - Might need restart to change.

### Itsycal

- Make sure it starts at login.
- Show month and day of week.

## Password Manager

- Bitwarden for personal.
- KeepassXC for work.
- Install Raycast extension/s:
  - command + , to open settings -> extensions -> +-sign -> install from store.

## Firefox

### Settings

#### General

- Open previous windows and tabs.
- Change to dark theme.
- Use your operating system setting for "English (Finland)" to format dates, times, numbers, and measurements.
- Always ask you where to save files.

#### Home

- Blank page as home, new window and new tab (will install add-on for this later).
- Remove all home content.

#### Search

- DuckDuckGo as default search engine.
- Remove Google and Bing as search shortcuts (can still use !g as google etc.).

#### Privacy & Security

- Tell websites not to sell or share my data.
- Send websites a "Do Not Track" request.
- Do not ask to save passwords.
- No data collection.

### Add-ons

- Tabliss — set as default when prompted.
- OneTab — pin to toolbar.
- Tab Session Manager — pin to toolbar.
- Dark Reader — pin to toolbar. Inverted list only, add sites when needed.
- uBlock Origin — pin to toolbar.
- Privacy Badger — pin to toolbar.
- Decentraleyes.
- Add-on for password manager/s — pin to toolbar.

### Toolbar and UI

- Show bookmarks bar.
- Remove Firefox View on the left side.
- Remove flex space, pocket and other not needed things from toolbar and organize add-ons according to usage.

## Docker Desktop

- Choose dark theme.
- At least 4 cores, 8GB memory and 64GB disk.
- Need to enable Kubernetes to use it.
- Add zsh completions for docker by adding following command to `~/.config/zsh/.zshrc`:

```bash
source <(docker completion zsh)
```

## Neovim

- Open nvim and let lazy.nvim install plugins.
- Install Mason tools:

```bash
:MasonInstall shellcheck shfmt stylua prettier ruff hadolint tflint ansible-lint
```

## tmux

- Open tmux and press `ctrl+space I` to install plugins.

## Future Considerations

- Velja (choose which browser opens what link)
- Ejectify (usb control)
- Cron (calendar)
- Spark (mail)
- TempBox or mailsy (temporary email addresses)
- Shotrr (screenshots)
- ImageOptim (strip image metadata and reduce quality to save space)
- OnyX (system/disk level stuff)
- MenubarX (browser in the menubar)
