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

## MacOS Error Fix: _Curl is configured to use SSL, but we have not been able to determine which SSL backend it is using. Please see PycURL documentation for how to specify the SSL backend manually._

This command will install pycurl on macOS system. This should fix the SSL Error

```bash
PYCURL_SSL_LIBRARY=openssl LDFLAGS="-L/usr/local/opt/openssl/lib" CPPFLAGS="-I/usr/local/opt/openssl/include" pip install --no-cache-dir pycurl
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
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->