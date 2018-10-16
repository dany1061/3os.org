# Zsh (shell) on Steroids

This will Install oh-my-zsh shell with fish shell like history, auto suggestions and syntax highlighting.

## Requirements:

```bash
apt-get install git wget zsh
```

## Install oh-my-zsh

```bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

## Install Plugins

This will create ~/.zsh folder and clone plugins from git:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.zsh/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-history-substring-search ~/.zsh/zsh-zsh-history-substring-search
```

## Add plugins to ~/.zshrc:

```bash
echo "source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc && source ~/.zshrc
echo "source ~/.zsh/zsh-zsh-history-substring-search/zsh-history-substring-search.zsh" >> ~/.zshrc && source ~/.zshrc
echo "source ~/.zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc && source ~/.zshrc
```

`Note: make sure zsh-syntax-highlighting is the last one in the above list.`

Restart zsh

## Make Zsh default shell:

```bash
chsh -s $(which zsh)
```

## Optional:

### Fix background theme issues(not necessary depends on your theme.)

```bash
echo "ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=white'" >> ~/.zshrc && source ~/.zshrc
```

Restart zsh
