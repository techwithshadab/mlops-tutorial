# Insurance Cross Sell Prediction 🏠🏥
[![GitHub](https://img.shields.io/badge/GitHub-code-blue?style=flat&logo=github&logoColor=white&color=red)](https://github.com/techwithshadab/mlops-tutorial)

Welcome to the Insurance Cross-Selling Prediction project! The goal of this project is to predict which customers are most likely to purchase additional insurance products using a machine learning model. This README provides comprehensive instructions for setting up the environment, running the project, and using the integrated code quality and CI/CD tools.

## Getting Started

### Prerequisites

-   Python 3.10+
-   Docker
-   Make

### Initial Setup

1.  **Clone the Repository**

    ```bash
    git clone https://github.com/techwithshadab/mlops-tutorial
    cd mlops-tutorial
    ```

2.  **Set Up the Environment**

    This command creates a Python virtual environment, upgrades `pip`, and installs all required packages from `requirements.txt`.

    ```bash
    make setup
    ```

## Code Quality and Formatting

This project uses a suite of tools to ensure high code quality and consistent formatting.

-   **`black`**: An uncompromising code formatter.
-   **`isort`**: A tool to sort Python imports automatically.
-   **`flake8`**: A linter to check for PEP8 style guide violations.

Configurations for these tools are in the `.flake8` and `pyproject.toml` files.

### Pre-commit Hooks

The repository is configured to use `pre-commit` to automate code quality checks before each `git commit`.

1.  **Install the Git Hooks:**

    After setting up the environment with `make setup`, run the following command once to install the hooks into your local `.git` directory.

    ```bash
    pre-commit install
    ```

2.  **Usage:**

    Once installed, the hooks will run automatically each time you attempt to make a commit. If a hook fails, simply `git add` the modified files and attempt your commit again.

3.  **Run Manually:**

    You can manually run all pre-commit hooks on all files at any time:

    ```bash
    pre-commit run --all-files
    ```

## CI/CD with GitHub Actions

This project includes a CI/CD pipeline using GitHub Actions, defined in `.github/workflows/ci-cd.yml`.

### Continuous Integration (CI)

The CI pipeline runs on every push and pull request to the `main` branch. It performs the following checks:
-   Installs dependencies.
-   Runs `pre-commit` hooks for linting and formatting.
-   Executes the `pytest` test suite.

### Continuous Deployment (CD)

The CD pipeline is triggered on every push to the `main` branch, provided the CI pipeline succeeds. It performs the following steps:
1.  Logs in to Docker Hub.
2.  Builds the Docker image.
3.  Pushes the image to Docker Hub with the `latest` and commit SHA tags.

### GitHub Secrets Configuration

To enable the CD pipeline, you must configure the following secrets in your GitHub repository settings under **Settings > Secrets and variables > Actions**:

-   `DOCKER_USERNAME`: Your Docker Hub username.
-   `DOCKER_PASSWORD`: Your Docker Hub password or an access token.

## Data and Model Versioning with DVC

This project uses [DVC (Data Version Control)](https://dvc.org/) to manage large files like datasets and models.

-   **Retrieve Data:** `dvc pull`
-   **Version New Data:** `dvc add <file>`, `git add <file.dvc>`, `dvc push`

## Model Monitoring with Evidently AI

The `notebook/monitor.ipynb` notebook is used to monitor the model for data drift, data quality, and target drift using Evidently AI.

-   It compares the training data (`reference`) with recent test (`current`) and production data.
-   It generates interactive HTML reports (e.g., `test_drift.html`) that visualize any detected drift or data quality issues.

To run the monitoring, execute the cells in the `notebook/monitor.ipynb` notebook.

## Available Makefile Commands

-   `make setup`: Sets up the virtual environment and installs dependencies.
-   `make run`: Runs the main application (`main.py`) to train the model.
-   `make test`: Executes the test suite using `pytest`.
-   `make mlflow`: Starts the MLflow tracking UI.
-   `make clean`: Removes temporary files and caches.
-   `make remove`: Deletes the virtual
