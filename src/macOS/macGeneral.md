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

## Change the Launchpad Grid Layout

Change the _springboard-columns_ and _springboard-rows_ values according to your preference

```bash
write com.apple.dock springboard-columns -int 9
write com.apple.dock springboard-rows -int 7
write com.apple.dock ResetLaunchPad -bool TRUE
killall Dock
```

## Disable StrictHostKeyChecking in SSH

To disable strict host checking on OS X for the current user,
create or edit ~/.ssh/ssh_config and add the following lines:

```bash
   StrictHostKeyChecking no
```

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

## List listening Ports and Programs and Users

```bash
sudo lsof -i -P | grep -i "listen"
```

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

Right Click on the new "Firefox Profile Manager" application.
Drug the original application to the icon in the left corner of the "get info"

## Disable/Enable SIP (System Integrity Protection)

Reboot your Mac into Recovery Mode by restarting your computer and holding down **Command+R** until the Apple logo appears on your screen.  
Click _Utilities > Terminal._  
In the Terminal window, type in:

Status:

```bash
csrutil status
```

Disable:

```bash
csrutil disable
```

Enable:

```bash
csrutil enable
```

Press Enter and restart your Mac.

## Syntax Highlighting In Nano on Mac OS X

Install Nano from homebrew
Create _nanorc_ file with the syntax below

```bash
brew install nano
nano ~/.nanorc
```

nanorc:

```bash
include /usr/local/share/nano/asm.nanorc
include /usr/local/share/nano/awk.nanorc
include /usr/local/share/nano/c.nanorc
include /usr/local/share/nano/cmake.nanorc
include /usr/local/share/nano/css.nanorc
include /usr/local/share/nano/debian.nanorc
include /usr/local/share/nano/fortran.nanorc
include /usr/local/share/nano/gentoo.nanorc
include /usr/local/share/nano/groff.nanorc
include /usr/local/share/nano/html.nanorc
include /usr/local/share/nano/java.nanorc
include /usr/local/share/nano/makefile.nanorc
include /usr/local/share/nano/man.nanorc
include /usr/local/share/nano/mgp.nanorc
include /usr/local/share/nano/mutt.nanorc
include /usr/local/share/nano/nanorc.nanorc
include /usr/local/share/nano/objc.nanorc
include /usr/local/share/nano/ocaml.nanorc
include /usr/local/share/nano/patch.nanorc
include /usr/local/share/nano/perl.nanorc
include /usr/local/share/nano/php.nanorc
include /usr/local/share/nano/pov.nanorc
include /usr/local/share/nano/python.nanorc
include /usr/local/share/nano/ruby.nanorc
include /usr/local/share/nano/sh.nanorc
include /usr/local/share/nano/tcl.nanorc
include /usr/local/share/nano/tex.nanorc
```

Save & Exit

```bash
source ~/.zshrc
```

## Reset Launchpad Icons Sort

```bash
defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock
```

## Import RSA Keys

Copy your id_rsa, id_rsa.pub to _~/.ssh/_ folder

Step 1 - Store the key in the keychain
Just do this once:

```bash
ssh-add -K ~/.ssh/[your-private-key]
```

Enter your key passphrase, and you won't be asked for it again.

(If you're on a pre-Sierra version of OSX, you're done, Step 2 is not required.)

Step 2 - Configure SSH to always use the keychain
It seems that OSX Sierra removed the convenient behavior of persisting your keys between logins, and the update to ssh no longer uses the keychain by default. Because of this, you will get prompted to enter the passphrase for a key after you upgrade, and again after each restart.

The solution is fairly simple, and is outlined in this github thread comment. Here's how you set it up:

Ensure you've completed Step 1 above to store the key in the keychain.

If you haven't already, create an ~/.ssh/config file. In other words, in the .ssh directory in your home dir, make a file called config.

In that .ssh/config file, add the following lines:

```bash
Host *
  UseKeychain yes
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_rsa
```

Change ~/.ssh/id_rsa to the actual filename of your private key. If you have other private keys in your ~.ssh directory, also add an IdentityFile line for each of them. For example, I have one additional line that reads IdentityFile ~/.ssh/id_ed25519 for a 2nd private key.

The UseKeychain yes is the key part, which tells SSH to look in your OSX keychain for the key passphrase.

That's it! Next time you load any ssh connection, it will try the private keys you've specified, and it will look for their passphrase in the OSX keychain. No passphrase typing required.

## Change Login Screen Background

Backup the priginal picture

```bash
sudo mv /Library/Desktop\ Pictures/Mojave.heic /Library/Desktop\ Pictures/Mojave.heic.bak
```

Rename new picture to __Mojave.heic__

Move the new picture to _/Library/Desktop\ Pictures/_

## Google Drive File Sync Fix

quit Google Drive

```bash
cd ~/Library/Application\ Support/Google
mv DriveFS DriveFS.old
```

relaunch Google Drive

## Flush DNS

```bash
sudo killall -HUP mDNSResponder;sudo killall mDNSResponderHelper;sudo dscacheutil -flushcache
```

## Using Alt/Cmd + Right/Left Arrow in iTerm

Go to iTerm Preferences → Profiles, select your profile, then the Keys tab. Click Load Preset... and choose Natural Text Editing.

## Term2: how to remove the right arrow before the cursor line

you can turn it off by going in to Preferences > Profiles > (your profile) > Terminal, scroll down to "Shell Integration", and turn off "Show mark indicators".

## External MacOS Wireless USB Adapter Support

Based on [chris1111/Wireless-USB-Adapter at github](https://github.com/chris1111/Wireless-USB-Adapter)

[Installation Downloads](https://github.com/chris1111/Wireless-USB-Adapter/releases)
