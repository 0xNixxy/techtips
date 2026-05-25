# Python Quickstart Guide

Python is one of the easiest scripting languages to learn, but also one of the
easiest to overcomplicate when it comes to setup. This quickstart is designed
for both first-time learners and experienced developers who just need a
fuss-free way to get Python set up to start coding.

This opinionated guide focuses on a mainstream Python workflow on Linux, which
includes tools, commands, and conventions widely recommended in 2026, while
briefly covering older approaches you can safely skip over.

## Useful Background Knowledge

1. Use **Python 3** for your new projects. Python 2 is obsolete and deprecated
   since 2020. The latest Python versions can be found on the [official Python
   website](https://devguide.python.org/versions/).

1. Linux is technically easier to setup Python as Python often comes
   pre-installed with Linux. For Ubuntu 24.04, use the following commands to
   setup Python3

   ```bash
   sudo apt update
   sudo apt install python3 python-is-python3
   ```

   > ℹ️ Note
   >
   > Download the installer from the [official Python
   > website](https://www.python.org/downloads/windows/) to install Python on
   > Windows.

1. Use `uv` tool to install and manage specific versions of Python.

1. Use `ruff` tool for linting and formatting of Python source code. Linters
   help you catch mistakes early in your source code and help build good coding
   habits automatically in developers.

## Set up specific Python versions with `uv`

1. [Optional prerequisites] Ensure that your system has the following tools
   installed to proceed with the subsequent steps.

   ```bash
   sudo apt install curl
   ```

1. Install latest version of `uv` using the [official standalone
   installer](https://docs.astral.sh/uv/getting-started/installation/).

   ```bash
   curl -LsSf --tlsv1.3 https://astral.sh/uv/install.sh | sh
   ```

   > 💡 Tip
   >
   > To upgrade `uv`, use the `uv self update` command.
   >
   > To uninstall `uv`, use the following commands
   >
   > ```bash
   > uv cache clean
   > rm -r "$(uv python dir)"
   > rm -r "$(uv tool dir)"
   > ```

1. Restart your shell to activate `uv` environment settings.

1. Use the following command to validate that `uv` has been properly installed.
   You should see the version number printed to terminal.

   ```bash
   uv self version
   ```

1. Install a specific version of Python.

   ```bash
   uv python install 3.11
   ```

   > 💡 Tip
   >
   > To upgrade a specific Python version to the latest patch release, use
   > `uv python upgrade 3.11`.

1. Check that Python was installed properly.

   ```bash
   uv python list
   ```

1. Set a project to use a specific version of Python.

   ```bash
   mkdir hello-world
   cd hello-world
   uv python pin 3.11
   ```

   > 💡 Tip
   >
   > To set a global default version of Python in your user account, use
   > `uv python pin --global 3.11`.

1. Check the version of Python executed by `uv` in the project.

   ```bash
   uv run python --version
   ```

## Run Python scripts with `uv`

Once you have set up the target Python version with `uv` above, you can run
Python scripts in the following ways

1. Run script without 3rd-party dependencies.

   ```bash
   uv run hello-world.py
   ```

   > ℹ️ Note
   >
   > Usage of modules from the Python standard libraries is supported in this
   > mode of running Python scripts.

1. Run script with 3rd-party dependencies (ideally within a project).

   1. Create a new Python project with `uv`.

      ```bash
      mkdir hello-world
      cd hello-world
      uv init
      ```

   1. Run the Python project.

      ```bash
      uv run main.py
      ```

> 💡 Tip
>
> For more information on working on projects with `uv`, read the [official
> documentation](https://docs.astral.sh/uv/guides/projects/).

## Lint your Python project with `ruff`

To use a linter to check your Python source code in a project, follow the steps
below

1. (One-time setup) Install latest version of `ruff` globally.

   ```bash
   uv tool install ruff@latest
   ```

1. Format code style for all Python source files in current directory.

   ```bash
   ruff format
   ```

1. Lint (check) all Python source files in current directory.

   ```bash
   ruff check
   ```

## Gradual deprecation of older Python tools

Python developers are rapidly consolidating around a new generation of tools,
such as `uv` and `ruff`, which are designed to replace the older fragmented
toolchain. However, many active Python projects have yet to migrate to the new
toolchains and will likely take a few years for the entire Python ecosystem to
complete migration.

New and experienced developers will need to recognise these older tools when
there is a need to integrate the new toolchain with older Python projects.
The following table summarises the list of old tools and the superseding new
tools.

| Old Tool | Purpose | Equivalent New Tool |
| -------- | ------- | ------------------- |
| `pyenv` | Version manager for Python | `uv python install` |
| `pip` | Install packages | `uv add` |
| `python -m venv` | Create virtual environments | `uv` |
| `pipenv` | Package + env management | `uv` |
| `poetry` | Dependency management | `uv` |
| `requirements.txt` | List dependencies used by `pip` | `uv` uses `pyproject.toml` |
| `flake8` / `pylint` | Linting | `ruff check` |
| `black` | Formatting | `ruff format` |
| `virtualenv` | Older `venv` tool | Obsolete since Python 3.3 |
| `conda` | Python + non-Python packages | Only needed for scientific stacks |

---

← [Back to Main Page](../index.md)
