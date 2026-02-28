# ⚔️ TORN // Inactive Hunter

> **A fast, mobile-friendly attack dashboard for Torn City — scan inactive players across multiple lists, check live status, and strike fast.**

![HTML](https://img.shields.io/badge/Built_With-HTML%2FJS-ff3c3c?style=flat-square)
![API](https://img.shields.io/badge/Torn_API-v1-ff7b00?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-00e676?style=flat-square)
![No Server](https://img.shields.io/badge/No_Server-Required-29b6f6?style=flat-square)
![Mobile](https://img.shields.io/badge/Mobile-Friendly-00e676?style=flat-square)

---

## 📸 Preview

**Desktop — Table View**
```
┌─────────────────────────────────────────────────────────────────────────┐
│  TORN // INACTIVE HUNTER                                                │
│  MY INACTIVE LIST (UNDER 500 STATS)  ·  125 TARGETS                    │
├─────────────────────────────────────────────────────────────────────────┤
│  API KEY // [••••••••]  [— Select list ▾]           [ ▶ SCAN ]          │
├──────┬─────────────┬─────────┬─────┬────────────────────┬──────────────┤
│  #   │ NAME        │ ID      │ LVL │ STATUS             │ ATTACK       │
├──────┼─────────────┼─────────┼─────┼────────────────────┼──────────────┤
│  1   │ maverick    │ 522960  │ 31  │ ✅ OKAY             │ ⚔ ATTACK    │
│  2   │ OwlByNite   │ 1046495 │ 29  │ 🏥 HOSPITAL [2m]   │ ⚔ ATTACK    │
│  3   │ Dragon      │ 234429  │ 27  │ 🏥 HOSPITAL [45m]  │   (locked)  │
│  4   │ babymolly   │ 879148  │ 27  │ ⚑  JAIL [1h 20m]  │   (locked)  │
└──────┴─────────────┴─────────┴─────┴────────────────────┴──────────────┘
```

**Mobile — Card View**
```
┌──────────────────────────────────┐
│ maverick1972          [ ⚔ ATK ] │
│ #1 · ID: 522960                  │
│ ✅ OKAY                          │
│ LVL 31  STATS 396  1451d ago     │
├──────────────────────────────────┤
│ OwlByNite             [  ATK  ] │
│ #2 · ID: 1046495                 │
│ 🏥 HOSPITAL  [2m 14s]            │
│ LVL 29  STATS 450  890d ago      │
└──────────────────────────────────┘
          ┌───────────────────┐
          │  ⚔ SCAN & HUNT   │  ← sticky bottom button
          └───────────────────┘
```

---

## ✨ Features

- ⚡ **Blazing fast scans** — all requests fire simultaneously via `Promise.all`, no batching delays
- 📋 **Multi-list support** — manage multiple target lists in one `data.json`, switch via dropdown
- 📱 **Mobile-first card layout** — no horizontal scrolling, big thumb-friendly attack buttons, sticky scan button
- 🖥️ **Desktop table view** — full sortable table on wider screens
- 🎯 **Smart auto-sort** — players ranked by attack priority after every scan:
  1. `OKAY` — attackable right now, always first
  2. `HOSPITAL` — sorted by **shortest time remaining** (ascending)
  3. `JAIL` — sorted by **shortest time remaining** (ascending)
  4. `TRAVELING` — listed after
  5. Unknown / errors — bottom
- ⏱️ **Live countdown timers** — ticks every second, auto-flips to OKAY when time expires
- ⚔️ **Direct attack links** — opens Torn attack page instantly, disabled while target is unavailable
- 🔍 **Search + filter pills** — filter by name, ID, or status
- 📊 **Live stats bar** — count of Okay / Hospital / Jail / Traveling at a glance
- 💾 **Remembers everything** — API key and last selected list saved in `localStorage`
- ⏳ **30s cooldown** — prevents accidental API spam after each scan
- 🔒 **Privacy first** — API key never leaves your browser

---

## 🚀 Quick Start

### Option 1 — Netlify Drop (Easiest, 10 seconds)
1. Download both `index.html` and `data.json`
2. Go to **[app.netlify.com/drop](https://app.netlify.com/drop)**
3. Select **both files** and drag & drop them together
4. 🎉 Live instantly — share the URL

### Option 2 — GitHub Pages (Recommended)
```bash
git clone https://github.com/YOUR_USERNAME/torn-inactive-hunter
cd torn-inactive-hunter
git add index.html data.json
git commit -m "initial deploy"
git push
```
Go to **Settings → Pages → Branch: main → Save**

Live at: `https://YOUR_USERNAME.github.io/torn-inactive-hunter`

> To update your lists later, just edit `data.json` and push — no need to touch `index.html`.

### Option 3 — Run Locally
Use a simple local server (required for `data.json` to load):
```bash
python3 -m http.server 8080
# open http://localhost:8080
```
> ⚠️ Double-clicking `index.html` directly won't work — the browser blocks local file fetches.

---

## 🔑 API Key Setup

1. Log in to **[Torn City](https://www.torn.com)**
2. Go to **Settings → API Key**
3. Create a key with **`Public` access level** (minimum required)
4. Paste it into the dashboard — saved automatically for next visit

> ⚠️ Use a `Public` key only. This tool uses the `basic` selection which needs no elevated permissions.

---

## 📁 File Structure

```
torn-inactive-hunter/
├── index.html    ← dashboard UI  (never needs editing)
└── data.json     ← your target lists  (edit this freely)
```

---

## 🗂️ Managing Target Lists (`data.json`)

Everything lives in `data.json`. The format is a simple JSON object — each key is a list name, each value is a player array.

### Full example

```json
{
  "My Inactive List": [
    {
      "name": "maverick1972",
      "id": "522960",
      "lvl": "31",
      "total": "396",
      "str": "106",
      "def": "107",
      "spd": "99",
      "dex": "84"
    },
    {
      "name": "OwlByNite",
      "id": "1046495",
      "lvl": "29",
      "total": "450",
      "str": "141",
      "def": "104",
      "spd": "101",
      "dex": "104"
    }
  ],
  "High Priority Targets": [
    { "name": "somePlayer", "id": "123456" }
  ]
}
```

> **Minimum required:** `name` and `id`. All stat fields (`lvl`, `total`, `str`, `def`, `spd`, `dex`) are optional but displayed on mobile cards.

### Common tasks

| Task | How |
|------|-----|
| **Add a player** | Append `{ "name": "...", "id": "..." }` to the array |
| **Remove a player** | Delete their `{ }` block |
| **Add a new list** | Add a new top-level key with a player array |
| **Rename a list** | Change the key string — updates in dropdown automatically |
| **Reorder lists** | Rearrange key blocks — dropdown follows JSON order |
| **Add stat columns** | Include `lvl`, `total`, `str`, `def`, `spd`, `dex` fields |

---

## 📡 How It Works

```
Browser loads index.html
    │
    ├── Fetches data.json → populates list dropdown
    │
    ├── User selects list + pastes API key → clicks SCAN
    │
    ├── Fires ALL player requests simultaneously (Promise.all):
    │       GET https://api.torn.com/user/{ID}?selections=basic&key={KEY}
    │
    ├── Extracts per player:
    │       ├── level
    │       ├── status.state        (Okay / Hospital / Jail / Traveling)
    │       ├── status.description  (e.g. "In hospital for 15 mins")
    │       ├── status.until        (unix timestamp)
    │       └── last_action.relative
    │
    ├── Sorts: Okay → Hospital (shortest first) → Jail (shortest first) → Travel
    │
    ├── Renders cards (mobile) + table rows (desktop) in one pass
    │
    └── 1s tick updates timer text only — flips badge to OKAY when expired
```

---

## 📋 Changelog

### v1.4 — JSON-Driven Lists + Mobile-First UI
- Player data moved out of `index.html` into external `data.json`
- Multi-list support with dropdown — switch lists without rescanning
- Remembers last selected list via `localStorage`
- Mobile: card layout replaces table — no horizontal scrolling
- Mobile: sticky `⚔ SCAN & HUNT` button fixed at bottom of screen
- Mobile: horizontally scrollable filter pills
- Mobile: full-width search box, large tap targets
- Desktop: inline list dropdown + scan button in API bar
- Stats bar responsive grid (5-col on mobile, inline on desktop)

### v1.3 — Performance Rewrite
- Replaced batched fetching (5 + 600ms delay) with `Promise.all` — all requests fire at once
- Switched API selection from `profile` to `basic` (lighter, faster)
- Table renders once after all results resolve — no per-request re-renders
- Live tick-down updates only timer `span` text — no DOM re-renders
- API key auto-saved to `localStorage`
- 30s cooldown button after each scan

### v1.2 — Smart Auto-Sort
- Auto-sort by attack priority after every scan
- Hospital/Jail sorted by shortest remaining time (ascending)
- Live countdown timers on status badges

### v1.1 — Initial Release
- 125 pre-loaded targets (hardcoded)
- Torn API integration, status badges, attack buttons
- Search, filter, column sorting, progress bar

---

## 🛠️ Tech Stack

| Component | Details |
|-----------|---------|
| Frontend  | Vanilla HTML / CSS / JS — zero frameworks, zero build step |
| Fonts     | [Orbitron](https://fonts.google.com/specimen/Orbitron) + [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) |
| Data      | External `data.json` — edit without touching the UI |
| API       | [Torn City Public API v1](https://www.torn.com/api.html) — `basic` selection |
| Hosting   | Any static host — Netlify, GitHub Pages, Vercel, or `python3 -m http.server` |

---

## ⚖️ Disclaimer

Unofficial fan project, not affiliated with or endorsed by Torn City or Torn Ltd. Use responsibly and in accordance with [Torn's Terms of Service](https://www.torn.com/terms.php).

---

## 📄 License

MIT — do whatever you want with it.

---

<div align="center">
  <sub>Built for the Torn grind. Stay aggressive. ⚔️</sub>
</div>
