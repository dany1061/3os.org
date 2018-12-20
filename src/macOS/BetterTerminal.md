# macOS Better Terminal - iTerm2, Oh-My-Zsh, Theme & Fonts Guide

## WORK IN PROGRESS!!!

## Installation

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

## ~/.zshrc Config Highlights

```bash
POWERLEVEL9K_MODE='awesome-fontconfig'
ZSH_THEME="powerlevel9k/powerlevel9k"

plugins=(
  git
  colored-man-pages
  docker
  iterm2
  nmap
  node
  npm
  
)

# Locale
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8

# Ruby Configuration for Brew
export PATH="/usr/local/opt/ruby/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/ruby/lib"
export CPPFLAGS="-I/usr/local/opt/ruby/include"
export PKG_CONFIG_PATH="/usr/local/opt/ruby/lib/pkgconfig"

# POWERLEVEL9K Config
POWERLEVEL9K_PROMPT_ADD_NEWLINE=true
POWERLEVEL9K_MODE='nerdfont-complete'

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



# Shell Integration and plugins
source "${HOME}/.iterm2_shell_integration.zsh"
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/local/share/zsh-autosuggestions/zsh-autosuggestions.zsh
## Fix for Slow zsh-autosuggestions copy&paste
autoload -Uz bracketed-paste-magic
zle -N bracketed-paste bracketed-paste-magic
zstyle ':bracketed-paste-magic' active-widgets '.self-*'
```