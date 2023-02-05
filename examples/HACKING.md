This is an example HACKING file for a Python project called `toot`

# Hacking `toot`

This file describes what's necessary to begin development on `toot`. Be sure to
reference the [CONTRIBUTING](CONTRIBUTING.md) file before creating a pull
request.

## Dependencies

In order to work on `toot`, you will need the following on your computer:

* [Python 3.8](https://www.python.org/downloads/release/python-3810/).
`toot` supports all versions from 3.8, so ensure that your code will run in all
versions >= 3.8.
* [Tox 3.8](https://tox.wiki/en/latest/installation.html) or newer. `toot` 
requires 4.3, but is configured to allow tox >= 3.8 to bootstrap a newer 
version if needed.
* [Pyright 1.1.291](https://github.com/microsoft/pyright). This exact version
is what's used on our CI, so using a different version *could* have pyright on
your machine conflict with our CI.

## Setup

After cloning the toot repository, enter the directory and run `tox`. This will
install all necessary dependencies and run the linters and tests. If a failure
occurs on a cleanly cloned repository pointing to `main`, this is likely either
a bug or due to incomplete requirements specified above. Please file an issue.

If tox can't find Python 3.8, please ensure it's in your path and that 
you have 3.8 specifically, as the default tests run in 3.8

### Testing against other Python versions

`toot` has tox configurations to test against all supported versions of Python.
If you have all the necessary versions of Python, you can run `tox run -m tests`
to run the tests in all environments.

### Setting up a development environment

You can create a virtual environment for `toot` by running:

    tox devenv -e test-py38

Substitute `py38` as appropriate for setting up a development environment with
a different version of Python.

## Tools

`tox` is our main interface for handling code quality tools. A normal
development session will look approximately as follows:

1. Write necessary code, tests, documentation, etc.
2. Run `tox run -m format` to run all auto-formatters
3. Run `tox run -m lint` to run all linters
4. Run `tox run -e test-py38` to run tests in Python 3.8.
5. Fix any issues found in steps 2-4 and repeat
6. Commit and file a pull request following our [contributing 
guidelines](CONTRIBUTING.md)

Note: If you run `tox` without any parameters, it will run the formatters,
the linters, and the tests in order. If you need to test on multiple Python
versions, you can either specify a different python version or run
`tox run -m tests` to run it under all Python versions.

Finally, if you want to run exactly what gets run in CI, you can run:

    tox run -m ci
