# 📦 Smart Replenishment Planner

A web-based inventory replenishment tool that maps **warehouse availability** with **store stock health** data from Power BI, and generates smart order recommendations with pack-size rounding.

🔗 **Live Demo:** `https://<your-username>.github.io/replenishment-planner/`

---

## What It Does

Upload two Excel files → get a complete order plan:

| Input | Source |
|---|---|
| **Warehouse Report** | Order Able Manifest (Excel from warehouse system) |
| **Stock Health** | Export from Power BI (stock levels, sales, health status) |

The tool:
1. Maps SKUs between both files using Product Code / skuCode
2. Uses your Power BI data directly (Avg Daily Sales, Stock Health, Sale Qty 30D/90D)
3. Calculates **Qty to Buy** = (Avg Daily Sales × Target Days) − Current Store Stock
4. Rounds up to **pack size** using the Specification column (e.g., `1*12` → packs of 12)
5. Generates a **Reason** column explaining why each SKU needs ordering
6. Exports everything to Excel — all original columns preserved + 12 appended columns

## Appended Columns

| Column | Description |
|---|---|
| Store Stock | Current inventory from Power BI |
| Stock Health | Status from Power BI (Good, Under Observation, Dead Stock, etc.) |
| Sale Qty 30D | Last 30 days sales |
| Sale Qty 90D | Last 90 days sales |
| Avg Daily Sales | Average daily sales rate |
| Days of Cover Left | How many days current stock will last |
| Qty Needed | Raw quantity needed |
| Pack Size | Parsed from Specification column (1*12 → 12) |
| Packs to Order | Qty Needed ÷ Pack Size (rounded up) |
| Final Order Qty | Packs × Pack Size |
| Order Value (₹) | Final Qty × Order Price |
| Reason | Plain English explanation |

## Quick Start

### Option 1: Just Open It
1. Download `index.html`
2. Open it in Chrome / Edge / Firefox
3. That's it — no server needed, runs 100% in your browser

### Option 2: Host on GitHub Pages (so your team can use it)
1. Create a new repository on GitHub
2. Upload `index.html` to the repository
3. Go to **Settings → Pages**
4. Under "Source", select **Deploy from a branch**
5. Select **main** branch and **/ (root)** folder
6. Click **Save**
7. Your site will be live at `https://<username>.github.io/<repo-name>/`

### Option 3: Clone and Deploy
```bash
git clone https://github.com/<your-username>/replenishment-planner.git
cd replenishment-planner
# Just open index.html in a browser, or push to GitHub Pages
```

## Privacy & Security

- **All data stays in your browser.** No files are uploaded to any server.
- Processing happens 100% client-side using JavaScript.
- No analytics, no tracking, no cookies.
- Safe to use with confidential inventory data.

## Tech Stack

- React 18 (CDN)
- SheetJS/xlsx (CDN) for Excel read/write
- Babel Standalone for JSX compilation
- Zero build step — single HTML file

## Requirements

- A modern web browser (Chrome, Edge, Firefox, Safari)
- Two Excel files: Warehouse manifest + Stock health export from Power BI

---

Built for retail inventory management. Works with Miniso store data format.
