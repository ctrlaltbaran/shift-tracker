# StoreCheck

A lightweight Progressive Web App (PWA) for retail district managers to track store visits. GPS auto-detects when you arrive at a location and logs the visit. The home screen shows every location sorted by how long it's been since your last visit so you always know where you're overdue.

---

## What It Does

StoreCheck answers one question: **when did I last visit each store?**

Open the app and you instantly see all your locations sorted from most overdue to most recently visited, color-coded by urgency. GPS runs in the background and automatically logs a visit when you arrive at any registered location — once per day per location, so driving by twice doesn't double-count.

---

## Features

### Home Screen
- All locations sorted by most overdue first
- Color coding — green (recent), amber (7–13 days), red (14+ days or never visited)
- "Here now" indicator when GPS detects your presence
- Summary bar showing how many locations are overdue
- One-tap manual check-in on any location

### GPS Auto-Detection
- Continuously scans in the background while the app is open
- Automatically logs a visit when you arrive within range of a registered location
- Configurable detection radius (30m–300m)
- One visit logged per location per day — no duplicates from passing through

### History
- Day-by-day log of every location visited
- Shows approximate time of each visit
- Tap ✕ on any visit to remove it if something was logged by mistake

### Log Past Visit
- Manually log a visit to any location on any past date
- Useful when GPS missed you or you forgot to open the app

### Data & Backup
- **JSON backup** — exports everything (visits + GPS pins) to a file you can restore on any device
- **CSV export** — one row per visit with location, date, and time; open in Excel or Google Sheets
- **Restore from backup** — upload a JSON backup to merge data; duplicates are skipped automatically
- **Clear all data** — wipe everything with a confirmation prompt

---

## File Structure

```
storecheck.html    — the main app
manifest.json      — PWA manifest (makes it installable)
sw.js              — service worker (offline support + background persistence)
icon-192.png       — app icon (192×192)
icon-512.png       — app icon (512×512)
README.md          — this file
```

All five app files must be in the same folder for the PWA to work correctly.

---

## Hosting on GitHub Pages

1. Create a **public** repository on GitHub
2. Upload all five files to the repository root
3. Go to **Settings → Pages**, set source to **main / root**, click Save
4. After ~60 seconds your app is live at:
   ```
   https://yourusername.github.io/your-repo-name/storecheck.html
   ```

---

## Installing as a PWA (Recommended)

Installing StoreCheck as a PWA on your phone gives it much better GPS reliability than running it as a browser tab. On Android (including Samsung Fold), an installed PWA runs in its own process and GPS stays active even when the screen is off or you switch apps.

### On Android (Chrome)
1. Open your GitHub Pages URL in Chrome
2. A green **"Install StoreCheck"** banner will appear — tap **Install**
3. The app is added to your home screen with its own icon
4. Always open it from the home screen icon, not the browser

### On iPhone (Safari)
1. Open your GitHub Pages URL in Safari
2. Tap the **Share** button → **Add to Home Screen**
3. Tap **Add**

> **Note:** GPS reliability on iPhone is lower than Android because iOS aggressively suspends background processes. Opening the app from the home screen icon (not Safari) gives the best results.

---

## First-Time Setup

### Register Your Locations
1. Drive to each store
2. Open the app and go to the **Setup** tab
3. Tap the store's card — the app saves your current GPS coordinates
4. Repeat for every location
5. You only need to do this once per location

### Set Detection Radius
The radius slider in Setup controls how close you need to be before a visit is logged. Start at **100m** and adjust based on how your stores are laid out:
- Stores in dense areas → smaller radius (50–75m)
- Stores with large parking lots → larger radius (150–200m)

---

## GPS Notes

GPS auto-logging only works while the app is open. For the best experience:

- **Install as a PWA** (see above) — this is the most reliable setup on Android
- Open the app at the start of your day and leave it running
- On Samsung devices, go to **Settings → Apps → StoreCheck → Battery** and set to **Unrestricted** to prevent the OS from suspending it

If GPS misses a visit, use the **Log Visit** tab to add it manually.

---

## Locations

Pre-loaded with the following locations:

| | | | |
|---|---|---|---|
| Store #102 | Store #103 | Store #104 | Store #201 |
| Store #203 | Store #205 | Store #206 | Store #207 |
| Store #208 | Store #211 | Store #222 | Store #364 |
| Store #381 | HQ | | |

To change the location list, open `storecheck.html` in a text editor and update the `LOCATIONS` array near the top of the `<script>` section. After editing, re-upload the file to GitHub.

---

## Browser Compatibility

| Browser | GPS | PWA Install | Recommended |
|---------|-----|-------------|-------------|
| Chrome (Android) | ✅ | ✅ | ✅ Best experience |
| Samsung Internet | ✅ | ✅ | ✅ Works great on Fold |
| Safari (iOS) | ✅ | ✅ via Add to Home Screen | ✅ Good |
| Chrome (desktop) | ✅ | ✅ | ✅ Works well |
| Firefox | ✅ | ❌ | For backup use only |

---

## Data Storage

All data is saved in the browser's `localStorage` on the device where you use the app. Clearing browser data or switching browsers will erase your visit history — use the **JSON backup** in the Data tab regularly to protect your data.

---

*Built with Claude — from idea to working PWA in a single conversation.*
