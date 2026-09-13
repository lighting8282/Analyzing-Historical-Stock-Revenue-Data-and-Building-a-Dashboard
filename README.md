# Historical Stock & Revenue Dashboard

Extracts historical share price and quarterly revenue data for **Tesla (TSLA)** and
**GameStop (GME)**, then visualizes the two series together to compare market price
against underlying business performance.

Built as the capstone for IBM's *Python Project for Data Science* (PY0220EN), then
cleaned up and extended.

## What it does

1. **API extraction** — pulls complete daily price histories via the `yfinance`
   library (`Ticker.history(period="max")`).
2. **Web scraping** — retrieves quarterly revenue tables with `requests` and parses
   them using `BeautifulSoup`, walking `<tbody>` / `<tr>` / `<td>` structure to
   build records.
3. **Cleaning** — strips currency symbols and thousands separators, drops null and
   empty rows, and coerces the result into typed pandas DataFrames.
4. **Visualization** — renders a two-panel, shared-x-axis Plotly figure per ticker:
   share price on top, revenue below, truncated to a common date range so the
   series line up.

## Stack

`Python 3.12` · `pandas` · `yfinance` · `requests` · `BeautifulSoup4` · `Plotly` · `Jupyter`

## Running it

```bash
pip install yfinance bs4 pandas plotly nbformat
jupyter notebook "Analyzing Historical Stock Revenue Data and Building a Dashboard.ipynb"
```

The notebook sets `pio.renderers.default = "plotly_mimetype+notebook"`, so each
figure is embedded in the `.ipynb` as Plotly JSON — GitHub renders these natively,
meaning the charts are visible and interactive directly in the repo without
running anything.

## Notes

Revenue data is scraped from static HTML snapshots hosted by the course, so the
revenue series ends where those snapshots do. Price data comes live from
`yfinance` and will extend to the current date on re-run — the plotting function
trims both to a shared cutoff so the comparison stays honest.
