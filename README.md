# The Bhagavata Podcast — Analytics Dashboard

A self-contained monthly analytics dashboard for [The Bhagavata Podcast](https://www.youtube.com/@TheBhagavataPodcast), produced by the Gaudiya Studies Research Programme at the Oxford Centre for Hindu Studies.

It pulls together YouTube Studio and Buzzsprout numbers each month into one page: headline KPIs, charts, prioritised actions to improve, and selected viewer comments.

## View it

The dashboard is a single file, `index.html`, with all data embedded — no build step, no server. Open it locally in any browser, or publish it free via **GitHub Pages**:

1. Push this repo to GitHub.
2. Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch**.
3. Branch: `main`, folder: `/ (root)`. Save.
4. After a minute it's live at `https://<your-username>.github.io/<repo-name>/`.

## How it updates each month

All the data lives in one place — the `<script id="dashboard-data">` JSON block near the bottom of `index.html`. To add a month, append one object to the `months` array:

```json
{
  "key": "2026-06",
  "label": "June 2026",
  "youtube": { "views": 0, "impressions": 0, "ctr": 0, "watchHours": 0, "subsNet": 0 },
  "buzzsprout": { "downloads": 0, "downloads30d": 0 },
  "episodes": [ ... ],
  "platforms": [ ... ],
  "comments": [ ... ],
  "actions": [ ... ]
}
```

Also update `lastUpdated`, `current.subscribers`, and the `annual` block. The KPI cards then auto-compare to the previous month, and the trend charts extend automatically.

In practice this is run for you: the monthly data-collection workflow reads the dashboards, then appends the new month and commits the change.

## Files

- `index.html` — the dashboard (data + charts + styling, all inline)
- `podcast-data-YYYY-MM.md` — the raw monthly data block each update is built from
- `README.md` — this file

## Data sources

YouTube Studio (channel analytics, per-video stats, comments) and Buzzsprout (downloads, listening apps). All figures are read directly from the live dashboards; any value that couldn't be read cleanly is flagged rather than estimated.
