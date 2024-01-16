# How to move from PIP to Poetry

## With PIP

### Add a dependency

```bash
pip install click==8.0.0
```

The above command add the package into the global environment. 

```shell
Requirement already satisfied: click in /home/linuxbrew/.linuxbrew/opt/python@3.11/lib/python3.11/site-packages (8.0.0)
```

Now if you want to share your project with others, you need to create a `requirements.txt` file.

```bash
pip freeze > requirements.txt
```

As you can see, the `requirements.txt` file contains all the dependencies of your project and all packages installed into your system.

You need to clean it up and remove all the packages that are not required for your project.

### Update a dependency

```bash
pip install --upgrade click
```

As you can see, the above command updates the package into the global environment, but it does not update the `requirements.txt` file.


### Use pylint

In order to use pylint, you need to install it into your global environment.

```bash
pip install pylint
```

But you can also add it as a dev dependency in a specific requirements file called `requirements-dev.txt`.

After that you can configure it with a `.pylintrc` file.

### Conclusion

As you can see, PIP is not a good tool to manage your project dependencies. It is not easy to share your project with others.

You should :

1) Create a `requirements.txt` file
2) Create a `requirements-dev.txt` file
3) Create a `.pylintrc` file
4) Manage the versions manually
5) Be careful with the global environment

## With Poetry

### Install Poetry

https://python-poetry.org/docs/#installation

### Initialize a new project

```bash
poetry init my_app
```

### Configure your project

Open the `pyproject.toml` file and check the following lines:

```toml
[tool.poetry]
name = "my-app"
version = "0.1.0"
description = ""
authors = ["Somebody <m.somebody@betclicgroup.com>"]
readme = "README.md"

[tool.poetry.dependencies]
python = "~3.11"


[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

As you can see, the `pyproject.toml` file contains all the information about your project.

### Add a dependency

```bash
poetry add click@~8
```

This command does the following things:

1) Add the package into the `pyproject.toml` file
2) Add the package into the virtual environment of your project
3) Create a `poetry.lock` file if it does not exist


```toml
[tool.poetry.dependencies]
python = "^3.11"
click = "~8"
```

### Update a dependency

```bash
poetry update click
```

### Add a dev dependency

```bash
poetry add pylint@~2 --group dev
```

```toml
[tool.poetry.group.dev.dependencies]
pylint = "~2"
```

### Configure pylint

1) Remove the `.pylintrc` file
2) Add the following lines into the `pyproject.toml` file

```toml
[tool.pylint.'MASTER']
ignore-path = "test/" # Ignore all tests

[tool.pylint.'MESSAGES CONTROL']
disable = [
    "C0114", # missing-module-docstring
    "C0115", # missing-class-docstring
    "C0116", # missing-function-docstring
    "W1203", # logging-fstring-interpolation
    "C0301", # line-too-long
    "R0903", # too-few-public-methods
    "R1710", # inconsistent-return-statements
    "W0718", # broad-exception-caught
    "I1101", # c-extension-no-member
]

[tool.pylint.'FORMAT']
max-line-length = 120 # Maximum number of characters on a single line.
max-args = 6

[tool.pylint.'design']
max-locals = 20
```

## Build and distribute your project

### Build your project

```bash
poetry build
```

1) Open the `dist` folder
2) Check the `my-app-0.1.0-py3-none-any.whl` file
3) Publish it on a private repository