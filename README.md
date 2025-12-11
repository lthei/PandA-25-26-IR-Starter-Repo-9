# Part 9 - Starter

This part builds on your Part 8 solution. The key goal is to restructure
the code by moving functionality from `app.py` and `models.py` into a
new module, `file_utilities.py`. See the ToDos for details.

We also introduce a new setting, `:hl-mode`, which lets the user choose
between two different ways of highlighting the search results.

## Run the app

``` bash
python -m part9.app
```

## What to implement (ToDos)

Your ToDos are located in `part9/app.py` and `part9/models.py`.

0.  **Copy/redo** your implementation from Part 8.

    1.  Move `combine_results` to `SearchResult` and rename it to
        `combine_with`. Update all calls accordingly.
    2.  Move the printing of a single `SearchResult` to a method `print`
        inside the `SearchResult` class. Move `ansi_highlight` along
        with it.
    3.  Move `search_sonnet` to the `Sonnet` class and rename it to
        `search_for`. Move `find_spans` as well to make this work.

1.  You realize that `models.py` is starting to get too large. Move all
    file-related functionality to a new module, `file_utilities.py`. In
    this module, include the `Configuration` class and the following
    functions from `app.py`: `load_config`, `save_config`,
    `fetch_sonnets_from_api`, and `load_sonnets`.

    You will need to move other parts of your code to make this work.
    For example, it makes sense to put the constants `POETRYDB_URL` and
    `CACHE_FILENAME` in this module as well. Additionally, move
    `module_relative_path`, since the file operations rely on it. Some
    imports will also need to be moved to the new module.

2.  You are not satisfied with the way search results are currently
    shown. You want the user to be able to choose between:

    -   the existing **yellow background, black text**, and
    -   a new option: **bold light-green text**.

    You discover that the new highlighting mode can be implemented by
    replacing the control string `"\033[43m\033[30m"` in the static method
    `ansi_highlight` with another control string: `"\033[1;92m"`.

    Add a new configuration option that allows the user to switch
    between these two highlight modes using the command `:hl-mode` with
    either the value `DEFAULT` (yellow background variant) or `GREEN`
    (the new one). Save the current value to the `config.json` file so
    that users can permanently change their highlighting.

3. Now that you are starting to become an OOP expert, you also notice that
   it would be cleaner to move the `save_config` function from the newly
   created `file_utilities` module into the `Configuration` class. 
   Since you are already familiar with this kind of refactoring, you move
   the function into the class, rename it to `save`, and update the
   corresponding code in `app.py` to use the new method.
