title: Linux - Installing oh-my-zsh Shell
description: Linux - Installing oh-my-zsh Shell how to, guides, examples, and simple usage

# Installing oh-my-zsh Shell

This will Install oh-my-zsh shell with fish shell like history, auto suggestions and syntax highlighting.

## Requirements

```bash
apt-get install git wget zsh
```

## Install oh-my-zsh

```bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

## Make Zsh default shell

```bash
chsh -s $(which zsh)
```

## Bonus

Edit `zshrc`
 and choose one of those themes from this [list](https://github.com/robbyrussell/oh-my-zsh/wiki/themes "oh-my-zsh themes")  
My favorite one is `fishy`

```bash
nano ~/.zshrc
```

look for the `ZSH_THEME=""` it should look like this:

```bash
# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
ZSH_THEME="fishy"
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="220px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->