# How this repository is set up

### Tools used

This repo uses the following generic tools:

- [Poetry](https://python-poetry.org/)
  - Gracefully manages Python virtual environments and dependencies;
  - conveniently enables a project to set fixed dependencies with specific package versions, so that the project builds consistently; and
  - is handily integrated with PyPi for easier publishing of releases.

- [`pre-commit`](https://pre-commit.com/)
  - A security and standardisation tool that enables automatic running of scripts (specifically [Git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)) to identify, and sometimes auto-fix, issues before they are committed to the project's Git history.
  - Examples of issues that can be identified include:
    - non-empty Jupyter notebook outputs that may contain patient-identifying information;
    - incorrect syntax; and
    - non-standard code formatting that makes code review painful.

- [`pylint`](https://pylint.org/)
  - A commonly used python code [linter](https://en.wikipedia.org/wiki/Lint_(software)).
  - Ensures code matches a particular style guide (e.g. [PEP-8](https://www.python.org/dev/peps/pep-0008/))
    - But for this repo, `black` primarily serves this purpose (see below).
  - Detects certain errors. E.g., are the requisite modules imported?
  - Can be run in `pre-commit`, but isn't in this repo due to time-cost of pylint.

- [`pytest`](https://docs.pytest.org/en/6.2.x/)
  - A python auto-testing framework with certain advantages over the native [Unittest](https://docs.python.org/3/library/unittest.html).

- [`black`](https://github.com/psf/black)
  - An uncompromising auto-formatter for python
  - Runs in `pre-commit`.

- [`codespell`](https://github.com/codespell-project/codespell)
  - Fixes common misspellings in text files; designed primarily for source code.
  - Runs in `pre-commit`.

- [`isort`](https://github.com/PyCQA/isort)
  - Handy sorting of python imports.
  - Runs in `pre-commit`.

- [`nbstripout`](https://github.com/kynan/nbstripout)
  - Helps ensure no Jupyter notebook outputs that make contain patient data make it into repo
  - Runs in `pre-commit`.

### Record of repository setup tasks

Assumptions:
- The `thursday` Repository has already been created in Github and cloned to the local machine
- All above tools have been correctly installed on the local machine

Tasks:

1. Initialise Poetry by running `poetry init` within the local repo directory

   - Type "no" in all prompts to obtain barebones Poetry environment

   *This generates the `pyproject.toml` file, which is used to store build system dependencies for Python projects.*

2. Run a poetry installation for the first time by running `poetry install`

   *You can find a well-written explanation of project setup using Poetry and, especially, the function of `poetry install` [here](https://python-poetry.org/docs/basic-usage/#installing-without-poetrylock). In this particular case, since this script hasn't been run before and we haven't yuet specified any dependencies, running `poetry install` simply creates `poetry.lock`. This initial version of `poetry.lock` (view it [here](https://github.com/ACPSEM/thursday/blob/e427a79b4674d7e69894db84770c68cd3473b8c5/poetry.lock)) contains nothing particularly interesting except for the `content-hash`. Whenever you make changes to the project's Poetry environment (e.g. adding a dependency by runing `poetry add <new-dependency>`), `content-hash` updates to a new hash. Changes to `poetry.lock` can be tracked using this hash and controlled where necessary.*