# ✟ NSBC Communion Delivery Dashboard

A mobile-first, shareable web dashboard for managing monthly communion delivery assignments at **New Salem Baptist Church** (Columbus, Ohio). Upload an Excel spreadsheet or photo of the communion list — the dashboard automatically parses, groups by deacon team, and generates a live page with Google Maps navigation and tap-to-call links that can be shared with any deacon via a single URL.

![Dashboard Preview](docs/preview.png)

---

## The Problem

Every month, church administrators create an Excel spreadsheet listing homebound members who need communion delivered. Deacon teams are assigned visits, but distributing the list means printing paper copies or emailing a spreadsheet that's hard to use on a phone — especially when a deacon is driving between stops and needs quick access to an address, phone number, or navigation directions.

## The Solution

**One HTML file. No server. No app install. No accounts.**

1. Open the dashboard in any browser
2. Upload the monthly Excel spreadsheet (or a screenshot of it)
3. The dashboard renders instantly — grouped by deacon team with full details
4. Share the URL — it contains the entire dataset encoded in the link
5. Deacons open the link on their phones and get:
   - **Tap-to-Navigate** → opens Google Maps with turn-by-turn directions
   - **Tap-to-Call** → dials the member or point of contact directly
   - **Team filtering** → sticky nav bar to jump to their specific assignment
   - **Print-ready** layout for those who still want paper

---

## Features

### 📊 Smart Excel Parsing
- Auto-detects header row and maps columns by name (First Name, Last Name, Address, City, State, Zip, Phone, POC, Deacon Team, Notes)
- Handles merged cells, multi-line cell content, semicolon-delimited addresses, and facility names
- Parses the "Deacon Teams On Deck" and "Unavailable" sections at the bottom of the spreadsheet
- Extracts the service date from the spreadsheet header automatically
- Auto-corrects known spelling issues (e.g., "Marshell" → "Marshall")

