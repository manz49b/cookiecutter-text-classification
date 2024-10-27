# CCD's & Monkey Patch
The `monkey_patch.py` file in `ccds` customizes the behavior of the `cookiecutter` package by overriding or redefining certain functions in it. It enable the user to have a custom configuration file (called `ccds.json` instead of the default `cookiecutter.json`) and to modify how `cookiecutter` handles user input for the project configuration. 

### Key Sections and Functions

1. **`_prompt_choice_and_subitems()`**
   - This function extends the default behavior of handling choices in `cookiecutter.json` files.
   - It prompts the user to make a selection from a list of options, then collects any additional sub-values related to that selection if the choice is associated with a dictionary or list.
   - The resulting choices and their values are stored in a dictionary structure.

2. **`prompt_for_config()`**
   - This function is a customized version of `cookiecutter.prompt.prompt_for_config`. It sets up a configuration dictionary (`cookiecutter_dict`) by reading values from the `context`.
   - It processes variables in two stages:
     - First pass: handles simple variables, lists, and choices.
     - Second pass: handles dictionary variables that may depend on values from the first pass.
   - This function also includes error handling to alert the user if a variable cannot be rendered due to undefined values.

3. **`generate_context_wrapper()`**
   - This wrapper function intercepts calls to `generate_context`, which normally loads the project context from `cookiecutter.json`.
   - It replaces the default configuration file with `ccds.json` and then processes the context as usual.
   - After loading the context, it renames the key `ccds` to `cookiecutter` so that it matches the expected structure downstream in `cookiecutter`.

### Summary
In essence, this script allows a template project to use a custom JSON file (`ccds.json`) instead of the standard `cookiecutter.json`, with additional customization in how choices and nested fields are handled in the configuration prompts. This setup would be useful in cases where a more complex, hierarchical project configuration is needed, or where some variables should be auto-populated without prompting the user.