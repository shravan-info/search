# दहावी शोध — Class 10 Search (Maharashtra Board)

A fast, bilingual (मराठी + English) question–answer search engine for **Std X, Maharashtra State Board (SSC)**.
Static site: plain HTML + JSON, no build step, no dependencies.

## What is inside

- **2,035 questions** across all 9 SSC subjects: Marathi, Hindi, English, Algebra, Geometry,
  Science & Technology Part 1, Science & Technology Part 2, History & Political Science, Geography.
- Every question and answer exists in **Marathi and English**; 150+ multiple-choice questions carry
  four options with the correct option marked.
- Alphabet shards `data/a.json` … `data/z.json` (+ `data/0.json` for questions starting with a digit or symbol).
- `data/index.json` — a compact inverted token index (both languages) used for instant prefix search.
- `data/manifest.json` — counts, subject list and Marathi coverage.
- **5,300 real websites** in `data/sites/a.json … z.json` (+ `data/sites/index.json`,
  `data/sites/manifest.json`), spread over ~2,860 domains: board and government portals, study
  and solutions sites, Marathi newspapers, Wikipedia articles in both languages. Each entry keeps
  its URL, title, description, category and the source article it was found in.
- `scripts/harvest.py` + `scripts/build_sites.py` — the crawler that collects those URLs from
  Wikipedia's APIs (article search, extracts, external links) and curates them into shards.
- `.github/workflows/crawl-sites.yml` — runs the crawler on GitHub's runners on a schedule and
  commits the refreshed index; `.github/workflows/deploy-pages.yml` publishes the site.

## Two search modes

The header has two tabs: **प्रश्नोत्तरे** (Q&A, 2,035 entries) and **वेबसाइट्स** (websites, 5,300).
Both use the same instant-search engine; each mode has its own index and letter shards, loaded
lazily the first time that mode is opened.

## How the search works

1. `index.json` is fetched once (~180 KB gzipped) and gives token → record-id postings.
2. A query is tokenised, matched by prefix with IDF weighting, and the top candidates are re-ranked.
3. Only the shards holding the top hits are fetched (~8 KB gzipped each) and cached.
4. Results are rendered instantly; ↑/↓ navigate, `/` focuses the box, Esc clears.

## Run locally

```bash
python3 -m http.server 8000     # then open http://localhost:8000
```

## Syllabus

Chapter lists follow the current Balbharati textbooks for Std X. Questions and answers are compiled
for study use; always cross-check with your textbook for board-exam wording.
