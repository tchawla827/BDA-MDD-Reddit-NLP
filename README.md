# MDD Reddit Analytics
**Big Data Analytics (BDA) Course Project — 6th Semester**  
**Domain**: HDA-4 | **Group**: 4

## Overview
This repository contains an academic research implementation for text classification. Specifically, we classify and detect Natural Language indicators pointing to Major Depressive Disorder (MDD) symptoms extracted from Reddit self-reports.

### Team Members
- Krishna Sikheriya (IIT2023139)
- Priyam Jyoti Chakrabarty (IIT2023147)
- Tavish Chawla (IIT2023150)

## Directory Structure
- `data/` : Ignored by Git. Run the pipeline to generate `raw` and `processed` data.
- `notebooks/` : Contains the Submission version PRAW notebook (`Assignment_1_PRAW_Extraction.ipynb`).
- `src/` : Modular, purely `.py` implementation (scraper, pipeline logic).
- `docs/` : Methodology workflow, PDF assets, and initial assignment instructions.

## Installation & Setup
1. Standardize virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate  # On Unix
.venv\Scripts\activate     # On Windows
```

2. Install dependencies:
```bash
python -m pip install -r requirements.txt
```

## Running Assignment 1
To complete the *Data Extraction* assignment, run the core pipeline Python script:
1. Open terminal in the project root.
2. Ensure you have activated your environment and installed dependencies.
3. Run the complete pipeline via terminal:
```bash
python src/pipeline.py
```
This automatically scrapes PullPush.io, exports `data/raw/reddit_raw.csv`, processes linguistic parameters via NLP layers, and yields the final `data/processed/reddit_mdd_cleaned.csv` all autonomously.
