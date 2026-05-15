# Track Discovery

A personal music discovery explorer — timeline, label, source, and graph views — built from an Airtable export.

## Setup

1. **Fork or clone this repo** on GitHub
2. Go to **Settings → Pages** → set source to `main` branch, `/ (root)` folder
3. Your site will be live at `https://yourusername.github.io/track-discovery`

## Updating your data

When you want to refresh tracks from Airtable:

1. In Airtable: **Grid view → Download CSV**
2. Replace `tracks.json` in this repo with the new export (run the conversion script below, or use the hosted version)

### Quick conversion (Python)

```python
import csv, json

rows = []
with open('Track_Discovery_Main_View.csv', encoding='utf-8-sig') as f:
    reader = csv.DictReader(f)
    for r in reader:
        if r['Track Title'].strip() and r['Artist'].strip():
            rows.append({
                'title': r['Track Title'].strip(),
                'artist': r['Artist'].strip(),
                'label': r['Label'].strip() or None,
                'year': r['Year'].strip() or None,
                'source': r['Source'].strip() or None,
                'sourceDetail': r['Source Detail'].strip() or None,
                'dateHeard': r['Date Heard'].strip() or None,
                'status': r['Status'].strip() or None,
                'genre': r['Genre/Style'].strip() or None,
                'mood': r['Energy/Mood'].strip() or None,
                'notes': r['Notes'].strip() or None,
                'bandcamp': r['Bandcamp Search'].strip() or None,
                'discogs': r['Discogs Search'].strip() or None,
            })

with open('tracks.json', 'w') as f:
    json.dump(rows, f)
print(f'{len(rows)} tracks written')
```

## Views

- **Timeline** — tracks grouped by month, filterable by genre/mood/status
- **Graph** — force-directed node graph; switch between label, source, genre, or source-detail clustering
- **Labels** — browse by record label
- **Sources** — browse by how you discovered tracks (Instagram, Radio, DJ Mix, etc.)

Click any track to open the detail panel with Bandcamp + Discogs links.
