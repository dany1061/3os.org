title: Home-Brew
description: Home Brew, examples and simple usage

# Home-Brew

## Installing Homebrew

run this at terminal:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Fixing Errors Ruby rubocop for Brew

```bash
brew vendor-install ruby
```

## BrewUP - Upgrades Brew & Casks Packages, macOS AppStore Apps

This script will perform the following:

- Cheeks for required packages, installs them if missing
- Runs brew doctor - display if there are `errors` in brew
- Updates brew packages
- Updates brew casks
- Updates macOS AppStore Apps
- Cleanups all unused packages

Installation or Update: Run at Terminal

```bash
curl -fsSL https://git.io/fxlRD -o /usr/local/bin/brewup
chmod +x /usr/local/bin/brewup
```

Run brewup:

```bash
brewup
```

done.

Source:
[brewup gist](https://gist.github.com/fire1ce/f9b6645b4c8cff5b7229e5011a168a47)

