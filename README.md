# Premier League Club Performance & Discipline Index

This project builds a composite indicator for Premier League teams across multiple seasons using match-level CSV data from Football-Data.co.uk.

## Main notebook
Open and run:

`notebooks/01_premier_league_index.ipynb`

## Install requirements
```bash
pip install -r requirements.txt
```

## Output files
- `data/raw/` downloaded season CSVs
- `data/processed/team_season_index.csv`
- `visuals/` generated charts
- `report/report_draft.md`

## Git workflow
Commit after each meaningful change.
Example:
```bash
git add .
git commit -m "Add data download and cleaning section"
```
