# Popular Movies API

This project is a Jupyter Notebook experiment that retrieves popular movie data from [The Movie Database (TMDB)](https://www.themoviedb.org/) and turns selected fields into a pandas DataFrame. The notebook can also save the DataFrame as a CSV file.

## Project files

- `movies_api.ipynb` — sends requests to the TMDB popular-movies endpoint, selects movie fields, and exports the result.
- `config.py` — provides the `API_KEY` imported by the notebook.
- `movies.xls` — an existing spreadsheet in the project folder; the notebook does not currently read or update it.

## Requirements

- Python 3
- A TMDB API key
- Jupyter Notebook
- `pandas` and `requests`

Install the Python packages from PowerShell:

```powershell
python -m pip install jupyter pandas requests
```

## Configure the API key

The notebook imports `API_KEY` from `config.py`. Set it to your own TMDB API key before running the notebook:

```python
API_KEY = "YOUR_TMDB_API_KEY"
```

Do not publish or commit a real API key. The current `config.py` contains a hard-coded credential; if it has been shared or committed publicly, replace it in TMDB and keep the replacement private.

## Run the notebook

From the project folder, start Jupyter:

```powershell
jupyter notebook movies_api.ipynb
```

Run the notebook cells in order. The first request uses TMDB's `/3/movie/popular` endpoint. The notebook selects these columns:

| Column | Description |
| --- | --- |
| `id` | TMDB movie identifier |
| `title` | Movie title |
| `overview` | Movie synopsis |
| `release_date` | Release date |
| `popularity` | TMDB popularity score |
| `vote_average` | Average user rating |
| `vote_count` | Number of votes |

The final export cell writes `movies.csv` to the current working directory. Pandas includes the DataFrame index in the CSV by default.

## Current limitation

The notebook's multi-page request currently builds its URL with `&page{i}` instead of TMDB's `&page={i}` query parameter. As a result, the loop does not correctly request the intended page numbers, so the combined data should not be treated as a complete multi-page result. The loop also requests pages through 1001, which may exceed the endpoint's supported page range. Correct the page parameter and use a supported range before relying on that export.