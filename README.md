# StoreCheck

A Progressive Web App (PWA) for retail district leads/managers to track store visits. GPS auto-detects when you arrive at a location and logs the visit. The home screen shows every location sorted by how long it's been since your last visit — so you always know where you're overdue.

---

## What It Does

StoreCheck answers one question: **when did I last visit each store?**

Open the app and instantly see all your locations sorted from most overdue to most recently visited, color-coded by urgency. GPS runs in the background and automatically logs a visit when you arrive at any registered location — once per day per location, so driving by twice doesn't double-count. Add notes and visit type tags to build a searchable field log over time.

---

## Tabs

### Locations
The home screen. All 14 locations sorted by most overdue first with a summary bar showing how many are overdue. Each card shows the last visit date, color-coded green (recent), amber (7–13 days), or red (14+ days / never visited). Tap **Check in** to manually log a visit, or **📝 Note** to add a note — which also logs a visit if one hasn't been recorded today.

### Field Log
Your complete visit history grouped by day. Filter by store, visit type, or search by keyword across location names, notes, and tags. Matching keywords are highlighted in the results. Tap any visit card to edit its note.

### Manual Entry
Log a visit that GPS missed. Select a location, date, approximate time, visit type, and notes, then save. The entry appears immediately in the Field Log.

### Settings
Three sections in one tab:
- **GPS Setup** — register each location's coordinates and adjust the detection radius
- **Data & Backup** — download a JSON backup, export to CSV, or restore from a backup file
- **Danger Zone** — clear all data

---

## Visit Type Tags

Each visit can be tagged with one of the following:

| Tag | Use for |
|-----|---------|
| **Normal Visit** | Routine check-in |
| **Support Request** | Responding to a store issue or ticket |
| **Follow-up** | Returning after a previous issue |
| **Other** | Anything that doesn't fit the above |

---

## File Structure

All five files must be in the same folder for the PWA to work:

```
storecheck.html    — the main app
manifest.json      — PWA manifest (makes it installable)
sw.js              — service worker (offline support + GPS persistence)
icon-192.png       — app icon (192×192)
icon-512.png       — app icon (512×512)
README.md          — this file
```

---

## Hosting on GitHub Pages

1. Create a **public** repository on GitHub
2. Upload all five app files to the repository root
3. Go to **Settings → Pages**, set source to **main / root**, click Save
4. After ~60 seconds your app is live at:
   ```
   https://yourusername.github.io/your-repo-name/storecheck.html
   ```

---

## Installing as a PWA (Recommended)

Installing StoreCheck as a PWA gives it much better GPS reliability than a browser tab. On Android, an installed PWA runs in its own process and GPS stays active even when the screen is off.

### On Android (Chrome)
1. Open your GitHub Pages URL in Chrome
2. A green **"Install StoreCheck"** banner appears at the top — tap **Install**
3. The app is added to your home screen with its own icon
4. Always open it from the home screen icon, not the browser

### On iPhone (Safari)
1. Open your GitHub Pages URL in Safari
2. Tap the **Share** button → **Add to Home Screen** → **Add**

> GPS reliability on iPhone is lower than Android. iOS aggressively suspends background processes even for installed PWAs.

---

## First-Time Setup

### Register Your Locations
1. Drive to each store
2. Open the app and go to the **Settings** tab
3. Tap the store's card — the app saves your current GPS coordinates
4. Repeat for every location (one-time setup)

### Set Detection Radius
The radius slider in Settings controls how close you need to be before a visit is logged. Start at **100m** and adjust:
- Dense areas or indoor stores → 50–75m
- Large parking lots or outdoor locations → 150–200m

---

## GPS Notes

GPS auto-logging requires the app to be open. For best results:

- **Install as a PWA** — most reliable setup on Android
- Open the app at the start of your day and leave it running
- On Samsung devices: **Settings → Apps → StoreCheck → Battery → Unrestricted**

If GPS misses a visit, use the **Manual Entry** tab to add it.

---

## Field Log Search & Filters

The Field Log supports three simultaneous filters:

- **Keyword search** — searches location names, note text, and visit type labels. Matches are highlighted in green.
- **Store filter** — tap one or more store names to show only those locations. Multi-select.
- **Type filter** — filter by Normal, Support, Follow-up, Other, or No tag. Multi-select.

A results count shows how many visits match, and a **Clear filters** link resets everything at once.

---

## Data & Backup

All data is saved in the browser's `localStorage`. To protect against data loss:

- Go to **Settings → Data & Backup → Download Backup** regularly
- Restore on a new device or browser by uploading the `.json` file
- CSV export includes location, date, time, visit type, and notes — ready for Excel or Google Sheets

---

## Locations

Pre-loaded with the following locations:

| | | | |
|---|---|---|---|
| Store #102 | Store #103 | Store #104 | Store #201 |
| Store #203 | Store #205 | Store #206 | Store #207 |
| Store #208 | Store #211 | Store #222 | Store #240 |
| Store #364 | Store #381 | HQ | |

To change the location list, open `storecheck.html` in a text editor and update the `LOCATIONS` array near the top of the `<script>` section. Re-upload to GitHub after editing.

---

## Browser Compatibility

| Browser | GPS | PWA Install | Recommended |
|---------|-----|-------------|-------------|
| Chrome (Android) | ✅ | ✅ | ✅ Best experience |
| Samsung Internet | ✅ | ✅ | ✅ Works great |
| Safari (iOS) | ✅ | ✅ via Add to Home Screen | ✅ Good |
| Chrome (desktop) | ✅ | ✅ | For setup/testing only |
| Firefox | ✅ | ❌ | Not recommended |

---

*Built with Claude*
