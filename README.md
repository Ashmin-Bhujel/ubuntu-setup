# Ubuntu Setup

## Install Ubuntu

- Make a bootable drive for Ubuntu
- Boot with the drive
- Install Ubuntu with appropriate configurations

## Update The Packages

```bash
sudo apt update
sudo apt upgrade
sudo apt install nala git
sudo nala full-upgrade
```

## Update Snap Store

```bash
sudo snap refresh snap-store
```

- Uninstall snap version of Firefox browser

## Install Necessary Packages

```bash
sudo nala install curl wget git git-flow build-essential net-tools gnome-tweaks gnome-shell-extension-manager btop gdb ubuntu-restricted-extras vlc libgtop2-dev fzf ripgrep bat fd-find
```

## Install Fastfetch

```bash
sudo add-apt-repository ppa:zhangsongcui3371/fastfetch
sudo nala update
sudo nala install fastfetch
```

## Install Ghostty Terminal

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/mkasberg/ghostty-ubuntu/HEAD/install.sh)"
```

## Setup Zsh and Oh My Zsh

1. Install Zsh

   ```bash
   sudo nala install zsh
   ```

2. Setup Oh My Zsh

   ```bash
   sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```

3. Add `zsh-syntax-highlighting` plugin

   ```bash
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```

   - Add `zsh-syntax-highlighting` in plugins list inside `.zshrc` file

4. Install `spaceship-prompt` theme for Oh My Zsh

   ```bash
   git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
   ```

   ```bash
   ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
   ```

   - Set `ZSH_THEME="spaceship"` in your `.zshrc` file

## Setup Ubuntu's look and feel

1. Tweak system settings

2. Gnome extensions
   - Appindicator and KStausNotifierItem Support - [ 3v1n0 ] `Disable the default Appindicator First`
   - Clipboard Indicator - [ Tudmotu ]
   - System Monitor - [ fmuellner ]
   - Logo Menu - [ Aryan Kausik ]
     - Extension Manager
     - Software Center: snap-store
   - Transparent Top Bar [ Gonzague ]
   - Ubuntu Dock
     - Icon Size: 32
     - Behaviour - { CA: Focus, minimize or show preview, SA: Cycle through windows }
     - Appearance - { Indicator: Dots (Dominant color), Dynamic: 0 to 100 }

## Install Web Browser

- Brave browser (Chromium based)

  ```bash
  curl -fsS https://dl.brave.com/install.sh | sh
  ```

  - Setup Brave browser
  - Import Bookmarks
  - Extensions
    - Dark Reader
    - JSON Formatter [Dark: Ayu Dark, Light: Xq Light]
    - Material Icons for GitHub
    - React Developer Tools
    - Redux DevTools
    - Wappalyzer
    - WhatFont

- Zen browser (Firefox based)

  - Install Zen browser using tarball script

    ```bash
    bash <(curl -s https://updates.zen-browser.app/install.sh)
    ```

  - Create a `zen-local` file inside `/etc/apparmor.d` directory with the following content if a warning pop us when starting up the browser

    **NOTE:** Replace {username} with your username, There will also some configurations needed to be done after initial startup.

    ```bash
    # This profile allows everything and only exists to give the
    # application a name instead of having the label "unconfined"
    abi <abi/4.0>,
    include <tunables/global>
    profile zen-local
    /home/{username}/.tarball-installations/zen/{zen,zen-bin,updater}
    flags=(unconfined) {
      userns,
      # Site-specific additions and overrides. See local/README for details.
      include if exists <local/zen>
    }
    ```

  - Extensions

    - Zen Mods

      - Floating status bar
      - Smaller compact mode

    - Dark Reader
    - uBlock Origin
    - JSON Formatter
    - Wappalyzer
    - WhatFont
    - Material Icons for GitHub

## Install Other GUI Applications

- Spotify Music Player

  ```bash
  curl -sS https://download.spotify.com/debian/pubkey_C85668DF69375001.gpg | sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/spotify.gpg
  echo "deb https://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
  sudo nala update
  sudo nala install spotify-client
  ```

- OBS Studio

  ```bash
  sudo add-apt-repository ppa:obsproject/obs-studio
  sudo nala update
  sudo nala install ffmpeg obs-studio
  ```

## Install Development Tools

- Setup Git and GitHub

  - Git config

    ```bash
    git config --global user.name "Your Name"
    ```

    ```bash
    git config --global user.email "Your Email"
    ```

    ```bash
    git config --global init.defaultBranch "main"
    ```

  - Lazygit

    ```bash
    LAZYGIT_VERSION=$(curl -s "https://api.github.com/repos/jesseduffield/lazygit/releases/latest" | \grep -Po '"tag_name": *"v\K[^"]*')
    curl -Lo lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/download/v${LAZYGIT_VERSION}/lazygit_${LAZYGIT_VERSION}_Linux_x86_64.tar.gz"
    tar xf lazygit.tar.gz lazygit
    sudo install lazygit -D -t /usr/local/bin/
    ```

  - Setup SSH key

    ```bash
    ssh-keygen
    ```

    - Copy the public key from `.ssh/` directory
    - Go to GitHub > Settings > SSH and GPG Keys then add the generated SSH key
    - Check the connection by `ssh -T git@github`

- Zed Code Editor (Rust Based)

  ```bash
  curl -f https://zed.dev/install.sh | sh
  ```

- VS Code [Optional]

  - Download and install the `.deb` setup file from the official website
  - Login to GitHub account and setup VS Code

- Tmux

  ```bash
  sudo nala install tmux
  git clone https://github.com/tmux-plugins/tpm ~/.config/tmux/plugins/tpm
  ```

- Node.js

  **Note:** Its recommended to visit the official [Node.js](https://nodejs.org/en) site for latest version of installation command.

  ```bash
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
  nvm install --lts
  ```

- Bun.js

  ```bash
  curl -fsSL https://bun.sh/install | bash
  ```

- PNPM

  ```bash
  curl -fsSL https://get.pnpm.io/install.sh | sh -
  ```

- uv and Python

  - Install `uv`

    ```bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
    ```

  - Install `python`

    ```bash
    uv python install
    ```

- Neovim [Optional]

  ```bash
  curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim-linux-x86_64.tar.gz
  sudo rm -rf /opt/nvim-linux-x86_64
  sudo tar -C /opt -xzf nvim-linux-x86_64.tar.gz
  ```

  Then add this to your shell config (~/.bashrc or ~/.zshrc or other)

  ```bash
  export PATH="$PATH:/opt/nvim-linux-x86_64/bin"
  ```

  - Lazyvim

    ```bash
    git clone https://github.com/LazyVim/starter ~/.config/nvim
    ```

    Use the `LazyExtra` and `TSInstall` command to install required plugins, LSPs, etc.

- Docker

  **Note:** Follow the post install steps for Docker engine

  Visit Docker Engine [installation site](https://docs.docker.com/engine/install/ubuntu/).

  - Lazydocker

    ```bash
    curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash
    ```
