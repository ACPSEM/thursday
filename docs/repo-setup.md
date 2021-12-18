# How this repository is set up

This repo uses the following generic tools (non-specific ):

- [Poetry](https://python-poetry.org/)
  - gracefully manages Python virtual environments and dependencies;
  - conveniently enables a project to set fixed dependencies with specific package versions, so that the project builds consistently; and
  - is handily integrated with PyPi for easier publishing of releases.

- [`pre-commit`](https://pre-commit.com/)
  - a security and standardisation tool that enables automatic running of scripts (specifically [Git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)) to identify, and sometimes auto-fix, issues before they are committed to the project's Git history.
  - Examples of issues that can be identified include:
    - non-empty Jupyter notebook outputs that may contain patient-identifying information;
    - incorrect syntax; and
    - non-standard code formatting that makes code review painful.

- [`pylint`](https://pylint.org/)
  - A commonly used python code [linter](https://en.wikipedia.org/wiki/Lint_(software)).
  - Ensures code matches a particular style guide (e.g. [PEP-8](https://www.python.org/dev/peps/pep-0008/))
    - But for this repo, `black` primarily serves this purpose (see below).
  - Detects certain errors. E.g., are the requisite modules imported?
  - can be run in `pre-commit`, but isn't in this repo due to time-cost of pylint.

- [`pytest`](https://docs.pytest.org/en/6.2.x/)
  - A python auto-testing framework with certain advantages over the native [Unittest](https://docs.python.org/3/library/unittest.html).

- [`black`](https://github.com/psf/black)
  - An uncompromising auto-formatter for python
  - runs in `pre-commit`.

- [`isort`](https://github.com/PyCQA/isort)
  - handy sorting of python imports.
  - runs in `pre-commit`.

- [`nbstripout`](https://github.com/kynan/nbstripout)
  - helps ensure no Jupyter notebook outputs that make contain patient data make it into repo
  - runs in `pre-commit`.