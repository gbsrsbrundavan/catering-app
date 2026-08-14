# GB SRS Brundavan — Catering Order Tracker

A real-time catering order management web app built for **GB SRS Brundavan** (Registered Charity No. 1150660), 55 High Street, Cowley, Uxbridge, UB8 2DZ.

Built as a Progressive Web App (PWA) — installable on iPhone and Android directly from the browser. No app store required.

---

## Live App

**URL:** https://gbsrsbrundavan.github.io/catering-app

**Database:** Firebase Firestore (Google) — real-time sync, free tier, EU region

---

## Access

| Role | How to access | PIN |
|------|--------------|-----|
| Volunteer | Open app → tap Volunteer | 0660 |
| Admin | Open app → tap Admin | Set on first login |

**Forgot admin PIN?** Tap "Forgot PIN?" on the login screen and enter the reset passphrase.

---

## Features

- 📅 Full year calendar — add orders to any date in any month
- 📋 Detailed order cards — devotee name, event, portions, time, venue, menu, volunteers, quote price, notes
- 💰 Summary bar — confirmed count, tentative count, total quoted (£)
- 📊 60/40 split — volunteer share (60%) and Matha share (40%) of total quoted value
- 📆 Per-date breakdown — orders, portions and quoted value per day, grouped by month
- 👥 Volunteer roster — managed by admin, shown on every order card
- 🏛️ Venue manager — add/delete custom venues with addresses
- ✅ Order status — Confirmed / Tentative / Cancelled
- 🗺️ Venue types — Temple (Cowley), Devotee's house, custom venues, Other
- ✏️ Edit and delete with mandatory reason capture
- 🕓 Change history log per order — full audit trail
- 🔔 In-app notifications — bell badge alerts when orders are added, updated or deleted
- 🔒 Two-PIN security — separate PIN for volunteers and admin
- 🌐 Real-time sync — all devices update live via Firebase Realtime
- 📱 PWA — installs as home screen app on iPhone and Android
- 📥 CSV import — import orders, volunteers and venues from CSV (Data tools in Admin)
- 🍽️ Menu formatting — items display as clean bullet list on order cards

---

## Tech Stack

| Layer | Technology | Cost |
|-------|-----------|------|
| Hosting | GitHub Pages | Free |
| Database | Firebase Firestore (Google) | Free Spark plan |
| Real-time | Firebase onSnapshot listeners | Free |
| Frontend | Vanilla HTML / CSS / JavaScript | — |
| Icons | Tabler Icons (CDN) | Free |
| Fonts | Inter — Google Fonts | Free |

---

## Database Collections (Firebase Firestore)

### `orders`
| Field | Type | Description |
|-------|------|-------------|
| date_id | string | Calendar date (YYYY-MM-DD) |
| devotee_name | string | Name of the devotee |
| client | string | Event / occasion name |
| portions | number | Number of portions |
| time_slot | string | Serving time |
| menu | string | Menu items (newline or comma separated) |
| contact | string | Contact person and phone number |
| volunteers | array | Assigned volunteer names |
| venue_type | string | \_\_temple\_\_ / \_\_devotee\_\_ / venue ID / \_\_other\_\_ |
| venue_other | string | Free-text venue name (if Other selected) |
| order_status | string | confirmed / tentative / cancelled |
| quote_price | number | Quoted price in GBP |
| notes | string | Additional notes and dietary requirements |
| created_at | string | ISO timestamp |

### `volunteers`
| Field | Type | Description |
|-------|------|-------------|
| name | string | Volunteer name (unique) |
| created_at | string | ISO timestamp |

### `venues`
| Field | Type | Description |
|-------|------|-------------|
| name | string | Venue name |
| address | string | Venue address (optional) |
| created_at | string | ISO timestamp |

### `order_changes`
| Field | Type | Description |
|-------|------|-------------|
| order_id | string | Reference to order document ID |
| order_client | string | Order name snapshot |
| order_date | string | Order date snapshot |
| action | string | edited / deleted |
| reason | string | Reason captured from admin |
| changed_at | string | ISO timestamp |

---

## Files

| File | Purpose |
|------|---------|
| `index.html` | Full app — all HTML, CSS and JavaScript in one file |
| `manifest.json` | PWA manifest — app name, icon, theme colour |
| `sw.js` | Service worker — offline caching |
| `icon-192.png` | App icon (192×192 px) |
| `icon-512.png` | App icon (512×512 px) |
| `README.md` | This file |

---

## Installing as a Phone App

### iPhone (Safari only)
1. Open the app URL in **Safari** (must be Safari, not Chrome)
2. Tap the **Share button** (□↑) at the bottom of the screen
3. Tap **"Add to Home Screen"**
4. Tap **Add**
5. The app icon appears on your home screen

### Android (Chrome)
1. Open the app URL in **Chrome**
2. Tap the **three dots menu** (⋮) at the top right
3. Tap **"Add to Home screen"**
4. Tap **Add**
5. The app icon appears on your home screen

---

## Updating the App

1. Download the updated `index.html` (and any other changed files)
2. Go to your GitHub repository — **github.com/gbsrsbrundavan/catering-app**
3. Click **"Add file"** → **"Upload files"**
4. Drag the updated file(s) into the upload box
5. Click **"Commit changes"**
6. Wait ~30 seconds for GitHub Pages to rebuild
7. Hard refresh the app URL — **Ctrl+Shift+R** (desktop) or open in a new incognito window

