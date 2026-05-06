# Tender Intelligence Dashboard

A data analytics dashboard for Kuwait Ministry of Islamic Affairs tender data.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The dashboard — open this in a browser or host it online |
| `tenders.json` | Your data (auto-generated, update whenever you have new data) |
| `convert_tenders.py` | Converts raw scraped text → `tenders.json` |

---

## Step 1 — Convert your data

Every time you have new scraped data, run:

```bash
python convert_tenders.py your_data.txt
```

This produces `tenders.json`. The script expects a plain text file in the same format as your scraper output (the `Number: … / Tender Number: …` header format with CSV rows below).

If you paste data directly into the script's `SAMPLE` variable (at the top), just run:

```bash
python convert_tenders.py
```

---

## Step 2 — Host on GitHub Pages (free, permanent URL)

### First-time setup

1. Go to [github.com](https://github.com) and create a free account if you don't have one
2. Click **New repository** → name it `tender-dashboard` → set to **Public** → click **Create repository**
3. Upload these 3 files: `index.html`, `tenders.json`, `convert_tenders.py`
   - Click **Add file → Upload files** and drag them in
   - Click **Commit changes**
4. Go to **Settings → Pages** (left sidebar)
5. Under **Source**, select **Deploy from a branch**
6. Set branch to `main`, folder to `/ (root)` → click **Save**
7. Wait ~60 seconds. Your dashboard will be live at:
   ```
   https://YOUR-USERNAME.github.io/tender-dashboard/
   ```

### Updating data (after first setup)

When you have new scraped data:
1. Run `python convert_tenders.py new_data.txt` to regenerate `tenders.json`
2. Go to your GitHub repo
3. Click on `tenders.json` → click the **pencil icon** to edit → paste the new JSON content → **Commit changes**
   - OR: delete the old file and re-upload the new one

The dashboard updates automatically within a minute.

---

## Dashboard views

| Tab | What it shows |
|-----|---------------|
| **Overview** | Summary stats, most active companies, win rates |
| **Winners & Rankings** | Full leaderboard sorted by wins, win rate, avg position |
| **Bid Aggressiveness** | Who bids lowest, average gap from winner, competitive assessment |
| **Company Comparison** | Pick any two companies for a head-to-head breakdown |
| **Tender Breakdown** | All tenders, searchable, with full bid tables |

---

## Data format reference

Your input text should have tenders separated like this:

```
Number: [tender number]           ← OR: Tender Number:
Tender Subject: [subject text]
Organization: [org name]
Publish Date: Month DD YYYY
Closing Date: Month DD YYYY
Meeting Date: Month DD YYYY
No,Contractor number,Contractor name,Status,Reason,Offer Total,Position,Difference L1,L1 Percentage,Difference amongst bidder,Percentage amongst bidder
1,12345,Company Name,مقبول,Approved,2500000,1,0,0%,0,0%
2,67890,Another Company,مقبول,Approved,2700000,2,200000,8%,200000,8%
...
```

- **Offer Total** can be a number (KWD amount) OR a percentage like `-51.6%`
- **Status** `مقبول` = approved, `مستبعد` = excluded
- Excluded rows will have empty Position/Difference fields — that's fine

---

## Troubleshooting

**"tenders.json not found"** — The dashboard falls back to built-in sample data. Make sure `tenders.json` is in the same folder as `index.html`.

**Charts don't show** — Open browser DevTools (F12) → Console tab to see any errors.

**Arabic text looks wrong** — Make sure your text file is saved as UTF-8 encoding.
