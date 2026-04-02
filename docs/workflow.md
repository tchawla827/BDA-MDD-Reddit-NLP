# Workflow Documentation: Data Extraction & Cleaning

**Deliverable 1 for Assignment 1**  
**Task ID:** HDA-4

## 1. Data Source Selection
Initially, Reddit's official API (`praw`) was considered. However, due to restrictive modern API limits and manual developer approval delays, we pivoted to **PullPush.io**, a recognized archival dataset for academic research.
- **Advantage:** Unrestricted rate limits, historical retrieval without API keys, access to deleted/removed records.

## 2. Scraping Methodology
We implemented a custom Python object (`PullPushScraper` in `src/scraper.py`) utilizing the `requests` library.
1. **Target Subreddits:**
   - **MDD Class (Class 1):** `r/depression` (2,500 posts), `r/SuicideWatch` (2,500 posts)
   - **Control Class (Class 0):** `r/CasualConversation` (5,000 posts)
2. **Pagination Strategy:** Since PullPush allows max 100 posts per request, we iteratively send requests where `before=EPOCH_TIMESTAMP`, extracting older and older posts over time.
3. **Filtering at Source:** We excluded submission bodies that were exactly `[removed]` or `[deleted]` to ensure high data quality upfront.

## 3. Data Cleaning Pipeline
Conducted entirely within the `notebooks/01_extraction_and_cleaning.ipynb` notebook.
- **Lowercase Conversion:** Normalizes entire strings.
- **Regex Cleaning:** Removed all HTTP links, special symbols, newlines, and digits, leaving strictly `[a-z\s]`.
- **Stop Words:** Implemented NLTK's English stop words removal to increase signal-to-noise ratio for TF-IDF / embeddings.
- **Extreme Length Clipping:** Automatically removed empty strings or documents containing fewer than 5 cleaned words.

## 4. Feature Engineering
We initialized a foundational sentiment analysis layer over the uncleaned text using **VADER** from `vaderSentiment`. This adds `sentiment_score` to the resultant CSV, creating a numerical baseline for emotional analysis before moving onto ClinicalBERT in Assignment 2.

## 5. Output
Generated two datasets:
- `data/raw/reddit_raw.csv` - The original unmodified posts.
- `data/processed/reddit_mdd_cleaned.csv` - The preprocessed training dataset designated as the **Secondary Dataset Deliverable**.
