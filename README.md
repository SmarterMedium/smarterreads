# SmarterReads — AI Literacy Reading Room

Content repository for the Assisting Intelligence Reading Room, a curated book catalog deployed as a SCORM 2004 learning app.

## Repository Structure

```
smarterreads/
├── config.json              ← Branding, affiliate ID, content source URLs
├── catalog-template.csv     ← Import template for Google Sheets catalog
├── assets/
│   └── AI_Logo_LongWH.png   ← Assisting Intelligence logo
├── reviews/
│   ├── _TEMPLATE.md         ← Review authoring template
│   └── fuller-operating-manual.md
└── README.md
```

## How It Works

The SCORM shell (deployed separately in the LMS) fetches content from two sources at runtime:

1. **Google Sheet** (published as CSV) — The book catalog. One row per book. Add, edit, or remove books anytime without touching the LMS.
2. **This repository** (served via GitHub Pages) — Editorial reviews as markdown files, branding config, and the logo.

No rebuild or redeployment required for content updates.

## Setup

### 1. Enable GitHub Pages

Go to **Settings → Pages** and set the source to `main` branch, root (`/`). Your content will be served at:

```
https://smartermedium.github.io/smarterreads/
```

### 2. Create the Google Sheet

1. Create a new Google Sheet
2. Import `catalog-template.csv` as the first sheet (File → Import → Upload)
3. Publish the sheet: **File → Share → Publish to web** → Select "Comma-separated values (.csv)" → Publish
4. Copy the published CSV URL
5. Paste it into `config.json` under `content.catalog_csv_url`

### 3. Add Books

Add a row to the Google Sheet. Required columns:

| Column | Description |
|--------|-------------|
| `title` | Book title |
| `author` | Author name(s) |
| `hook` | One-line editorial hook for the card |
| `source` | `bookshop`, `gutenberg`, `archive`, `pdf`, or `direct` |
| `order_url` | Full URL for the order/read button |
| `shelf` | Category label (e.g., "Foundations") |

Optional but recommended: `isbn` (for cover images via Open Library), `review_slug` (links to a review file), `price`, `sort_order`.

### 4. Write Reviews

1. Copy `reviews/_TEMPLATE.md`
2. Name it to match the `review_slug` in the Sheet (e.g., `fuller-operating-manual.md`)
3. Fill in the frontmatter and editorial content
4. Commit and push — the review is live immediately

### Cover Images

Covers resolve in this order:
1. `image_url` column (if set) — direct URL to a cover image
2. `isbn` column — fetched from Open Library: `https://covers.openlibrary.org/b/isbn/{isbn}-L.jpg`
3. Neither — typographic fallback card (title + author on dark background)

## Source Types

| Source | Button Label | Behavior |
|--------|-------------|----------|
| `bookshop` | Order on Bookshop.org | Opens affiliate link (ID: 109081) |
| `gutenberg` | Read Free | Opens Project Gutenberg page |
| `archive` | Borrow Free | Opens Internet Archive page |
| `pdf` | Read Now | Opens PDF URL |
| `direct` | Visit Source | Opens external URL |

## Affiliate

Bookshop.org affiliate ID: `109081`. Commission supports Assisting Intelligence and independent bookstores.

## Content License

Editorial reviews and catalog curation © Assisting Intelligence / SmarterMedium. All rights reserved.
