# Web Crawler & Word Cloud Generator

A Python tool that crawls a website, extracts and cleans visible text from each page, and generates a word cloud visualization for every page collected. Built as an NLP text-mining assignment using BBC News as the target site.

## Overview

The script performs a breadth-first crawl of a given website, keeping only internal (same-domain) pages that meet a minimum word count. For each qualifying page it strips out HTML noise, normalizes the text (lowercasing, lemmatization, stopword removal), and renders a word cloud image summarizing the page's most frequent terms.

## Key Features

- **BFS web crawler**: follows internal links from a starting URL up to a configurable page limit, skipping anchors, mailto, and JavaScript links
- **HTML text extraction**: strips scripts, styles, and markup with BeautifulSoup to isolate visible text
- **Text normalization pipeline**: alphabetic-only tokenization, custom stopword list (colors, timestamps, site-generic terms), and WordNet lemmatization to merge word variants (e.g. "animals" → "animal")
- **Minimum content filter**: only pages with at least a configurable word count are processed, avoiding thin/low-content pages
- **Word cloud generation**: renders and saves a 1600x900 word cloud image per page using the `wordcloud` library
- **Per-page output**: saves both the cleaned raw text and the generated word cloud image for each crawled page

## Tech Stack

- `requests` — HTTP fetching
- `BeautifulSoup` (bs4) — HTML parsing and text extraction
- `nltk` (WordNetLemmatizer) — lemmatization
- `wordcloud` — word cloud rendering
- `matplotlib` — image saving

## Requirements

```bash
pip install requests beautifulsoup4 wordcloud matplotlib nltk
```

On first run, uncomment and execute `nltk.download("wordnet")` to fetch the WordNet corpus.

## Configuration

| Setting | Default | Description |
|---|---|---|
| `START_URL` | `https://www.bbc.com/` | Root URL to begin crawling from |
| `MAX_PAGES` | 20 | Maximum number of qualifying pages to collect |
| `MIN_WORDS` | 500 | Minimum word count for a page to be kept |
| `OUTPUT_DIR` | `wordcloud_output` | Folder where results are saved |

## Usage

```bash
python Assign_4.py
```

The script will:
1. Crawl the site breadth-first, starting from `START_URL`.
2. Keep the first `MAX_PAGES` internal pages with at least `MIN_WORDS` words.
3. For each page, save `page_XX_text.txt` (URL + cleaned text) and `page_XX_wordcloud.png` (word cloud image) into `OUTPUT_DIR`.

## Results

Successfully crawled and processed 20 pages from bbc.com (news, sport, business, culture, travel, and regional news sections), each generating a cleaned text file and a corresponding word cloud image highlighting dominant topics per section.

## Author

Salem Eidhah Bin Ishaq
