# Tox: A meta-tool for Python

While it's not the only meta-tool in the Python world, Tox is a fairly widely
used meta-tool for Python. As a tool, what it does isn't exactly Python-specific,
though as it currently exists it would need further development to be a useful
meta-tool for other languages. (Notably, it would need support for creating
environments other than Python virtualenvs and for installing packages other
than through pip.) 

Tox is just one way to achieve this, but it can be used to great effect.

Below is an example `tox.ini` file that illustrates its
use as a meta-tool:

```ini
[tox]
minversion = 4.0
requires = 
    tox >= 4.0.0
    virtualenv >= 20.2
    # This allows multiple "environments" to share one virtualenv
    tox-ignore-env-name-mismatch==0.2.0.post2
env_list = 
    format-black
    format-ruff
    lint-ruff
    test-py310

[lint]  # Default configuration for all linting and formatting environments
deps = 
    black>=13.0
    ruff>=0.0.234
runner = ignore_env_name_mismatch
env_dir = {work_dir}/linting

[testenv:lint-{black,ruff}]
base = lint
labels = lint
commands =
    black: black {tty:--color} --check --diff {posargs:.}
    ruff: ruff --diff --respect-gitignore {posargs:.}

[testenv:format-{black-ruff}]
base = lint
labels = format
commands = 
    black: black {tty:--color} {posargs} .
    ruff: ruff --fix --respect-gitignore {posargs} .

[testenv:test-py310]
labels = test
extras = dev, test
commands = 
    pytest {tty:--color=yes} --cov {posargs:tests}
```

Let's examine the major pieces and why they're beneficial:

```ini
[tox]
minversion = 4.0
requires = 
    tox >= 4.0.0
    virtualenv >= 20.2
    # This allows multiple "environments" to share one virtualenv
    tox-ignore-env-name-mismatch==0.2.0.post2
```

This makes tox, at least to an extent, self-bootstrapping. You have to have a
fairly recent copy of tox (>=3.8.0, released 2019-03-27), but other than that,
you don't need to have a specific version, and you don't need to create a
virtual environment for your project before running tox. Rather, tox can be
installed system-wide, and if the system environment doesn't match the
requirements, tox will create a virtualenv that does match the requirements
and work from there. 

Of course, this isn't without consequences. Got Tox 3 on your machine but 5
projects that all require Tox 4? You're going to have 5 copies of tox 4.
But on the plus side, if you've got a project that requires tox 4 and one that
requires tox 3 and specifically not tox 4, there's no dance about managing
which version of tox is used for which project. It does that itself.

Importantly though, tox isn't automatically installed in the virtual environments
where linting, tests, etc. are run.

```ini
[lint]  # Default configuration for all linting and formatting environments
deps = 
    black==13.0
    ruff==0.0.234
runner = ignore_env_name_mismatch
env_dir = {work_dir}/linting

[testenv:lint-{black,ruff}]
base = lint
labels = lint
commands =
    black: black {tty:--color} --check --diff {posargs:.}
    ruff: ruff --diff --respect-gitignore {posargs:.}
```

The next three sections work together, but we'll start with just two of them.
These two sections describe how to run the various linting tools for this
project. In this case, we're using [black](https://github.com/psf/black) and
[ruff](https://github.com/charliermarsh/ruff).

The specific implementation here isn't important. What's important is:

1. Everyone, everywhere, is going to get the same versions of these tools.
2. There is one, and only one, place where that version is decided, and a change
in that one location updates it for all developers, the CI, and any other
system involved in linting this project.

```ini
[testenv:format-{black-ruff}]
base = lint
labels = format
commands = 
    black: black {tty:--color} {posargs} .
    ruff: ruff --fix --respect-gitignore {posargs} .
```

This section runs in the same virtual environment as the `lint` section.
More importantly though, it uses the same versions of `black` and `ruff` to
auto-format the code as it uses to lint the code. This is important because
rules and configuration can change from one version to another, and a project
should make these changes deliberately.

```ini
[testenv:test-py310]
labels = test
extras = dev, test
commands = 
    pytest {tty:--color=yes} --cov {posargs:tests}
```

Finally, the last paragraph simply runs unit tests, with coverage, in a
Python 3.10 environment, after installing the `dev` and `test` extras as well
as the package itself and any dependencies. 

## But Why?

The actual inner workings of the tox environment aren't that important here
other than as a guide. What's important is that this tox configuration:

1. Keeps your project's code separate from other code (such as linters) that
may have different dependencies
2. Handles installation and updating of tools automatically (every time you
run tox, it ensures that the virtual environment matches the configuration).
3. Is consistent and repeatable, across machines, operating systems, and
runtime environments. It works the same way in your CI as it does on your
desktop, and it works  the same way on your desktop as on your coworker's.
