# Insurance Cross Sell Predict### 3. Data Preparation

    Pull the data from DVC. If this command fails, the necessary data is already included in the `data/` directory.

    ```bash
    dvc pull
    ```

## Data and Model Versioning with DVC

This project uses [DVC (Data Version Control)](https://dvc.org/) to manage large files, such as datasets and models, that are not stored in Git. The configuration for DVC is in the `.dvc/` directory, and it helps ensure that experiments are reproducible.

### Retrieving Data

To retrieve the versioned data and models, run the following command after setting up the environment. This will download the `data/` directory tracked by DVC.

```bash
dvc pull
```

### Versioning New Data

If you modify the dataset or retrain the model, you can update the versioned files using the following steps:

1.  **Add the files to DVC tracking:**
    This command tells DVC to start tracking a file or directory.

    ```bash
    dvc add data/
    ```

2.  **Commit the changes to Git:**
    The `dvc add` command creates a new `.dvc` file (e.g., `data.dvc`). This small file acts as a pointer to the actual data and should be committed to Git.

    ```bash
    git add data.dvc
    git commit -m "Updated dataset"
    ```

3.  **Push the data to DVC remote storage:**
    This command uploads the actual data file (tracked by DVC) to the configured remote storage.

    ```bash
    dvc push
    ```

[![GitHub](https://img.shields.io/badge/GitHub-code-blue?style=flat&logo=github&logoColor=white&color=red)](https://github.com/techwithshadab/mlops-tutorial)

Welcome to the Insurance Cross-Selling Prediction project! The goal of this project is to predict which customers are most likely to purchase additional insurance products using a machine learning model. This README provides comprehensive instructions for setting up the environment, running the project, and using the integrated code quality tools.

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

3.  **Data Preparation**

    Pull the data from DVC. If this command fails, the necessary data is already included in the `data/` directory.

    ```bash
    dvc pull
    ```

## Code Quality and Formatting

This project uses a suite of tools to ensure high code quality and consistent formatting.

-   **`black`**: An uncompromising code formatter.
-   **`isort`**: A tool to sort Python imports automatically.
-   **`flake8`**: A linter to check for PEP8 style guide violations.

Configurations for these tools are in the `.flake8` and `pyproject.toml` files.

### Pre-commit Hooks

The repository is configured to use `pre-commit` to automate code quality checks before each `git commit`. The hooks will format your code, lint it, run tests, and check if the Docker image builds successfully.

1.  **Install the Git Hooks:**

    After setting up the environment with `make setup`, run the following command once to install the hooks into your local `.git` directory.

    ```bash
    pre-commit install
    ```

2.  **Usage:**

    Once installed, the hooks will run automatically each time you attempt to make a commit. If a hook fails (e.g., a file needs reformatting), it may modify files. Simply `git add` the modified files and attempt your commit again.

3.  **Run Manually:**

    You can manually run all pre-commit hooks on all files at any time:

    ```bash
    pre-commit run --all-files
    ```

## Available Makefile Commands

The `Makefile` provides convenient shortcuts for common tasks:

-   `make setup`: Sets up the virtual environment and installs dependencies.
-   `make run`: Runs the main application (`main.py`) to train the model.
-   `make test`: Executes the test suite using `pytest`.
-   `make mlflow`: Starts the MLflow tracking UI.
-   `make clean`: Removes temporary files and caches (`__pycache__`, `.pytest_cache`).
-   `make remove`: Deletes the virtual environment and `mlruns` directory.

## Running the Application

### FastAPI

To start the FastAPI application for real-time predictions:

```bash
uvicorn app:app --reload
```

### Docker

To build and run the application as a Docker container:

1.  **Build the image:**

    ```bash
    docker build -t mlops-tutorial .
    ```

2.  **Run the container:**

    ```bash
    docker run -p 80:80 mlops-tutorial
    ```
Once your Docker image is built, you can push it to a container registry like Docker Hub for deployment.

## Model Monitoring

To monitor the model for data drift and performance degradation, run the `monitor.ipynb` notebook, which integrates Evidently AI for model analysis.
