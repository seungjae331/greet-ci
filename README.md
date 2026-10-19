# greet-ci

A small greeting program with GitHub Actions CI.

## Setup and run

Install Git and uv. From the repository root:

```sh
uv sync --locked
uv run --locked python greet.py Hee
uv run --locked python greet.py
```

Expected output, respectively:

```text
Hello, Hee!
Hello, world!
```

## Local checks

```sh
uv run --locked pytest -q greet.py
uv run --locked black --check greet.py
uv run --locked flake8 greet.py
uv run --locked mypy greet.py
uv build
```

After changing project dependencies, run `uv lock` and commit both
`pyproject.toml` and `uv.lock`.

## CI

Pull requests targeting main and pushes to main run four test jobs
(Ubuntu and Windows, each with Python 3.11 and 3.12), one quality job,
and one package build job. The build waits for all checks to pass and
uploads the distributions as the `greet-dist` artifact.
