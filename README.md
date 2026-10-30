# MLOps Lecture

Hands-on mini-labs covering the main building blocks of an MLOps workflow: experiment tracking, data versioning, pipelines, monitoring and CI/CD.

## Table of contents

- [Repository structure](#repository-structure)
- [Set-up](#set-up)
- [Quickstarts](#quickstarts)
  - [MLflow: experiment tracking](#mlflow--experiment-tracking)
  - [DVC: data versioning](#dvc--data-versioning)
  - [Kedro: reproducible pipelines](#kedro--reproducible-pipelines)
  - [Evidently: data & model monitoring](#evidently--data--model-monitoring)
  - [CI/CD with GitHub Actions](#cicd-with-github-actions)
- [Useful commands](#useful-commands)

## Repository structure

```text
.
├── .dvc/                      # DVC configuration
├── .github/workflow/          # GitHub Actions workflow (CI/CD), to be renamed in your fork
├── cicd-demo/                 # Demo project used for the CI/CD lab
├── dvc_quickstart.ipynb       # Data versioning with DVC
├── evidently_quickstart.ipynb # Monitoring with Evidently
├── kedro_quickstart.ipynb     # Pipelines with Kedro
├── mlflow_quickstart.ipynb    # Experiment tracking with MLflow
├── pyproject.toml             # Project dependencies (managed by uv)
└── uv.lock                    # Locked dependency versions
```

## Set-up

### Introducing uv as new standard package-manager

[uv](https://docs.astral.sh/uv/) is a fast Python package and project manager that replaces `pip`, `venv` and `pip-tools` in a single tool.

```bash
# Install uv package manager
pip install uv

# Install Python 3.11
uv python install 3.11

# Pin Python version to 3.11 for this project
uv python pin 3.11

# Sync dependencies from pyproject.toml
uv sync
```

## Quickstarts

Each quickstart is a self-contained notebook. Run `uv sync` first, then open the notebook of your choice.

### MLflow: experiment tracking

**Notebook:** [`mlflow_quickstart.ipynb`](mlflow_quickstart.ipynb)

Track your machine learning experiments: log parameters, metrics and artifacts for each run, compare runs side by side and keep a registry of your models. Launch the tracking UI with:

```bash
uv run mlflow ui
```

### DVC: data versioning

**Notebook:** [`dvc_quickstart.ipynb`](dvc_quickstart.ipynb)

Version large datasets and models alongside your code without storing them in Git. DVC keeps lightweight pointer files in the repository and the actual data in a local or remote storage. Configuration lives in the [`.dvc/`](.dvc) folder.

```bash
# Track a file or folder with DVC
uv run dvc add data/

# Push the data to the configured remote
uv run dvc push
```

### Kedro: reproducible pipelines

**Notebook:** [`kedro_quickstart.ipynb`](kedro_quickstart.ipynb)

Structure your data science code into modular, testable pipelines made of nodes, with a data catalog to manage inputs and outputs. It is a good starting point for moving from exploratory notebooks to production-ready code.

### Evidently: data & model monitoring

**Notebook:** [`evidently_quickstart.ipynb`](evidently_quickstart.ipynb)

Monitor your models once they are deployed: detect data drift, check data quality and generate visual reports on model performance over time.

### CI/CD with GitHub Actions

**Demo project:** [`cicd-demo/`](cicd-demo) · **Workflow:** [`.github/workflow/ci.yml`](.github/workflow/ci.yml)

Automate testing and deployment on every push and pull request. The workflow sets up Python 3.11, installs the dependencies, runs the tests with `pytest` and runs a (simulated) deployment on `main`.

You can have a look at the file in [`cicd-demo/`](cicd-demo) as an example of unit tests: it contains a simple function and its test, which `pytest` detects and runs automatically in the workflow.

> **Your turn:** the workflow folder is deliberately named `.github/workflow` (without the **s**), so it is **not** picked up by GitHub as is. Fork this repository, then rename the folder yourself so that the workflow appears and runs in the **Actions** tab of your fork:
>
> ```bash
> git mv .github/workflow .github/workflows
> git commit -m "fix: rename workflow folder to workflows"
> git push
> ```
>
> Remember to enable Actions from the **Actions** tab of your fork if GitHub asks you to.

## Useful commands

```bash
# Run the main script
uv run main.py

# Convert requirements.txt to uv like pyproject.toml
uv add -r requirements.txt

# Add a new dependency
uv add <package>

# Run a command inside the project environment
uv run <command>
```