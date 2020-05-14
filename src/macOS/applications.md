title: macOS Applications Tweaks
description: macOS Applications tweaks and tips for better experience, productivity and workflow and more

# macOS Applications Tweaks and Tips for Better Experience, Productivity and Workflow and more

## iTerm2 Tweaks and Tips

__Using Alt/Cmd + Right/Left Arrow in iTerm__

Go to iTerm Preferences → Profiles, select your profile, then the Keys tab. Click Load Preset... and choose Natural Text Editing.

__Remove the Right Arrow Before the Cursor Line__

you can turn it off by going in to Preferences > Profiles > (your profile) > Terminal, scroll down to "Shell Integration", and turn off "Show mark indicators".

## Add External Wireless USB Adapter Support macOS (Wifi)

If you have an external Wireless USB Adapter macOS won't let you use or control it.
Thanks to __chris1111__ for his git repository with supported software that's allows you to use external wireless usb parallel to the internal wifi card. Follow this link to for supported devices installation:

* [chris1111's Wireless-USB-Adapter Github Page](https://github.com/chris1111/Wireless-USB-Adapter){target=_blank}
* [Wireless-USB-Adapter Releases Download](https://github.com/chris1111/Wireless-USB-Adapter/releases){target=_blank}

## Disable FortiClinet Auto Start-up

Edit those files:

```bash
/Library/LaunchAgents/com.fortinet.forticlient.credential_store.plist
/Library/LaunchAgents/com.fortinet.forticlient.fct_launcher.plist
```

Change RunAtLoad to __false__ it should look like this

```bash
        <key>RunAtLoad</key>
        <false/>
```
