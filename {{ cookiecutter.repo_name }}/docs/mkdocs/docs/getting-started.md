Getting started
===============

This is where you describe how to get set up on a clean install, including the
commands necessary to get the raw data (using the `sync_data_from_s3` command,
for example), and then how to make the cleaned, final data sets.

# Setting Up Your Environment

## 1. Install Conda
Start by installing [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html) if you haven’t already. Conda is a package and environment management tool that helps manage dependencies and packages across different projects.

## 2. Install Mamba
Mamba is a fast alternative to Conda for managing environments and packages. To install Mamba, run:
```bash
conda install mamba
```

## 3. Install Poetry
[Poetry](https://python-poetry.org/) is a Python dependency management tool that makes it easy to manage your projects' dependencies, virtual environments, and packaging. You can install it via Mamba:
```bash
mamba install poetry
```

## 4. Enable Tab Completion for Poetry
To enable tab completion for Poetry commands in Bash, Fish, or Zsh, use the following command (for Bash):
```bash
poetry completions bash >> ~/.bash_completion
```
If you're using **Zsh**, replace `bash` with `zsh`:
```bash
poetry completions zsh >> ~/.zshrc
```
For **Fish**, use:
```fish
poetry completions fish > ~/.config/fish/completions/poetry.fish
```

Now you’re all set up! 🎉 You can use Mamba and Poetry to manage your projects efficiently, with helpful tab completions for quick navigation.

--- 