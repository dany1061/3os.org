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

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->