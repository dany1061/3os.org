title: Development - Python
description: Development - Python how to, guides, examples, and simple usage

# Python

## Python Virtual

Make sure you’ve got Python & pip¶

```bash
python --version
pip --version
```

Installing Pipenv¶ & Virtualenv

```bash
pip install --user pipenv
pip install virtualenv
```

Create Virtualenv for Your Project

```bash
cd project_folder
virtualenv 
```

Delete Virtualenv for Your Project

```bash
cd project_folder
rm -rf venv
```


Activate Virtualenv at Project's Folder

```bash
pipenv shell
```

Installing Requirements

```python
pip install -r requirements.txt
```

## Pip Update

### Update Pip Itself

```bash
pip install --upgrade pip
```

### Update All Packages Installed With Pip

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