---

## CSV Import (Data tools)

Admin area → scroll to bottom → click **"Data tools"** to expand.

### Orders CSV
Must include columns: `date_id, client, portions, time_slot, menu, contact, volunteers, venue_type, order_status, quote_price, notes, devotee_name`

- `date_id` must be in `YYYY-MM-DD` format
- `volunteers` can be a JSON array `["Name1","Name2"]` or semicolon-separated `Name1;Name2`
- Menu fields can span multiple lines (quoted fields supported)

### Volunteers CSV
Must include column: `name`

### Venues CSV
Must include column: `name` — `address` is optional

---

## Security Notes

| Item | Status |
|------|--------|
| Firebase API key | Restricted to gbsrsbrundavan.github.io in Google Cloud |
| GitHub repository | Public (API key domain-restricted so safe) |
| Firestore rules | Currently open — tighten with Firebase Auth when ready |
| Volunteer PIN | 0660 — share only with catering team |
| Admin PIN | Set by admin on first login — keep confidential |
| Reset passphrase | Keep confidential — share only with trustees |

---

## GDPR Notes (UK GDPR)

| Item | Detail |
|------|--------|
| Personal data held | Devotee name, contact number, volunteer names |
| Lawful basis | Legitimate interests (catering service delivery) |
| Data processor | Google Firebase (Google DPA applies) |
| Storage region | Firebase default — confirm EU region in Firebase console |
| Retention | Review and delete orders older than 12 months |
| Right to erasure | Delete individual orders via Admin → Delete |
| Data breach | Notify ICO within 72 hours if database compromised |

**Action required:** Sign Google/Firebase DPA at **firebase.google.com/terms**

---

## Changelog

### v1.0 — Initial release
- Basic catering order tracker with fixed dates
- Volunteer view and Admin view
- Order fields: client, portions, time, menu, contact, volunteers, notes, status
- Admin PIN login
- Local browser storage only

### v1.1 — Real-time sync via Supabase
- Replaced local storage with Supabase PostgreSQL database
- Real-time sync across all devices
- Live connection indicator

### v1.2 — New fields and venue support
- Added devotee name, venue type, order status (Confirmed/Tentative/Cancelled), notes field
- Volunteer selection changed to checkbox grid

### v1.3 — Full calendar navigation
- Fixed date chips replaced with full month calendar
- Navigate any month across the entire year
- Colour-coded dots on dates with orders
- Today button

### v1.4 — Admin security and volunteer roster
- Two-PIN security — separate volunteer PIN (0660) and admin PIN
- Role selection screen on app open
- Admin-managed volunteer roster
- Forgot PIN flow with reset passphrase

### v1.5 — Venue manager
- Venue manager in Admin — add/delete venues with name and address
- Venue dropdown in order form populated from venue roster
- Venue badge on order cards

### v1.6 — Edit and delete with reason capture
- Edit and delete orders require a mandatory reason
- Preset reason dropdowns for edits and deletions
- All changes logged to order_changes collection
- History button on each order card

### v1.7 — Quote price per order
- Quote price (£) field added to order form
- Quote price shown on order cards

### v1.8 — Per-date summary breakdown
- Summary bar with global totals
- By date breakdown — scrollable cards per date, grouped by month
- Tapping a date card navigates calendar

### v1.9 — Volunteer PIN pre-set
- Volunteer PIN pre-set to 0660
- First-time admin login prompts PIN creation

### v1.10 — PWA (Progressive Web App)
- Installable as home screen icon on iPhone and Android
- manifest.json and service worker added
- App icons generated at 192×192 and 512×512
- Offline caching of app shell

### v1.11 — In-app notifications
- Bell icon with unread badge count
- Notifications on order add, update, delete
- Slide-down notification panel
- Tap notification to jump to date
- Mark all read

### v1.12 — Volunteer display fix
- Fixed double-fire bug in volunteer checkbox toggle
- Supabase null array normalised on load
- Volunteers always visible on order cards

### v1.13 — Menu formatting
- Menu items display as formatted bullet list on order cards
- Supports comma-separated and newline-separated input

### v1.14 — By date breakdown fix
- Legacy date IDs filtered out
- Breakdown grouped by month with section headers
- Active date card auto-scrolls into view

### v1.15 — Security and GDPR assessment
- Full security audit documented
- UK GDPR compliance review completed
- Data register template produced
- Action plan documented

### v1.16 — Migrated to Firebase Firestore
- Replaced Supabase with Firebase Firestore (no domain restrictions)
- Full real-time sync via Firebase onSnapshot listeners
- CSV import tool — orders, volunteers, venues
- RFC 4180 compliant CSV parser — handles multiline quoted fields and JSON volunteer arrays
- CSV import moved to collapsible Data tools section in Admin
- 60/40 revenue split — volunteer share (60%) and Matha share (40%) shown in summary bar
- Firebase API key restricted to GitHub Pages domain in Google Cloud Console

---

## Support

For any issues or changes contact the GB SRS Brundavan admin team.

**Charity No.** 1150660 | **Address:** 55 High Street, Cowley, Uxbridge, UB8 2DZ | **Website:** gb-srsbrundavan.org
