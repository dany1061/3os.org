title: MacOS Tips & Guides
description: MacOS Tips & Guides, examples and simple usage

# MacOS Tips & Guides

## Hide All The Icons On Your Desktop

Disable Icons:

```bash
defaults write com.apple.finder CreateDesktop false
killall Finder
```

Enable Icons:

```bash
defaults write com.apple.finder CreateDesktop true
killall Finder
```

## Force RGB mode For External Screens

Download this script from [github](https://gist.github.com/adaugherity/7435890)
Extract the file and run it:

```bash
ruby patch-edid.rb
```

This will create new directory named: `DisplayVendorID-*` at the root directory of the script.

- Power off your mac
- Boot to into the recovery system (Cmd+R during boot).
- Run Disk `Disk Utility`, choose the boot drive and hit `Mount`, exit `Disk Utility`
- Click `Utilities` and then `Terminal`

`Remember that every path is now prefixed by “/Volumes/Macintosh HD/”.`

- Copy `DisplayVendorID-*` E.g. I had the Ruby script in a folder “EDID-Fix” on my desktop.

```bash
cp -r /Volumes/Macintosh\ HD/Users/marcus/Desktop/EDID-Fix/DisplayVendorID-* /Volumes/Macintosh\ HD/System/Library/Displays/Contents/Resources/Overrides/
```

- Reboot to your system.
- Go to Settings - Displays - Color.
- Choose the new color profile for your external screen.

## Set the `Same View Options` for all Finder windows

First, we want to set the default view options for all new Finder windows. To do so, open Finder and click on the view setting that you want to use. The settings are four icons and the top of your Finder window.
If you don't see the Finder toolbar type:

```bash
cmd + option + t
```

After selecting the option you want, type:

```bash
cmd + j
```

to open the view options window.

Make sure you check the top two checkboxes that say Always open in list view and Browse in list view. Keep in mind it will reflect whichever view you've selected.

Now click the button at the bottom that says "Use as Defaults".

### Delete all .DS_Store files on your computer

Chances are you've opened some Finder windows in the past. Individual folder options will override this default setting that we just set.

In order reset your folder settings across the entire machine we have to delete all .DS_Store files. This will ensure that all folders start fresh. Open up the Terminal application (Applications/Utilities/Terminal), and type:

```bash
sudo find / -name .DS_Store -delete; killall Finder
```

`Note: In the future, whenever you switch views, it will automatically save in the new .DS_Store file. This will override the default settings.`

## Installing rbenv (ruby send box) - Ruby alternative to the one that macOS uses

Install rbenv with brew

```bash
brew install rbenv
```

Add eval `"$(rbenv init -)"` to the end of `~/.zshrc` or `~/.bash_profile`

Install a ruby version

```bash
rbenv install 2.3.1
```

Select a ruby version by rbenv

```bash
rbenv global 2.3.1
```

Open a new terminal window

Verify that the right gem folder is being used with `gem env home`(should report something in your user folder not system wide)

## Running Multi Session - Burp Suite

Launch the Script Editor choose temporary folder

copy this:

```bash
do shell script "open -n /Applications/Burp\\ Suite\\ Professional.app"
```

File > Export

Use the following settings:

Save AS As: `Burp Multi Session`
Where: `Applications`
File Format: `Application`

Right Click on the new "Burp Multi Session" application.
Drug the original application to the icon in the left corner of the "get info"

## Firefox Profile Manager Application.md

Launch the Script Editor choose temporary folder

copy this:

```bash
do shell script "/Applications/Firefox.app/Contents/MacOS/firefox -ProfileManager &> /dev/null &"
```

File > Export

Use the following settings:

Save AS As: `Firefox Profile Manager`
Where: `Applications`
File Format: `Application`

Right Click on the new "Burp Multi Session" application.
Drug the original application to the icon in the left corner of the "get info"

## Add Macbook Keybourd Layout for ubuntu

for desktop:

```bash
gsettings set org.gnome.desktop.input-sources xkb-options "['apple:badmap']"
```

Terminal command to disable the option:

```bash
gsettings reset org.gnome.desktop.input-sources xkb-options
```

<!-- for headless (server):

```bash
sudo apt-get install keyboard-configuration console-data console-setup console-locales
sudo dpkg-reconfigure keyboard-configuration
```

-> MacBook / MacBookPro (Intl)

-> English

-> English

-> Right Alt (AltGr)

-> No Compose Key -->

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->