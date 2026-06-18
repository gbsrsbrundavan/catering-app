# GB SRS Brundavan — Catering Order Tracker

A real-time catering order management web app built for **GB SRS Brundavan** (Registered Charity No. 1150660), Cowley, UB8 2DZ.

Built as a Progressive Web App (PWA) — installable on iPhone and Android directly from the browser. No app store required.

---

## Live App

Hosted on **GitHub Pages** | Database on **Supabase** (real-time sync)

---

## Access

| Role | How to access | PIN |
|------|--------------|-----|
| Volunteer | Open app → tap Volunteer | 0660 |
| Admin | Open app → tap Admin | Set on first login |

**Forgot admin PIN?** Use the reset passphrase on the login screen.

---

## Features

- 📅 Full year calendar — add orders to any date
- 📋 Detailed order cards — devotee name, event, portions, time, venue, menu, volunteers, quote price, notes
- 👥 Volunteer roster — managed by admin, shown on every order
- 🏛️ Venue manager — add/delete custom venues with addresses
- ✅ Order status — Confirmed / Tentative / Cancelled
- ✏️ Edit and delete with mandatory reason capture
- 🕓 Change history log per order
- 📊 Summary bar — confirmed, tentative, total quoted (£)
- 📆 Per-date breakdown — orders, portions and quoted value per day
- 🔔 In-app notifications — bell badge alerts when orders are added, updated or deleted
- 🔒 Two-PIN security — separate PIN for volunteers and admin
- 🌐 Real-time sync — all devices update live via Supabase Realtime
- 📱 PWA — installs as a home screen app on iPhone and Android

---

## Tech Stack

| Layer | Technology | Cost |
|-------|-----------|------|
| Hosting | GitHub Pages | Free |
| Database | Supabase (PostgreSQL) | Free tier |
| Real-time | Supabase Realtime | Free tier |
| Frontend | Vanilla HTML/CSS/JS | — |
| Icons | Tabler Icons | Free |
| Fonts | Inter (Google Fonts) | Free |

---

## Database Tables (Supabase)

### `orders`
| Column | Type | Description |
|--------|------|-------------|
| id | uuid | Primary key |
| date_id | text | Calendar date (YYYY-MM-DD) |
| devotee_name | text | Name of the devotee |
| client | text | Event / occasion name |
| portions | integer | Number of portions |
| time_slot | text | Serving time |
| menu | text | Menu items |
| contact | text | Contact person and phone |
| volunteers | text[] | Assigned volunteer names |
| venue_type | text | temple / devotee / venue ID / __other__ |
| venue_other | text | Free-text venue (if Other selected) |
| order_status | text | confirmed / tentative / cancelled |
| quote_price | numeric | Quoted price in GBP |
| notes | text | Additional notes and dietary info |
| created_at | timestamptz | Timestamp |

### `volunteers`
| Column | Type | Description |
|--------|------|-------------|
| id | uuid | Primary key |
| name | text | Volunteer name (unique) |
| created_at | timestamptz | Timestamp |

### `venues`
| Column | Type | Description |
|--------|------|-------------|
| id | uuid | Primary key |
| name | text | Venue name |
| address | text | Venue address (optional) |
| created_at | timestamptz | Timestamp |

### `order_changes`
| Column | Type | Description |
|--------|------|-------------|
| id | uuid | Primary key |
| order_id | uuid | Reference to order |
| order_client | text | Order name snapshot |
| order_date | text | Order date snapshot |
| action | text | edited / deleted |
| reason | text | Reason captured from admin |
| changed_at | timestamptz | Timestamp |

---

## Files

| File | Purpose |
|------|---------|
| `index.html` | Full app — all HTML, CSS and JavaScript |
| `manifest.json` | PWA manifest — app name, icon, theme colour |
| `sw.js` | Service worker — offline caching |
| `icon-192.png` | App icon (192×192) |
| `icon-512.png` | App icon (512×512) |
| `README.md` | This file |

---

## Installing as a Phone App

### iPhone (Safari only)
1. Open the app URL in **Safari**
2. Tap the **Share button** (□↑) at the bottom
3. Tap **"Add to Home Screen"**
4. Tap **Add**

### Android (Chrome)
1. Open the app URL in **Chrome**
2. Tap the **three dots menu** (⋮)
3. Tap **"Add to Home screen"**
4. Tap **Add**

---

## Updating the App

1. Edit `index.html` (or other files) locally
2. Go to your GitHub repository
3. Click **"Add file" → "Upload files"**
4. Upload the updated file(s)
5. Click **"Commit changes"**
6. Wait ~30 seconds — GitHub Pages rebuilds automatically
7. Hard refresh the app URL (**Ctrl+Shift+R** / **Cmd+Shift+R**)

