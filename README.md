# 📊 Claude Usage Tracker

A macOS menu bar app that monitors your [Claude.ai](https://claude.ai) daily and weekly usage limits in real time — so you never get caught off guard by hitting your limit mid-conversation.

![macOS Menu Bar](https://img.shields.io/badge/macOS-Menu%20Bar%20App-blue)
![Version](https://img.shields.io/badge/version-1.2.1-orange)
![License](https://img.shields.io/badge/license-MIT-green)
![Platform](https://img.shields.io/badge/platform-macOS-lightgrey)

---

## Features

- 📅 **Daily usage** — see how many messages you've used today and what % of your limit
- 📊 **Weekly usage** — track your weekly consumption at a glance
- ⏰ **Reset countdowns** — know exactly when your daily and weekly limits reset
- 🔄 **Auto-refresh** — checks your usage every 5 minutes automatically
- 🖥️ **Menu bar icon** — lives quietly in your menu bar, out of the way
- 🔔 **Warning alerts** — notifies you when you're approaching your limits

---

## Screenshot

```
Menu Bar:  📊 D:12% W:34%

Dropdown:
  Daily: 60/500 (12%)
  Weekly: 510/1500 (34%)
  ─────────────────────
  Daily resets in: 3 hr 22 min
  Weekly resets: Thu 2:00 PM
  ─────────────────────
  Last updated: 2:45:00 PM
  ─────────────────────
  Open Settings
  Refresh Now
  ─────────────────────
  Quit
```

---

## Requirements

- macOS 12 or later
- [Brave Browser](https://brave.com) or [Google Chrome](https://www.google.com/chrome/) installed
- A [Claude.ai](https://claude.ai) account (Pro, Max, Team, or Enterprise)

> **Note:** This app works by scraping your Claude.ai settings page. It requires a browser to stay running in the background. An official Anthropic API for usage data does not currently exist.

---

## Installation

### Option A: Download the DMG (easiest)

1. Go to the [Releases](../../releases) page
2. Download the latest `Claude Usage Tracker-x.x.x.dmg`
3. Open the DMG and drag the app to your **Applications** folder
4. Launch **Claude Usage Tracker** from Applications

> **First launch security warning:** macOS may say the app "cannot be opened because the developer cannot be verified." To bypass this, run this one-time command in Terminal:
> ```bash
> xattr -cr "/Applications/Claude Usage Tracker.app"
> ```
> Then launch the app normally. You only need to do this once.

### Option B: Build from source

```bash
# Clone the repo
git clone https://github.com/yourusername/claude-usage-tracker.git
cd claude-usage-tracker

# Install dependencies
npm install

# Run in development mode
npm start

# Build the DMG
npm run build
```

---

## First Time Setup

1. **Launch the app** — you'll see the Claude Usage Tracker window appear
2. **Click the Settings tab**
3. **Click "Initialize Browser & Login"**
   - A browser window will open and navigate to Claude.ai
   - Log in to your Claude.ai account in that window
   - Keep the browser window open (you can minimize it)
4. **Click the Dashboard tab**
5. **Click "Start Tracking"**
6. ✅ Done! Your usage will now appear in the menu bar

---

## How It Works

Since Anthropic doesn't provide a public API for usage data, this app:

1. Opens a separate browser profile (won't affect your regular browsing)
2. Navigates to your Claude.ai Settings → Usage page
3. Reads the usage percentages and reset times from the page
4. Displays them in your menu bar and updates every 5 minutes

Your credentials are never stored — you log in manually each time via the browser window.

---

## Troubleshooting

| Problem | Solution |
|--------|----------|
| "App cannot be opened" security warning | Run `xattr -cr "/Applications/Claude Usage Tracker.app"` in Terminal |
| Browser window closes immediately | Click "Initialize Browser & Login" again |
| Usage shows 0% | Click "Refresh Now" from the menu bar icon |
| App not in menu bar | Click the Electron icon in the Dock |
| "Could not find browser" error | Install [Brave](https://brave.com) or [Chrome](https://www.google.com/chrome/) |
| Detached frame error | Click "Refresh Now" — app will auto-recover |
| Stats stop updating | Restart the app with "Quit" then relaunch |

---

## Limitations

- Requires Brave or Chrome to be installed
- The browser window must remain open in the background
- May break if Anthropic changes the Claude.ai settings page layout
- Usage counts are estimated from percentages (Claude.ai only shows %)
- Not affiliated with or endorsed by Anthropic

---

## Contributing

Pull requests welcome! Key files:

| File | Purpose |
|------|---------|
| `main.js` | Electron main process, menu bar tray |
| `renderer.js` | App UI logic |
| `scraper.js` | Puppeteer browser automation |
| `index.html` | App UI layout and styles |

---

## License

MIT — use freely, modify as you wish.

---

## Disclaimer

This is an unofficial, community-built tool. It is not affiliated with, endorsed by, or supported by Anthropic. Use in accordance with [Claude.ai's Terms of Service](https://www.anthropic.com/legal/consumer-terms).

If you find this useful, consider requesting an official usage API from Anthropic via the feedback button in Claude.ai! 🙏

---

## Changelog

### v1.2.1
- ⏱️ Added "Next update in: Xm Xs" countdown to menu bar dropdown

### v1.2.0
- 🛡️ Auto-recovery from detached frame errors (no more manual restart needed)
- 🔐 Session expiry detection — app alerts you to re-login instead of silently failing
- 💥 Browser crash recovery — automatically restarts browser if it crashes
- 🚫 Concurrent scrape prevention — won't run overlapping scrapes
- 🌐 Network error detection with friendly messages
- 🧹 Memory leak prevention — properly closes duplicate tabs
- ✅ Better error messages with actionable instructions

### v1.1.0
- ✅ Added daily and weekly percentage to menu bar dropdown
- ✅ Fixed reset times to show actual values from Claude.ai (not estimated)
- ✅ Fixed multiple browser tabs accumulating over time
- ✅ Fixed detached frame error after long running sessions
- ✅ Removed developer console window opening on startup
- ✅ Improved browser compatibility (Brave + Chrome)
- ✅ Added separate browser profile so main browser session is unaffected
- ✅ Added macOS security bypass instructions

### v1.0.0
- 🎉 Initial release
- Daily and weekly usage tracking
- Menu bar icon with usage stats
- Auto-refresh every 5 minutes
- Login via Brave or Chrome browser
