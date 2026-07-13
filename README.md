# Internship Tracker

<img width="850" height="400" alt="image" src="https://github.com/user-attachments/assets/50e906e0-32a9-4ed4-9cf3-6c38c5db1639" />


A live-syncing, mobile-friendly dashboard to track placement / internship applications, PPTs, tests, resumes, and EA portal submissions — all organized by deadline and status.

## Features

- **6 organized views** to see what matters right now:
  - **By date** — upcoming deadlines and events, chronologically sorted with countdowns
  - **PPT schedule** — pending PPTs to attend, separated from missed ones, with completed PPTs marked ✓
  - **Test schedule** — tests yet to give, grouped away from passed tests
  - **Resume schedule** — resumes pending submission, vs. already submitted
  - **EA applications** — companies requiring EA portal applications, tracking pending vs. applied
  - **All companies** — full reference list, searchable and filterable

- **Live sync with Google Sheets** — edit your tracker spreadsheet, and changes appear on the site within 5 minutes (or instantly via the Refresh button)
- **Mobile optimized** — works on phone, tablet, desktop
- **No re-prompting** — once you mark something done (resume submitted, test given, PPT attended), it moves to a completed section and won't show in to-do lists anymore
- **Smart status tracking**:
  - Resume submitted? Shown as ✓ Submitted
  - Test given? Shown as ✓ Test given
  - PPT attended? Shown as ✓ Attended
  - EA applied? Shown as ✓ Applied
- **Recently passed deadlines** — see events from the last 7 days in a dimmed "Recently passed" section so you don't forget what just wrapped up

## Getting started

### Prerequisites
- A Google Sheet with your placement tracker data (see "Setting up the sheet" below)
- A GitHub account (free)

### Setting up the sheet

1. Make sure your spreadsheet has columns for:
   - Company name
   - PPT date
   - PPT status
   - Resume deadline
   - Resume status
   - EA status
   - GD status (optional)
   - Test deadline
   - Test status
   - Interview (optional)
   - Current action

2. **Important**: Move the Passwords column to a separate, unpublished tab (or delete it). The next step makes your data publicly readable.

3. In Google Sheets:
   - **File → Share → Publish to web**
   - Choose your tracker sheet tab (not the entire document)
   - Select **CSV** format
   - Click **Publish**
   - Copy the resulting link (it ends in `output=csv`)

### Deploying via GitHub Pages (free & easy)