---

## Changelog

---

### v1.0 — Initial release
- Basic catering order tracker with fixed dates (27 Jun, 28 Jun, 1 Jul, 11 Jul, 12 Jul)
- Volunteer view and Admin view
- Order fields: client, portions, time, menu, contact, volunteers, notes, status
- Admin PIN login (4-digit)
- Local storage (no database)

---

### v1.1 — Real-time sync via Supabase
- Replaced local storage with Supabase PostgreSQL database
- Real-time sync across all devices using Supabase Realtime
- Live connection indicator (green/amber dot)
- Supabase keys baked into HTML for zero-setup deployment

---

### v1.2 — New fields and venue support
- Added **Devotee name** field
- Added **Venue** field — Temple (Cowley), Devotee's house, Other (free text)
- Added **Order status** — Confirmed / Tentative / Cancelled (replacing old Pending)
- Added **Notes and other details** field
- Volunteer selection changed from comma-separated text to checkbox grid

---

### v1.3 — Full calendar navigation
- Replaced fixed date chips with a **full month calendar**
- Navigate month by month across the entire year
- Colour-coded dots on calendar dates — green (confirmed), amber (tentative), red (cancelled)
- **Today** button to jump back to current date
- Admin can add orders to any date by tapping first then clicking Add order

---

### v1.4 — Admin security and volunteer roster
- **Two-PIN security** — separate Volunteer PIN (0660) and Admin PIN
- Role selection screen on app open — Volunteer or Admin
- Admin-managed **Volunteer roster** — add/remove volunteers from a central list
- Volunteer checkboxes in order form pulled from roster
- **Forgot PIN** flow with reset passphrase (`brundavan2025`)
- Session persistence — stays logged in within same browser session
- Admin logout returns to role selection screen

---

### v1.5 — Venue manager
- **Venue manager** in Admin area — add and delete venues with name and address
- Venues stored in Supabase `venues` table with real-time sync
- Order form venue dropdown dynamically populated from venue roster
- Fixed venue options: Temple (Cowley) and Devotee's house always available
- Other / unlisted option with free-text field for one-off venues
- Venue name shown as badge on every order card

---

### v1.6 — Edit and delete with reason capture
- Edit and delete orders now require a **mandatory reason** before proceeding
- Reason dropdown with preset options for edits and deletions
- Optional free-text field for additional context
- All changes logged to `order_changes` table in Supabase
- **History button** on each order card — shows full timestamped change log
- Change log shows action (edited/deleted), reason, and timestamp

---

### v1.7 — Quote price per order
- Added **Quote price (£)** field to order form
- Quote price shown on every order card
- Summary bar updated — **Total quoted (£)** replaces Total portions
- Quote price stored as `numeric(10,2)` in Supabase

---

### v1.8 — Per-date summary breakdown
- Summary bar now shows global totals (Confirmed, Tentative, Total quoted)
- New **By date** breakdown — horizontally scrollable cards below summary
- Each date card shows: number of orders, total portions, total quoted (£), status badges
- Tapping a date card navigates calendar to that date
- Active date card highlighted in purple
- Breakdown only shown when orders exist

---

### v1.9 — Volunteer PIN and pre-set access
- Volunteer PIN pre-set to **0660** — no setup needed for volunteers
- PIN stored in browser localStorage per device
- First-time admin login prompts PIN creation
- Volunteer session persists within browser session

---

### v1.10 — PWA (Progressive Web App)
- App installable as home screen icon on **iPhone and Android**
- Added `manifest.json` — app name, theme colour (#5C4EAD), display mode standalone
- Added `sw.js` — service worker for offline caching of app shell
- Static assets cached on install; Supabase API calls always go to network
- Safe area padding for iPhone notch
- App icon generated at 192×192 and 512×512 (purple with bowl motif)
- Theme colour applied to browser chrome on Android

---

### v1.11 — In-app notifications
- **Bell icon** in top bar with red unread badge count
- Notifications generated automatically via Supabase Realtime when:
  - A new order is added
  - An existing order is updated
  - An order is deleted
- Slide-down notification panel — unread items highlighted in purple
- Tapping a notification jumps calendar to the relevant date
- **Mark all read** button clears badge
- Notifications stored per device in localStorage (up to 50 entries)
- Panel closes when tapping outside

---

### v1.12 — Volunteer display fix
- Fixed double-fire bug in volunteer checkbox toggle (label + onclick conflict)
- Volunteer checkboxes rebuilt with indexed IDs — reliable single-fire toggle
- Supabase null array normalised to `[]` on order load
- Volunteers section always visible on order cards — shows "No volunteers assigned yet" when empty
- Volunteer tags restyled in purple accent colour for visibility

---
