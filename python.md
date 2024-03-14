# Python (programming language)

## Managing multiple versions of Python

[pyenv] lets you easily switch between multiple versions of Python. It does it
by (in most cases) compiling and installing the requested version of Python.
See [pyenv-installation] for installation instructions.

By default, _pyenv_ installs Python versions under `~/.pyenv`.
This can be changed by setting the `PYENV_ROOT` environment variable.

To install additional versions of Python, use:

```
$ PYENV_ROOT=... # Optional, where to install the requested Python version.
$                # It will be available in $PYENV_ROOT/versions/$VERSION$
$ pyenv install [--verbose] 3.11
```

Running:

```
$ PYENV_ROOT=... # Optional, needs to be provided if it was provided
$                # to the `pyenv install` command.
$ pyenv versions
```

gives the list of all installed versions.

See [pyenv-special-environment-variables] for some options to control the build
process.

> **FIXME**
>
> `eval "$(pyenv init -)"` in `~/.profile` should be only run after
> `PYENV_ROOT` is correctly set. Otherwise path to `shims` won't be
> set correctly.

[pyenv]: https://github.com/pyenv/pyenv
[pyenv-installation]: https://github.com/pyenv/pyenv#installation
[pyenv-special-environment-variables]: https://github.com/pyenv/pyenv/blob/master/plugins/python-build/README.md#special-environment-variables

## Virtual environment

[venv] - Creation of virtual environments.

Create, activate and deactivate virtual environment

```
$ path/to/python -m venv <PARENT DIRECTORY NAME (AKA ENVIRONMENT NAME)>
$ . <PARENT DIRECTORY NAME>/bin/activate
$ python stuff goes here ... (e.g. pip install)
$ exit # Close shell and exit the virtual environment
```

Configure `pip` to cache downloads in a different location

By default, `pip` will cache downloads in `~/.cache/pip`.
This can be changed with the following configuration file entry:

```
$ cat $VIRTUAL_ENV/pip.conf
[global]
cache-dir = path/to/pip-cache-dir
```

[venv]: https://docs.python.org/3/library/venv.html

## Poetry

[Poetry] is a tool for dependency management and packaging in Python. It allows
you to declare the libraries your project depends on and it will manage
(install/ update) them for you.

Poetry is best installed in and used from a Python virtual environment
(`(3.11)` is the name of the activated virtual environment):

```
(3.11) $ pip install poetry
```

To configure where Poetry stores its data, the following environment variables
can be used:

```
POETRY_CONFIG_DIR
POETRY_DATA_DIR
POETRY_CACHE_DIR
```

> **NOTE**
>
> These variables can be defined in the _virtualenv_'s `activate` script.
> And they can be unset in the `deactivate` script.

To select Python to use:

```
(3.11) $ poetry env use python3.11 # (or /full/path/to/python)
```

To install the defined dependencies for your project
(e.g. required Python packages):

```
(3.11) $ poetry install
```

[Poetry]: https://python-poetry.org/
