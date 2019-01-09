title: Development - Python
description: Development - Python how to, guides, examples, and simple usage

# Git

## Use Gist as Repository

It's probably easiest if you just start by cloning the gist, so that `origin` (a "remote" that refers to the original repository) is set up for you. Then you can just do `git push origin master`. For example:

```bash
git clone git@gist.github.com:869085.git mygist
cd mygist
# Make your changes...
git add .
git commit -m "Better comments"
git push origin master
```

However, if you don't want to redo your changes, you can do:

```bash
cd mygist
git remote add origin git@gist.github.com:869085.git
git fetch origin
# Push your changes, also setting the upstream for master:
git push -u origin master
```

Strictly speaking, the `git fetch origin` and `-u` argument to `git push origin master` are optional, but they will helpfully associate the upstream branch `master` in `origin` with your local branch `master`.

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->
