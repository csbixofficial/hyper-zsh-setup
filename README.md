# Step-by-Step Guide to Set Up Hyper Terminal on Mac

This guide walks you through setting up Hyper Terminal with ZSH, customizing the terminal appearance, installing plugins, and enhancing the experience with themes.

## Install Homebrew

If you don’t have Homebrew installed on your Mac, open the Terminal and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

* Source: [brew.sh](https://brew.sh/)

## Install Hyper Terminal

To install Hyper Terminal using Homebrew:

```bash
brew install --cask hyper
```

After installation, open the Hyper terminal by launching `Hyper.app` from the Applications folder.

## Configure ZSH Shell

ZSH is the default shell on macOS, so you don’t need to install it separately. However, you should configure it properly.

### Remove the ‘Last Login’ Prompt (Optional)

Run the following command to remove the "Last login" message that appears when you open a new terminal window:

```bash
cd ~ && touch .hushlogin
```

### Set the Tab Title to Current Directory

* Open the ZSH configuration file in VS Code:

```bash
code ~/.zshrc
```

* Uncomment the `DISABLE_AUTO_TITLE="true"` line and add the following code to set the tab title to your current directory:

```bash
# The zsh precmd function to set terminal tab title to the current working directory.
precmd () {
    tab_title="\\033]0;${PWD##*/}\\007"
    echo -ne "$tab_title"
}
```

## Customize Hyper Terminal

### Edit Hyper Configuration

* Open the Hyper configuration file using VS Code:

```bash
code ~/.hyper.js
```

To customize the cursor, add the following to the `config` section:

```javascript
cursorShape: 'BEAM',  // Change cursor shape to beam
cursorBlink: true,    // Enable blinking cursor
```

### Install Plugins

#### hyperpower

* This plugin animates your terminal's prompt.
* Install with:

```bash
hyper i hyperpower
```

* Source: [hyperpower](https://hyper.is/store/hyperpower)

#### hyperborder

* This plugin adds animated borders around the terminal.
* To install, first add it in the `plugins` section of your `~/.hyper.js` file like this:

```javascript
plugins: ["hyperborder"]
```

* Then, configure the border:

```javascript
module.exports = {
  config: {
    hyperBorder: {
      borderColors: ['random', 'random'],
      borderWidth: '4px',
      animate: true,
    }
  }
}
```

* Source: [hyperborder](https://github.com/webmatze/hyperborder)

## ZSH Plugins

### Oh My ZSH

* Install Oh My Zsh:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

* Source: [ohmyz.sh](https://ohmyz.sh/#install)

### zsh-autosuggestions

* Install this plugin to get command suggestions as you type:

```bash
brew install zsh-autosuggestions
```

* Add this at the end of your `~/.zshrc` file to to enable the plugin:

```bash
source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh
```

* Source: [Install with Homebrew](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#homebrew)

### zsh-syntax-highlighting

* Install this plugin to highlight syntax:

```bash
brew install zsh-autosuggestions
```

* Add this at the end of your `~/.zshrc` file to enable the plugin:

```bash
source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

## Install and Configure Fonts

### Install MesloLGS NF Font

* Download and install the `MesloLGS NF` font from [here](https://github.com/romkatv/powerlevel10k#manual-font-installation).

### Configure Hyper

* Open `~/.hyper.js` and set:

```javascript
fontFamily: 'MesloLGS NF',
fontSize: 12,
```

### Configure ZSH

* Open `Terminal.app`
* Go to `Terminal > Settings > Profiles > Basic > Text > Font`, and select `MesloLGS NF Regular` and set font size to `12`.

### (Optional) Configure VS Code

* Open `settings.json` and add:

```json
"terminal.integrated.fontFamily": "MesloLGS NF",
"terminal.integrated.fontSize": 14,
```

* You can also add the following to add some extra customizations:

```bash
"terminal.integrated.cursorStyle": "line",
"terminal.integrated.cursorBlinking": true,
"terminal.integrated.enablePersistentSessions": false,
"editor.fontFamily": "Fira Code",
"editor.fontSize": 14,
"editor.unicodeHighlight.nonBasicASCII": false,
```

## Install and Configure Themes

### Powerlevel10k

* Install Powerlevel10k:

```bash
brew install powerlevel10k
```

* Add this at the end of your `~/.zshrc` file to enable the plugin:

```bash
source $(brew --prefix)/share/powerlevel10k/powerlevel10k.zsh-theme
```

* Run `p10k configure` in the terminal to configure the prompt.
* Source: [Install with Homebrew](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#homebrew)

> To allow `powerlevel10k` take impact properly, run `p10k configure` after installing the theme.

### hyper-night-owl

* Install the plugin:

```bash
hyper i hyper-night-owl
```

* Source: [hyper-night-owl](https://hyper.is/store/hyper-night-owl)

> After installation, restart Hyper for the changes to take effect.

### (Optional) Night Owl in PyCharm

* To have the same theme as hyper, install [Night Owl Theme](https://plugins.jetbrains.com/plugin/12262-night-owl-theme) in PyCharm.

### (Optional) Atom Material Icons

* PyCharm: [Atom Material Icons](https://plugins.jetbrains.com/plugin/10044-atom-material-icons)
* Google Chrome: [Atom Material Icons](https://chrome.google.com/webstore/detail/atom-material-icons/pljfkbaipkidhmaljaaakibigbcmmpnc)

### Remove OS Icon from Prompt

* Open `~/.p10k.zsh`.
* Comment the `os_icon` as follows:

```bash
# The list of segments shown on the left. Fill it with the most important segments.
typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(
    # os_icon                 # os identifier
    dir                     # current directory
    vcs                     # git status
    # prompt_char           # prompt symbol
)
```

### How to Uninstall a Theme or Plugin

* In case you want to unstall a theme or plugin, you can do that via `hyper uninstall <theme or plugin name>`. 
* Example: `hyper uninstall hyper-material-theme`.
