# Better Terminal Experience - Oh-My-Zsh + Powerlevel9k Theme + Font-Awesome-Terminal

## WORK IN PROGRESS

Linux Terminal:

![Linux Terminal](../assets/images/guides/betterTerminal/linuxTerminal.png)

## MacOS Installation with iTerm2 and Homebrew

First of all we need to install [__Homebrew__](https://brew.sh/)

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

This will install all the necessary requirements:

```bash
brew tap homebrew/cask-fonts
brew install zsh-autosuggestions zsh-syntax-highlighting git wget zsh
brew cask install iterm2 font-awesome-terminal-fonts font-firacode-nerd-font
```

Install [__Oh-My-Zsh__](https://github.com/robbyrussell/oh-my-zsh)

```bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

### ~/.zshrc Config Modifications for MacOS

Set theme and fonts:

```bash
POWERLEVEL9K_MODE='awesome-fontconfig'
ZSH_THEME="powerlevel9k/powerlevel9k"
```

Add this to the the end of ~/.zshrc

```bash
### Theme and Plugins
## POWERLEVEL9K Config
POWERLEVEL9K_PROMPT_ADD_NEWLINE=true
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(
  # time
  custom_hostname
  custom_username
  dir
  vcs
  newline
)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(
  status
  # root_indicator
  # background_jobs
  # history
  time
)

# Custom Hostname & Username prompt segment
POWERLEVEL9K_CUSTOM_HOSTNAME="echo -n $(hostname) | sed 's/\..*$//' "
POWERLEVEL9K_CUSTOM_HOSTNAME_FOREGROUND="black"
POWERLEVEL9K_CUSTOM_HOSTNAME_BACKGROUND="white"
POWERLEVEL9K_CUSTOM_USERNAME="echo -n ${USER}"
POWERLEVEL9K_CUSTOM_HOSTNAME_FOREGROUND="black"
POWERLEVEL9K_CUSTOM_USERNAME_BACKGROUND="grey"

## Shell Integration and plugins
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/local/share/zsh-autosuggestions/zsh-autosuggestions.zsh
## Fix for Slow zsh-autosuggestions copy&paste
autoload -Uz bracketed-paste-magic
zle -N bracketed-paste bracketed-paste-magic
zstyle ':bracketed-paste-magic' active-widgets '.self-*'
```

## Linux Installation

Requirements: git, zsh

Install [__Oh-My-Zsh__](https://github.com/robbyrussell/oh-my-zsh)

```bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

Install Powerlevel9k Theme for Oh-My-Zsh

```bash
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```

Install Autosuggestions, Syntax-Highlighting Plugins

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Install Awesome-Terminal-Fonts

```bash
git clone https://github.com/gabrielelana/awesome-terminal-fonts.git
cp -r awesome-terminal-fonts/build ~/.fonts
rm -rf awesome-terminal-fonts
cd ~/.fonts
fc-cache -fv ~/.fonts
```

### ~/.zshrc Config Modifications for Linux

Set theme and fonts:

```bash
POWERLEVEL9K_MODE='awesome-fontconfig'
ZSH_THEME="powerlevel9k/powerlevel9k"
```

Activate the plugins

```bash
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```

Add this to the the end of ~/.zshrc

```bash
### Theme and Plugins
## POWERLEVEL9K Config
POWERLEVEL9K_PROMPT_ADD_NEWLINE=true
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(
  # time
  custom_hostname
  custom_username
  dir
  vcs
  newline
)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(
  status
  # root_indicator
  # background_jobs
  # history
  time
)

# Custom Hostname & Username prompt segment
POWERLEVEL9K_CUSTOM_HOSTNAME="echo -n $(hostname) | sed 's/\..*$//' "
POWERLEVEL9K_CUSTOM_HOSTNAME_FOREGROUND="black"
POWERLEVEL9K_CUSTOM_HOSTNAME_BACKGROUND="white"
POWERLEVEL9K_CUSTOM_USERNAME="echo -n ${USER}"
POWERLEVEL9K_CUSTOM_HOSTNAME_FOREGROUND="black"
POWERLEVEL9K_CUSTOM_USERNAME_BACKGROUND="grey"

## Fix for Slow zsh-autosuggestions copy&paste
autoload -Uz bracketed-paste-magic
zle -N bracketed-paste bracketed-paste-magic
zstyle ':bracketed-paste-magic' active-widgets '.self-*'
```