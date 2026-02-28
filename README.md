# ⚔️ TORN // Inactive Hunter

> **A sleek, single-file attack dashboard for Torn City — scan inactive players, check their status, and strike fast.**

![HTML](https://img.shields.io/badge/Built_With-HTML%2FJS-ff3c3c?style=flat-square)
![API](https://img.shields.io/badge/Torn_API-v1-ff7b00?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-00e676?style=flat-square)
![No Server](https://img.shields.io/badge/No_Server-Required-29b6f6?style=flat-square)

---

## 📸 Preview

```
┌─────────────────────────────────────────────────────────────────┐
│  TORN // INACTIVE HUNTER                                        │
│  INACTIVE PLAYER ATTACK DASHBOARD  |  125 TARGETS LOADED       │
├─────────────────────────────────────────────────────────────────┤
│  API KEY // [••••••••••••••••••]          [ ▶ SCAN ALL ]        │
├──────┬─────────────┬─────────┬─────┬──────────────────┬────────┤
│  #   │ NAME        │ ID      │ LVL │ STATUS           │ ACTION │
├──────┼─────────────┼─────────┼─────┼──────────────────┼────────┤
│  1   │ maverick    │ 522960  │ 31  │ ✅ OKAY           │ ATTACK │
│  2   │ OwlByNite   │ 1046495 │ 29  │ 🏥 HOSPITAL [2m] │ ATTACK │
│  3   │ Dragon      │ 234429  │ 27  │ 🏥 HOSPITAL [45m]│ ATTACK │
│  4   │ babymolly   │ 879148  │ 27  │ ⚑ JAIL [1h 20m] │ ATTACK │
└──────┴─────────────┴─────────┴─────┴──────────────────┴────────┘
```

---

## ✨ Features

- ⚡ **One-click scan** — fetches all 125 targets via Torn API simultaneously
- 🎯 **Smart auto-sort** — players ranked by attack priority automatically:
  1. `OKAY` — attackable right now, always at the top
  2. `HOSPITAL` — sorted by **shortest time remaining first**
  3. `JAIL` — sorted by **shortest time remaining first**
  4. `TRAVELING` — listed after
  5. Unknown / unloaded — at the bottom
- ⏱️ **Live countdown timers** — see exactly how long until a player is out of hospital or jail (e.g. `HOSPITAL [4m 32s]`)
- ⚔️ **One-click attack button** — opens Torn attack page directly for each player
- 🔍 **Search + filter** — filter by name/ID or status (Okay / Hospital / Jail / Traveling)
- 📊 **Stats bar** — live count of each status group as scan runs
- 🖥️ **Zero setup** — single `.html` file, no server, no install, no dependencies
- 🔒 **Privacy first** — your API key stays in your browser, never sent anywhere else

---

## 🚀 Quick Start

### Option 1 — Netlify Drop (Easiest, 10 seconds)
1. Download `index.html`
2. Go to **[app.netlify.com/drop](https://app.netlify.com/drop)**
3. Drag & drop the file
4. 🎉 Live instantly — share the URL with your faction

### Option 2 — GitHub Pages (Recommended for updates)
```bash
git clone https://github.com/YOUR_USERNAME/torn-inactive-hunter
cd torn-inactive-hunter
# Replace index.html with the latest version
git add .
git commit -m "update"
git push
```
Then go to **Settings → Pages → Branch: main → Save**
Your tool is live at `https://YOUR_USERNAME.github.io/torn-inactive-hunter`

### Option 3 — Run Locally
No server needed. Just double-click `index.html` and open in your browser.

---

## 🔑 API Key Setup

1. Log in to **[Torn City](https://www.torn.com)**
2. Go to **Settings → API Key**
3. Create a key with **`Public` access level** (minimum required)
4. Paste the key into the dashboard when scanning

> ⚠️ **Security tip:** Use a `Public` access key only — this tool only needs `profile` data. Never share your full-access key.

---

## 📡 How It Works

```
Your Browser
    │
    ├── Loads index.html (125 player IDs pre-loaded)
    │
    ├── On "SCAN ALL" click:
    │       └── Fetches each player via:
    │           GET https://api.torn.com/user/{ID}?selections=profile&key={YOUR_KEY}
    │
    ├── Extracts:
    │       ├── level
    │       ├── status.state        (Okay / Hospital / Jail / Traveling)
    │       ├── status.description  (e.g. "In hospital for 15 mins")
    │       ├── states.hospital_timestamp
    │       ├── states.jail_timestamp
    │       └── last_action.relative
    │
    └── Auto-sorts by priority + time remaining → renders table
```

Requests are batched **5 at a time** with a 600ms delay between batches to respect Torn's API rate limits.

---

## 🗂️ Player List

The dashboard comes pre-loaded with **125 inactive players** (under 500 battle stats). The list is embedded directly in `index.html` — to update it, edit the `PLAYERS` array in the `<script>` section:

```js
const PLAYERS = [
  { "name": "maverick1972", "id": 522960 },
  { "name": "OwlByNite",    "id": 1046495 },
  // ... add or remove players here
];
```

---

## 📋 Changelog

### v1.2 — Smart Auto-Sort
- Auto-sort by attack priority after every scan batch
- Hospital/Jail sorted by shortest time remaining (ascending)
- Live countdown timers on status badges
- Stores `hospitalUntil` and `jailUntil` timestamps from API

### v1.1 — Initial Release
- 125 pre-loaded targets
- Torn API integration with batch fetching
- Status badges, last active time, attack buttons
- Search, filter, column sorting
- Progress bar + stats counter

---

## 🛠️ Tech Stack

| Component | Details |
|-----------|---------|
| Frontend  | Vanilla HTML / CSS / JS — zero frameworks |
| Fonts     | [Orbitron](https://fonts.google.com/specimen/Orbitron) + [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) via Google Fonts |
| API       | [Torn City Public API v1](https://www.torn.com/api.html) |
| Hosting   | Any static host — Netlify, GitHub Pages, Vercel, or local |

---

## ⚖️ Disclaimer

This tool is an **unofficial fan project** and is not affiliated with or endorsed by Torn City or Torn Ltd. Use responsibly and in accordance with [Torn's Terms of Service](https://www.torn.com/terms.php). The developer is not responsible for any in-game consequences from using this tool.

---

## 📄 License

MIT — do whatever you want with it.

---

<div align="center">
  <sub>Built for the Torn grind. Stay aggressive. ⚔️</sub>
</div>
