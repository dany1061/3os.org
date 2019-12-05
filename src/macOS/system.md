title: macOS System Tweaks
description: macOS System tweaks and tips for better experience, productivity and workflow and more

<link rel="stylesheet" href="/assets/CSS/roundedCorners.css">

# macOS System Tweaks and Guides for Better Experience, Productivity and Workflow

## Import RSA Keys to macOS Keychain

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

## Disable StrictHostKeyChecking in SSH

To disable strict host checking on OS X for the current user,
create or edit ~/.ssh/ssh_config and add the following lines:

```bash
   StrictHostKeyChecking no
```

## Set macOS Hostname via CLI

```bash
sudo scutil --set HostName <NewHostNameHere>
```

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

## Force Language Change on iTerm Focus to English

* Install __KeyBoard Maestro__
* Create a group in __Groups__ section. I named my __Personal__
* Now create a macro with the name __Set iTerm Application Language.__
* Add another trigger -> __This application__ -> Select __iTerm__ -> Select __Active__ -> Repeating every __1 seconds__.
* Add __New Action__ -> Select __Set KeyBoard Layout__ -> Select the keyboard layout (i.e., language preference).

<div style="width:100%; margin:0 auto">
   <img src="/assets/images/macOS/itermToUS.jpg" alt="mac image">
</div>

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

## Running Multi Instances of an Application

Launch the Script Editor choose temporary folder

Copy the command to be executed to the Script Editor

```bash
do shell script "open -n <path to application>"
```

!!! example
    do shell script "open -n /Applications/'Visual Studio Code.app'"

File > Export

Use the following settings:

* Export As: __Your New Application Name__
* Where: __Applications__
* File Format: __Application__

^^Change The Icon of Your New Application:^^

In __Finder__ got to __Applications__ folder.
Right Click on the new __Your New Application__ application we just created and click __Get Info__.
Drug the original application icon (or any other) to the  in the left corner of the "get info" menu.

## Lunch Firefox Profile Manager as Application

Launch the Script Editor choose temporary folder

Copy the command to be executed to the Script Editor

```bash
do shell script "/Applications/Firefox.app/Contents/MacOS/firefox -ProfileManager &> /dev/null &"
```

File > Export

Use the following settings:

* Save As: __Firefox Profile Manager__
* Where: __Applications__
* File Format: __Application__

^^Change The Icon of Your New Firefox Profile Manager Application:^^

In __Finder__ got to __Applications__ folder.
Right Click on the new __Firefox Profile Manager__ application we just created and click __Get Info__.
Drug the original application to the icon in the left corner of the "get info" menu.

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

## List listening Ports and Programs and Users _(netstat like)_

```bash
sudo lsof -i -P | grep -i "listen"
```

## Flush DNS

```bash
sudo killall -HUP mDNSResponder;sudo killall mDNSResponderHelper;sudo dscacheutil -flushcache
```

## Google Drive File Sync Fix for macOS

quit Google Drive

```bash
cd ~/Library/Application\ Support/Google
mv DriveFS DriveFS.old
```

relaunch Google Drive

