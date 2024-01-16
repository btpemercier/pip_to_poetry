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