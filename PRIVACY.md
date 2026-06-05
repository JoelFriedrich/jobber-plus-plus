# Privacy Policy — Jobber++

**Last updated: May 2026**

Jobber++ is a Chrome extension built for field service professionals who use Jobber (secure.getjobber.com). This policy describes what data the extension accesses, how it is used, and what is never collected.

---

## Data We Collect

### Location (Optional)
If you use the Weather feature, you may enter a city name. That city name is sent to the [Open-Meteo Geocoding API](https://open-meteo.com) to retrieve latitude and longitude coordinates. Those coordinates are:
- Stored locally on your device via `chrome.storage.local`
- Sent to the [NOAA Weather API](https://api.weather.gov) to fetch forecast data

Your location is never sent to any server operated by Jobber++ or its developer.

### Schedule View URLs
If you use the View Presets feature, Jobber++ saves Jobber schedule URLs that you choose to save. These are stored via `chrome.storage.sync`, which means Google may sync them across your signed-in Chrome devices. No URL data is sent to any server operated by Jobber++ or its developer.

### Keyboard Input
Jobber++ listens for specific key combinations on Jobber pages only. No keystrokes are logged, recorded, or transmitted anywhere.

---

## Data We Do Not Collect

- No names, email addresses, or personal identifiers
- No Jobber account credentials or session data
- No client, job, invoice, or business data from your Jobber account
- No browsing history
- No analytics or usage tracking
- No crash reports
- No advertising identifiers

---

## Third-Party Services

| Service | Purpose | Data Sent |
|---|---|---|
| [NOAA Weather API](https://api.weather.gov) | Fetch weather forecasts | Latitude/longitude only |
| [Open-Meteo Geocoding API](https://open-meteo.com) | Convert city name to coordinates | City name you enter |

No other third-party services receive any data. No data brokers, ad networks, or analytics platforms are used.

---

## Data Storage

| Data | Storage | Scope |
|---|---|---|
| Weather location (coordinates) | `chrome.storage.local` | Your device only |
| Schedule view presets | `chrome.storage.sync` | Synced across your Chrome devices via Google |

You can delete all stored data at any time by removing the extension from Chrome, or by clearing extension storage in Chrome Settings → Privacy and Security → Site Settings.

---

## Children's Privacy

This extension is not directed at children under 13 and does not knowingly collect data from children.

---

## Changes

If this policy changes materially, the extension version number will be incremented and the change will be noted in the Chrome Web Store update changelog.

---

## Contact

Questions about this privacy policy?
Email: joelfriedrichdev+jobberpp@gmail.com