### 📸 Image Upload (OCR)
- Upload a photo or screenshot of the spreadsheet instead of the Excel file
- Uses [Tesseract.js](https://github.com/naptha/tesseract.js) for in-browser OCR
- Best-effort parsing — Excel upload is recommended for full accuracy

### 🔗 Shareable Links (No Server Required)
- After upload, the browser URL updates with a `#data=` hash containing the full dataset (base64-encoded JSON)
- Anyone who opens that URL sees the complete dashboard — **no upload needed on their end**
- Works via text message, email, AirDrop, or any link-sharing method
- Typical payload is ~5KB — well within URL limits for all modern browsers and messaging apps

### 📱 Mobile-First Design
- Responsive card layout optimized for phone screens
- **Tap-to-Call** buttons for every phone number (member, facility, point of contact)
- **Navigate** buttons that open Google Maps with the full address
- Sticky team navigation bar for quick access
- Fixed bottom action bar on mobile (Share, Print, Upload New)
- Native share sheet integration on iOS/Android
- Safe area support for notched devices

### 🖨️ Print-Ready
- Clean print stylesheet hides all interactive elements
- Cards avoid page breaks
- Works with any browser's print dialog or "Save as PDF"

### ✟ Church-Branded Theme
- Royal purple and gold color scheme inspired by [newsalemcares.com](https://newsalemcares.com)
- Gold Christian cross with radial glow in the header
- Cormorant Garamond serif headings with DM Sans body text
- Subtle cross-pattern texture overlay
- Entrance animations for a polished experience

---

## Getting Started

### Quick Start (Local)

1. Download `NSBC_Communion_Delivery.html`
2. Open it in any modern browser (Chrome, Safari, Firefox, Edge)
3. Upload your Excel spreadsheet (`.xlsx`, `.xls`, or `.csv`)
4. Done — the dashboard renders with all data

### Hosting for Shareable Links

For the shareable URL feature to work, the HTML file needs to be hosted at an accessible URL. Options:

| Host | Cost | Setup Time | URL Format |
|------|------|------------|------------|
| **GitHub Pages** | Free | 5 min | `username.github.io/nsbc-communion/` |
| **Netlify Drop** | Free | 30 sec | `random-name.netlify.app` |
| **Tiiny.host** | Free | 30 sec | `your-name.tiiny.site` |
| **Church website** | — | Varies | `newsalemcares.com/communion/` |
| **Google Drive** | Free | 2 min | Forces download (not ideal) |

#### GitHub Pages (Recommended)

```bash
# 1. Create a repository
git init nsbc-communion
cd nsbc-communion

# 2. Add the HTML file
cp /path/to/NSBC_Communion_Delivery.html index.html

# 3. Push to GitHub
git add .
git commit -m "Initial communion delivery dashboard"
git remote add origin https://github.com/YOUR_USERNAME/nsbc-communion.git
git push -u origin main

# 4. Enable GitHub Pages
# Go to repo Settings → Pages → Source: main branch → Save
# Your dashboard is live at https://YOUR_USERNAME.github.io/nsbc-communion/
```

#### Netlify Drop (Fastest)

1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag the HTML file onto the page
3. Get your shareable URL instantly

---

## Spreadsheet Format

The dashboard expects an Excel spreadsheet with this structure:

### Header Rows (Rows 1–4, merged cells)
```
Row 1: New Salem Baptist Church - Communion Delivery
Row 2: 2956 Cleveland Avenue
Row 3: Columbus, Ohio 43224
Row 4: Sunday, March 1, 2026    ← service date (auto-detected)
```

### Column Headers (Row 5)
| Column | Header | Required |
|--------|--------|----------|
| A | First Name | ✅ |
| B | Last Name | ✅ |
| C | Address | ✅ |
| D | City | ✅ |
| E | State | ✅ |
| F | Zip | ✅ |
| G | Phone Number | Recommended |
| H | Point of Contact First Name | Optional |
| I | Point of Contact Last Name | Optional |
| J | Point of Contact Phone Number | Optional |
| K | Point of Contact Email Address | Optional |
| L | Deacon(s) Team Assigned | ✅ |
| M | Notes | Optional |

### Data Rows (Row 6+)
- One member per row
- Address field can include facility names, room numbers, etc.
- Phone fields can contain multiple numbers separated by newlines
- Deacon team column uses format: `Deacons [Name] and [Name]`

### On Deck / Unavailable Section (After data rows)
```
Row N:   Deacon Teams On Deck
Row N+1: [empty or team names]
Row N+2: Unavailable
Row N+3: A. Hill
Row N+4: D. Cade
```

---

## How Sharing Works

```
┌─────────────────────────────────────────────────────┐
│  ADMINISTRATOR                                       │
│                                                       │
│  1. Opens hosted dashboard URL                        │
│  2. Uploads monthly Excel spreadsheet                 │
│  3. Dashboard renders with all data                   │
│  4. URL auto-updates: site.com/#data=eyJtZW1i...     │
│  5. Clicks "Share Dashboard" button                   │
│                                                       │
│         ┌──────────────────────────┐                  │
│         │  📱 Native Share Sheet   │                  │
│         │  • Text Message          │                  │
│         │  • Email                 │                  │
│         │  • AirDrop               │                  │
│         │  • Copy Link             │                  │
│         └──────────────────────────┘                  │
│                      │                                │
└──────────────────────┼────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│  DEACONS (on their phones)                           │
│                                                       │
│  1. Tap the shared link                               │
│  2. Dashboard loads instantly (data is in the URL)    │
│  3. Find their team in the sticky nav bar             │
│  4. Tap "Navigate" → Google Maps directions           │
│  5. Tap phone number → calls the member               │
│                                                       │
│  No upload needed. No app needed. No account needed.  │
└─────────────────────────────────────────────────────┘
```

---

## Technology

This is a **single HTML file** with zero build steps and zero server dependencies.

| Component | Technology |
|-----------|-----------|
| UI Framework | Vanilla HTML/CSS/JS |
| Excel Parsing | [SheetJS (xlsx)](https://sheetjs.com/) via CDN |
| Image OCR | [Tesseract.js v5](https://github.com/naptha/tesseract.js) via CDN |
| Fonts | Google Fonts (Cormorant Garamond + DM Sans) |
| Maps | Google Maps Search URLs |
| Phone Links | `tel:` URI scheme |
| Data Sharing | Base64-encoded JSON in URL hash fragment |
| Hosting | Any static file host (or local file) |

**No npm. No build. No backend. No database. No API keys.**

---

## Browser Support

| Browser | Desktop | Mobile |
|---------|---------|--------|
| Chrome | ✅ | ✅ |
| Safari | ✅ | ✅ (iOS) |
| Firefox | ✅ | ✅ |
| Edge | ✅ | ✅ |
| Samsung Internet | — | ✅ |

---

## Customization

### Changing the Church Name / Address
Edit the HTML header section — search for "New Salem Baptist Church" and update the text and contact info.

### Changing the Color Theme
All colors are defined as CSS variables at the top of the `<style>` block. Key variables:

```css
:root {
  --purple-deep: #2a1648;    /* Darkest background */
  --purple-dark: #3b2060;    /* Card backgrounds */
  --purple: #4e2d78;         /* Accent elements */
  --purple-mid: #6a3f9e;     /* Hover states */
  --gold: #d4a843;           /* Primary accent */
  --gold-bright: #ebc95e;    /* Hover accent */
  --bg: #160e24;             /* Page background */
  --bg-card: #231840;        /* Card background */
}
```

### Adding New Column Mappings
The `mapColumns()` function in the JavaScript section handles header-to-field mapping. Add new patterns to support additional column headers from different spreadsheet formats.

---

## Project Background

This project was built to solve a real operational need at New Salem Baptist Church in Columbus, Ohio. The church's deacon ministry coordinates monthly communion delivery to homebound members across the Columbus metro area. The previous workflow involved printing Excel spreadsheets — this dashboard digitizes the process while keeping it simple enough for anyone to use.

Built with [Claude AI](https://claude.ai) by Anthropic.

---

## License

MIT License — free to use, modify, and distribute. Built for the glory of God and the service of His people.

If your church would benefit from a similar tool, feel free to fork and customize.
