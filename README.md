# Jobber++

**Keyboard shortcuts, schedule view presets, and live weather for Jobber.**

Built by a field service business owner who uses Jobber every day. Jobber++ adds three features directly into the Jobber UI — no external dashboards, no logins, no friction.

---

## Features

### ⚡ Keyboard Shortcuts
Trigger common Jobber actions without touching the mouse.

| Shortcut (Mac) | Shortcut (Win) | Action |
|---|---|---|
| ⌘⇧S | Ctrl+Shift+S | Save current record |
| ⌘⇧E | Ctrl+Shift+E | Edit current record |
| ⌘⇧O | Ctrl+Shift+O | Primary action button |
| ⌘⇧C | Ctrl+Shift+C | New client |
| ⌘⇧R | Ctrl+Shift+R | New request |
| ⌘⇧M | Ctrl+Shift+M | Schedule: Month view |
| ⌘⇧L | Ctrl+Shift+L | Schedule: Week view |
| ⌘⇧D | Ctrl+Shift+D | Schedule: Day view |
| ⌘⇧U | Ctrl+Shift+U | Toggle unscheduled panel |
| ⌘⇧K | Ctrl+Shift+K | Toggle map view |

### 🗂 Schedule View Presets
Save any Jobber schedule URL configuration as a named button that lives directly in the schedule toolbar.

- Smart date handling — choose between "always show today" or a fixed historical date
- Drag to reorder, edit or delete any time via the ··· menu
- Syncs across Chrome devices

### ☀️ Weather Forecast Overlay
Live NOAA weather data overlaid directly on the Jobber schedule.

- Emoji icons on every day in month, week, and day views
- Three-tier display based on rain probability:
  - 0–25% → dominant condition icon only
  - 26–59% → dominant icon + faint precipitation risk icon
  - 60%+ → precipitation icon only (it's the story)
- Hover any day for high/low, rain %, and wind speed
- Current conditions widget in the schedule toolbar

---

## Installation

### From the Chrome Web Store
Search "Jobber++" or visit the store listing directly. Click **Add to Chrome**.

### From Source (Development)
1. Clone this repo
2. Open Chrome → `chrome://extensions`
3. Enable **Developer Mode** (top right)
4. Click **Load Unpacked** → select the `jobber-plus-plus` folder

---

## File Structure

```
jobber-plus-plus/
├── manifest.json           # MV3 manifest — permissions, content scripts
├── content.js              # Orchestrator — boots all three modules
├── content.css             # Injected styles for preset toolbar buttons
├── background.js           # Service worker — weather API, license stub
├── popup.html              # Tabbed popup UI
├── popup.js                # Popup logic: presets, shortcuts display, weather settings
├── popup.css               # Unified design system (Jobber green palette)
├── modules/
│   ├── shortcuts.js        # Keyboard shortcut definitions and handlers
│   ├── weather.js          # Weather fetch, icon logic, badge injection
│   └── presets.js          # Preset toolbar injection and management
├── utils/
│   ├── storage.js          # chrome.storage.sync/local helpers
│   └── urlUtils.js         # URL date detection, today substitution, name generation
└── icons/
    ├── icon16.png
    ├── icon48.png
    └── icon128.png
```

---

## Weather Logic

Weather icons use a three-tier system based on NOAA precipitation probability:

```
resolveWeatherIcons(shortForecast, rainPct)

  rainPct 0–25%   → { primary: dominantEmoji,  secondary: null }
  rainPct 26–59%  → { primary: dominantEmoji,  secondary: precipEmoji @ 40% opacity }
  rainPct 60%+    → { primary: precipEmoji,    secondary: null }
```

`dominantEmoji` is derived from the portion of the forecast string before "then" / "and".
`precipEmoji` scans the full string for precipitation keywords and returns the specific type — ⛈️ thunderstorms, 🌨️ snow/sleet, 🧊 freezing rain, 🌧️ rain — so snow plow operators, roofers, and landscapers each see what matters to them.

---

## Security

Pre-submission OWASP audit completed. Issues found and resolved:

- **XSS** — NOAA API data was being set via `innerHTML` in weather tooltips. Fixed: all external data now set via `textContent` and DOM methods only.
- **Unvalidated coordinates** — lat/lon from storage were interpolated directly into fetch URLs. Fixed: numeric validation and range checks applied before use.

---

## Privacy

Jobber++ collects no personal data. The only external network requests made are:

| Endpoint | Purpose |
|---|---|
| `api.weather.gov` | Fetch weather forecast (sends lat/lon only) |
| `geocoding-api.open-meteo.com` | Convert city name to coordinates |

No analytics. No tracking. No data brokers. Full privacy policy in `STORE_LISTING.md`.

---

## Stripe / Monetization (In Progress)

The extension is currently free. A `GATE_FEATURES` flag in `background.js` controls access gating — set to `false` for open access. When monetization is ready:

1. Set `GATE_FEATURES = true` in `background.js`
2. Uncomment the `VALIDATE_LICENSE` handler
3. Wire up Netlify functions: `create-checkout-session` and `stripe-webhook`
4. Add Supabase `subscribers` table
5. Update Account tab UI in `popup.html`

---

## Contact

Feedback: joelfriedrichdev+jobberpp@gmail.com
Built by [pizzacake.tech](https://pizzacake.tech)
