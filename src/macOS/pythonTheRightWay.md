title: How to Install Python on MacOS the Right Way and Use  Python Virtual Environment
description: How to Install Python on MacOS the Right Way and Use  Python Virtual Environment

<link rel="stylesheet" href="/assets/CSS/roundedCorners.css">

# Python on MacOS the Right Way

## How to Install Python on MacOS the Right Way

```bash
brew install pyenv
```

List available Python Version

```bash
pyenv install --list
```

Install Requeued Python Version (Exmaple version 3.8.2)

```bash
pyenv install 3.8.2
```

Set it as global

```bash
pyenv global 3.8.2
```

In order for it to work correctly, we need to add the following to our configuration file (.zshrc for me, possibly .bash_profile for you):

```bash
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.zshrc
```

Restart your shell and test:

```bash
python -V
pip -V
```

## How to Use with pipenv (Python Virtual Environment)

Install:

```bash
pip install --user pipenv
```

cd to desired folder and run:

```bash
pipenv shell
```

It will Create/Run Python Virtual Environment
