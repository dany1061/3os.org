title: Development - Python
description: Development - Python how to, guides, examples, and simple usage

# Python

## Update All the pip Packages

```bash
pip list --outdated --format=freeze | grep -v '^\-e' | cut -d = -f 1  | xargs -n1 pip install -U
```

## Generate requirements.txt For a Project

Run this command at terminal at the root of the project:

```bash
pip freeze > requirements.txt
```

## Simple HTTP Python Web Server

create bash script with any name:

```bash
touch simpleHTTPServer.sh
chmod +x simpleHTTPServer.sh
```

Edit simpleHTTPServer.sh file:

```bash
nano simpleHTTPServer.sh
```

Add this to the file, choose any available port.

```bash
open http://localhost:8000
python -m SimpleHTTPServer 8000
```

run the file:

```bash
./simpleHTTPServer.sh
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->