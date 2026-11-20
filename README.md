# DSCI 522: Predicting tea category from its caffeine level
DSCI 522 Team 12: 
* Clarissa Nada Dahjan
* Julia Gorospe
* Kangju Sun
* Yingwen Liu

Our team will be working with [The Chinese Tea Dataset](https://chinatea.house/dataset/), seeing how we can predict the tea type/category based on its caffeine level.
## Summary

We used the Chinese Tea Dataset to predict tea categories. The model using only caffeine level had an accuracy of 44.4%. Adding body and oxidation level increased it to 88.0%. The full model reached 78.6% on the test set.

This shows that caffeine level alone is not enough to predict tea category well.

## How to Run

Install uv and Quarto first.

1. Clone the repository:

   `git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Predicting-tea-category-from-its-caffeine-level.git`

2. Open the project folder:

   `cd DSCI-522-Predicting-tea-category-from-its-caffeine-level`

3. Install the packages:

   `uv sync`

4. Run the analysis.

   On Mac or Linux:

   `QUARTO_PYTHON="$PWD/.venv/bin/python" quarto render analysis/analysis.qmd --to html --execute-dir "$PWD"`

   On Windows PowerShell:

   `$env:QUARTO_PYTHON = (Resolve-Path ".venv\Scripts\python.exe").Path`

   `quarto render analysis/analysis.qmd --to html --execute-dir (Get-Location).Path`

The output is saved in `analysis/analysis.html`.

## Dependencies

We use Python 3.14, uv, and Quarto. Python packages are listed in `pyproject.toml` and `uv.lock`.

## License

The code uses the MIT License. The report uses CC BY-NC-ND 4.0.

See [LICENSE.md](LICENSE.md).

## AI Use

We used ChatGPT to help with data analysis, explain the logic, review our workflow, and check our code. We checked the results ourselves.

Example prompts:

- "Explain the logic of this code."
- "Check if our analysis steps make sense."
- "Check the Python code for errors."

## Report

[HTML report](analysis/analysis.html)
