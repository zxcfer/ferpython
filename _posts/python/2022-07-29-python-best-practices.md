---
layout: post
title:  "My Python Best Practices"
tags: ["python"]
---

# Python Development Guidelines

## 1. Code Structure and Files

We can use [Sample project]() in stash to get the basic structure for our Python projects.

Basic project structure:

* `docs/` directory is intented for keeping documentation configuration and reStrucured files. 
* `module_name/` dicrectory contains the source code of the module.
* `tests/` directory contains the unit tests
* `README.md` is intented to document the basic documentation for the project.
* `requirements.txt`
* `setup.py`

In the case you have to deploy in a kubernetes server, we also have to add following file:

```
Dockerfile
values.yml
```

## 2. Style Guidelines

**"Code is more often read than written."**

The PEP8 holds the community-generated style guide for Python. PEP stands for Python Enhancement Proposals. This is to make sure all Python code looks and feels the same. [PEP8](https://www.python.org/dev/peps/pep-0008/) is extensive, but here I present the most important and more frequently ommited guidelines:

- Use proper naming conventions for variables, functions, methods, and more.
    - Variables, functions, methods, packages, modules: this_is_a_variable
    - Classes and exceptions: CapWords
    - Constants: CAPS_WITH_UNDERSCORES
- Protected methods and internal functions: `_single_leading_underscore` Private methods: `__double_leading_underscore`
- Use naming conventions for identifiers this makes it easier to understand the code.
- Use comments, and whitespaces around operators and assignments.
- The maximum line length is 79 characters according to PEP8. However, in specific cases we can skip this rule, for example long queries we are not editting in the python file itself, but in SQL tool.

## 3. Check Coding Style

We will use flake8 to validate our coding style and structure. It allos multiple integrations: command line, PyCharm and other Python editors. For command line we can install:

```bash
pip install flake8
```

As PEP8 is very strict, you can skip some rules and provide specific configuration for Flake8 in file `.flake8`:

```ini
[flake8]
ignore = E226,E302,W291,E225,W293,E203,W391,F541,E201,E202
max-line-length = 200
exclude = tests/*
max-complexity = 10
```

Place `.flake8` file in the user directory and be sure to have the minimum of warnings when executing flake:

```bash
cd project_folder
flake8 module_name
```

## 4. Write tests and check test coverage

Testing code is important to keep.

## 5. Documentation

**"Code tells you how; Comments tell you why."**

Documenting your Python code is all centered on docstrings. These are built-in strings that, when configured correctly, can help us with project’s documentation.

Docstring conventions are described within PEP 257. Their purpose is to provide your users with a brief overview of the object. They should be kept concise enough to be easy to maintain but still be elaborate enough for new users to understand their purpose and how to use the documented object.

```py
class MyClass:
    """
    This is the documentation for this ``MyClass``.

    .. code-block:: py

        my_class = MyClass(0)

    """

    def __init__(self, pa):
        """
        documentation for the constructor

        :param pa: The first parameter.

        """
        self.pa = pa

    def get_value(self, mul):
        """
        returns the parameter multiplied by a value

        :param mul: a float
        :returns: result

        """
        return self.pa * mul
```

* For automatic documenting we will use sphinx. For installing just:

```bash
pip install sphinx
```

* Then we can generate the HTML for the project with:

```bash
cd docs
sphinx-apidoc -o . ../module_name
make html
```

* And finally you can show documentation in any web server, for example:

```bash
cd  _build/html
python -m http.server
```

> When creating documentation for existing project, just copy `docs` folder from **template project** to our **existing project**. Then follow the same steps, we just have to add or modify source folders according existing project.


## 6. Use Virtual Environments

You should create a virtual environment for each project you create.

This will avoid any library clashes, since different projects may need different versions of a certain library.

## 7. Write Object-Oriented Code

Python is also a object-oriented language. We should try to use the object-oriented paradigm even for simple features. It is very common that small scripts turn into bigger projects.

This has the advantages of data hiding and modularity. It allows reusability and modularity.

## 8. Version control

An important file is `.gitignore`. Avoiding noise to projects is very good practice, it avoids confusion.
Recomended file is:

```bash
.env
.idea
.project
.pydevproject
__pycache__/
.settings/
*.swp
.Python
build/
develop-eggs/
dist/
eggs/
.eggs/
pip-wheel-metadata/
.pytest_cache/
```

## 9. Deploy and publish

On the other hand, if we additionally we need to publish a web application and deploy on a k8s, we use the same file, but instead of publish in PyPi we deploy to Helm:

```hcl
  deployWith('helm') {
    adminTier
    helmRepository 'vmn-prod'
    chart {
      name 'vmn-generic'
      version '0.2.72'
    }
    values 'values.yaml'
  }
```

## 10. Logging and Exceptions

Avoid **generic logging**

```py
try:
    something()
except Exception:
    logger.error("something bad happened")
```

or **skip logging**

```py
try:
    something()
except Exception:
    pass
```

When writing logs we should provide the clear information and use custom exceptions if possible. If we are not sure about the cause of the error printing the complete trace is very helpful using `exc_info` parameter.

```py
try:
    spped = distance / time
    something()
except ZeroDivisionError:
     logger.error("Time could not be zero.")
except Exception:
    logger.error("Unknown error", exc_info=True)
```

```py
try:
    connect_oracle_db()
except ZeroDivisionError:
     logger.error("Time could not be zero.")
     dba_notify(message)
```

### 11. Imports

Avoid importing everything from a package (`from mylib import *`), this pollutes the global namespace and can cause clashes.
