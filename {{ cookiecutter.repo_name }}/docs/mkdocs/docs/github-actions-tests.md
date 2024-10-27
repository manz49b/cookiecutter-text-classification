# Github Actions Repository Tests
This `test.yml` file in `.github/workflows` is a GitHub Actions workflow configuration that defines automated actions for testing the codebase. 

### Workflow Name and Triggers
- **`name: tests`**: Names the workflow as "tests" to be displayed in the GitHub Actions tab.
- **`on` triggers**:
  - **`push` and `pull_request`**: This workflow runs when code is pushed to or a pull request is opened against the `master` branch, except for files in `docs` and `README.md` (to avoid unnecessary testing on documentation-only changes).
  - **`schedule`**: Runs weekly on Sunday at midnight (UTC).
  - **`workflow_dispatch`**: Allows manual triggering of the workflow.

### Jobs
#### 1. `code-quality` Job
This job checks the code quality:
- **`runs-on: ubuntu-latest`**: Uses Ubuntu for the job environment.
- **Steps**:
  - **`actions/checkout@v4`**: Checks out the repository.
  - **`Set up Python`**: Sets up Python 3.10 and uses caching for dependencies.
  - **`Install dependencies`**: Upgrades `pip` and installs project requirements.
  - **`Lint`**: Runs `make lint` to check for code style and quality issues.

#### 2. `tests` Job
This job runs the project tests across multiple operating systems and Python versions.
- **`needs: code-quality`**: This job only runs if `code-quality` is successful.
- **`strategy.matrix`**: Tests on different operating systems (Ubuntu, macOS, Windows) and Python versions (3.8 to 3.12).
- **Steps**:
  - **`actions/checkout@v4`**: Checks out the repository.
  - **`Set up Python`**: Configures each matrix's Python version with caching.
  - **`Set up Miniconda`**: Installs Miniconda and prepares for conda-based environments.
  - **`Cache conda packages`**: Caches packages to speed up repeated runs.
  - **`Setup for Windows`**: Installs GNU `make` on Windows and ensures the correct shell is set.
  - **`Install dependencies`**: Installs project dependencies.
  - **`Check dependencies`**: Verifies that key tools (`make`, `bash`, `conda`, etc.) are properly installed.
  - **`Run tests`**: Executes `make test` to run the test suite across all specified environments.

This workflow provides a comprehensive testing setup, checking both code quality and compatibility across OS and Python version combinations.