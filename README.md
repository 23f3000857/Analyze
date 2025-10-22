# Overview

This repository fixes the provided `execute.py`, adds a CSV export of the data, and introduces a GitHub Actions workflow that:

- Runs Ruff (Python linter) and prints its results in the CI logs.
- Executes `python execute.py > result.json`.
- Publishes `result.json` via GitHub Pages.

Key points:

- The bug referring to the misspelled "revenew" was fixed, and the data pipeline was completed and made robust for Python 3.11+ with pandas 2.3.
- `execute.py` prints a single JSON object to stdout. CI redirects it to `result.json`.
- `data.csv` is the CSV conversion of the given `data.xlsx` and should be committed to the repo.
- `result.json` is not committed; it is generated in CI and published to Pages.

# Setup

1. Create the following files and paths in your repository:
   - execute.py (from this project)
   - data.csv (converted from the provided data.xlsx)
   - .github/workflows/ci.yml
   - .gitignore (optional but recommended; includes result.json)

   You can copy file contents from index.html in this project. The index page shows each file with “Copy” and “Download” helpers.

2. Ensure that `data.xlsx` (original attachment) is present at the repository root so the conversion can be validated if needed. The script will also work with `data.csv` alone.

3. No extra config is needed for Ruff; the workflow uses the default rules.

# Usage

- Local run:
  - Ensure you have Python 3.11+.
  - Install dependencies:
    - pip install "pandas>=2.3,<2.4" openpyxl
  - Run:
    - python execute.py > result.json
  - Open result.json to see the summary including:
    - row_count
    - regions_count
    - top_n_products_by_revenue (top 3)
    - rolling_7d_revenue_by_region (last 7-day MA per region)

- CI:
  - Push to any branch.
  - The workflow:
    - Installs pandas 2.3, openpyxl, and ruff.
    - Runs Ruff and prints results.
    - Executes execute.py to produce result.json.
    - Publishes result.json to GitHub Pages at the environment URL shown in the job logs.

Notes:
- Do not commit result.json; it is generated in CI and published via Pages.
- execute.py supports reading from data.csv (preferred if present) or falls back to data.xlsx.

If Round 2, describe improvements made from previous version:
- N/A (this is Round 1).