1. **Create a GitHub repo**:
   - Go to [github.com](https://github.com)
   - Click **+** (top right) → **New repository**
   - Name it `internship-tracker`
   - Set it **Public**
   - Click **Create repository**

2. **Upload the tracker file**:
   - In your new repo, click **Add file → Upload files**
   - Download `placement-tracker.html` from the link provided
   - **Rename it to `index.html`** (GitHub Pages requires this)
   - Drag it into GitHub
   - Scroll down, click **Commit changes**

3. **Enable GitHub Pages**:
   - Go to repo **Settings** (top right)
   - Click **Pages** (left sidebar)
   - Under "Build and deployment", make sure **Source** is set to `main` branch, `/ (root)` folder
   - Wait 1–2 minutes, then refresh Settings → Pages
   - You'll see a green banner: **"Your site is published at https://yourusername.github.io/internship-tracker/"**
   - Share that link!

4. **Updating after changes**:
   - Edit your Google Sheet
   - On the tracker site, click the **↻ Refresh** button (top right) or wait 5 minutes for auto-sync
   - No need to touch GitHub — the site pulls fresh data from the sheet every time

## How to use

### Understanding the views

**By date**
- Shows all upcoming events (today onwards) sorted chronologically
- Each row has a countdown: "Today", "Tomorrow", "In 2 days", etc.
- Events older than today move to a "Recently passed" section below (last 7 days only, dimmed)

**PPT schedule**
- **Pending**: PPTs you haven't attended yet, by date
- **Missed**: PPTs you marked "Didnt attend" (for reference, no action needed)
- **Attended**: PPTs you've already sat through (marked ✓)

**Test schedule**
- **Pending**: Tests still to give, by date
- **Test given**: Tests already completed (✓)

**Resume schedule**
- **Pending**: Resumes not yet submitted
- **Submitted**: Resumes you've turned in (✓)

**EA applications**
- **Pending**: Companies where you still need to apply on the EA portal ("EA have to apply")
- **Applied**: Companies where you've already applied (✓)

**All companies**
- Full searchable/filterable table of every company
- Filter by Active (ongoing) or Closed applications
- Search by company name

### Status meanings

When entering data in your Google Sheet:

| Field | Meaning |
|-------|---------|
| `Attended PPT` | You went to this PPT → shows as ✓, won't reappear in pending |
| `Didnt attend` | You missed the PPT → moves to "Missed" section, no action needed |
| `Yet to attend PPT` | You haven't gone yet → shows in Pending with countdown |
| `Resume submitted` | You've submitted → shows as ✓, won't prompt for submission again |
| `Resume not submitted` | Pending → shows in Resume schedule with deadline countdown |
| `Gave test` | You took the test → shows as ✓, won't appear in pending |
| `Test yet to give` | Still pending → shows in Test schedule with deadline |
| `EA applied` | You've applied on the portal → shows as ✓ Applied |
| `EA have to apply` | Pending → shows in EA applications with no specific deadline |
| `Closed` | Application period over → company doesn't appear in active lists |

### Tips

1. **Dates matter**: Deadlines like "21st Jun EOD", "July 11th", "8th July 4:30 PM" are parsed automatically. Use clear, standard formats.
2. **Refresh manually** if you want changes to show up instantly — otherwise wait ~5 minutes.
3. **Mobile-friendly**: Open your GitHub Pages link on your phone, bookmark it.
4. **Share the link**: Just send the GitHub Pages URL to your friends / team. It's read-only; they can't edit it (only you can, via the sheet).

## Technical details

- **Single HTML file** — no installation, no dependencies
- **Live sync** — fetches your published Google Sheet CSV every 5 minutes
- **Fallback snapshot** — if Google Sheets is unreachable, shows a built-in snapshot so the site still works
- **Responsive design** — optimized for phone, tablet, desktop
- **Modern browser** — works in Chrome, Safari, Edge, Firefox (any modern browser)

## Customization

### Change auto-refresh interval
Open `placement-tracker.html` in a text editor, find:
```javascript
const AUTO_REFRESH_MINUTES = 5;
```
Change `5` to your preferred number (e.g., `1` for every minute, `10` for every 10 minutes).

### Use a different sheet
Open `placement-tracker.html`, find:
```javascript
const SHEET_CSV_URL = "https://docs.google.com/spreadsheets/d/...";
```
Replace with your published Google Sheet CSV link.

### Switch to snapshot data
To disable live sync and always use the built-in snapshot:
```javascript
const SHEET_CSV_URL = "";
```

## Troubleshooting

**"Sheet unreachable" message**
- Check that you published your sheet to the web (File → Share → Publish to web)
- Verify the CSV link is correct and accessible in your browser
- Refresh the page or click the ↻ Refresh button

**Changes aren't showing up**
- Wait a few seconds, then hit ↻ Refresh (top right)
- Check that you edited the correct sheet tab
- Ensure you actually saved the Google Sheet changes (Ctrl + S or Cmd + S)

**Site isn't live on GitHub Pages**
- Confirm your file is named exactly `index.html` (case-sensitive)
- Check Settings → Pages shows green "Your site is published"
- Hard-refresh your browser (Ctrl + Shift + R on desktop, or open in private/incognito mode on phone)

**Can't find a company I just added**
- The sheet must be published to the web first (File → Share → Publish to web)
- Wait ~5 minutes or click ↻ Refresh
- Make sure the company has at least a name in the first column

## Privacy & security

- **Your data is public** once you publish the sheet (anyone with the link can see it)
- **Remove the Passwords column** before publishing (it's not shown on the site, but the raw CSV is readable)
- **GitHub Pages is free** and secure (HTTPS by default)
- **No backend server** — everything runs locally in the browser

## Support

If something breaks or doesn't work as expected:
1. Open your browser's **Developer Console** (F12 → Console tab)
2. Check for error messages
3. Take a screenshot of the error
4. Verify your Google Sheet is published and the CSV link is accessible

---

**Happy tracking!** 🚀
