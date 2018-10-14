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