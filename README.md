# Maps Workflow

A browser tool that turns a list of Google Maps short URLs into a clean, enriched CSV.

**Live demo:** https://niro770.github.io/maps-workflow/

## What it does

Paste any number of `maps.app.goo.gl/...` URLs and the tool walks through six steps:

1. **Extract URLs** — dedupes, handles messy paste (CSV, text, anywhere)
2. **Resolve redirects** — follows short URLs through public CORS proxies
3. **Parse name & coords** — handles both `/place/Name/` and `?q=Name,Address` formats
4. **Fix LLC commas** — preserves names like "Edward Voccola & Co., LLC"
5. **Geocode missing** — Nominatim fallback for places without URL-embedded coords
6. **Google Places lookup** — phone, rating, review count via Places API (New)

Output: a downloadable CSV with name, address, phone, rating, review count, latitude, longitude, place ID, and source URL.

## Setup

1. Open https://niro770.github.io/maps-workflow/
2. Click `⚙ key` next to "run workflow"
3. Paste a Google Places API key (get one at [console.cloud.google.com](https://console.cloud.google.com/apis/library/places.googleapis.com))
4. Enable "Places API (New)" in your Google Cloud project
5. Test the connection, then paste your URLs and run

The key is saved to your browser's localStorage and is only sent to Google. Free tier covers ~10,000 lookups/month.

## Privacy

Nothing leaves your browser except:
- The Maps short URLs → CORS proxy → Google (to follow the redirect)
- The address → Nominatim (OpenStreetMap, for missing coords)
- The name + coordinates → Google Places API (for enrichment, only if you enable it)

No analytics, no tracking, no server.

## Tech

Single self-contained HTML file. No build step, no dependencies bundled — just open it. Uses Leaflet for the optional map view, and the Google Places API (New) for enrichment.

---

Built for Nir Hakim · Marketing 770
