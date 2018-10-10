# Python

## Update All the pip Packages

````bash
pip list --outdated --format=freeze | grep -v '^\-e' | cut -d = -f 1  | xargs -n1 pip install -U
````

## Generate requirements.txt For a Project

Run this command at terminal at the root of the project:

````bash
pip freeze > requirements.txt
```