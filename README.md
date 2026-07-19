# 🛒 Co-ord Women — BD E-Commerce Scraper

**Author:** Mohammod Hamed Hasan

**Email:** hamedhasan.dev@gmail.com

**LinkedIn:** [devhamed](https://www.google.com/search?q=https://www.linkedin.com/in/devhamed/)

An automated web scraping engine designed to target, extract, and monitor women's co-ord/cord set products across major Bangladeshi e-commerce platforms and marketplaces. Extracted data is automatically cleaned, deduplicated, and inserted directly into a designated Google Sheet.

---

## 🚀 Features

* **Multi-Platform Engine:** Native scrapers designed for Shopify JSON APIs, WooCommerce architectures, React SPA layouts (Daraz embedded JSON data strings), and generic custom e-commerce structures.
* **Target Sites:** Daraz, AjkerDeal, Othoba, Amirá Bangladesh, Aurum Bangladesh, Ecstasy, Hoor The Brand, Khacha, Inteblu, ComfyStyle, CityStanja, FashionHQ, WardrobeBySyra, and Freeland.
* **Advanced Bot Bypass (Zero Budget):** Utilizes `cloudscraper` paired with user-agent rotation (25+ real browser configurations), randomized human-like delays (`human_delay`), dynamic referer headers, and session cookie handling.
* **Smart Parsing:** Automatically handles translation of Bengali numerals (e.g., '০১২৩৪৫৬৭৮৯' ➔ '0123456789') and regex-cleans raw HTML strings into refined numeric prices.
* **Real-time Google Sheets Integration:** Automatically authenticates via Google Service Account credentials to pull existing product records, cross-check links for incremental updates (avoids duplicates), and append fresh data points.

---

## 📋 Pre-requisites & Setup

### ⚠️ IMPORTANT: Share your Google Sheet

Before executing the scraper, you must grant access to the automated Google Service Account:

1. Open your target Google Sheet.
2. Click **Share** (top-right).
3. Add the following email address as an **Editor**:
`hamed-sheet-writer@akrub-cord-set.iam.gserviceaccount.com`

---

## 🛠️ How to Run (Step-by-Step)

The project is structured to run sequentially via Python notebooks (Google Colab/Jupyter) or as a script:

### Step 1: Install Dependencies

Run **Cell 1** to pull the necessary packages silently into your environment:

```bash
pip install cloudscraper beautifulsoup4 gspread google-auth lxml --quiet

```

### Step 2: Load Credentials & Site Config

Run **Cell 2**. This initializes search keywords (`cord set`, `co-ord set`, `matching set women`, etc.) and automatically constructs your service account credential file (`credentials_json.json`) inline.

### Step 3: Spin Up Engine Modules

Run **Cell 3 & 4** to load the custom User-Agent pools, connection session parameters, Google Sheets middleware layer, and the site-specific scraper factories (`ShopifyScraper`, `WooCommerceScraper`, `DarazScraper`, etc.).

### Step 4: Run Orchestration & Scrape

Run **Cell 6** to execute the scraper. You can modify your run scope using the built-in parameters:

* `All sites`: Scrapes all 14 configured platforms.
* `Shopify only (fast test)`: Targets fast JSON endpoints (`inteblu`, `comfystyle`, `citystanja`).
* `Daraz only` / `WooCommerce only`: Target specific architecture sets.
* `Dry run (no write)`: Extracts product data cleanly without appending rows to your remote spreadsheet.

---

## 📊 Extracted Data Schema

The following structural headers are checked and generated inside your designated target worksheet if missing:

| Column | Description |
| --- | --- |
| **Product Name** | Title of the matching co-ord set item |
| **Price** | Normalized numeric pricing string |
| **Currency** | Defaulted to `BDT` |
| **Web Link** | Direct URL to the item page (used for incremental tracking deduplication) |
| **Date** | Date of capture timestamp (`YYYY-MM-DD`) |
| **Source** | Platform provider label |
