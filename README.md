# ⚡ Bidgely Energy Games — Full Kit

A gamification dashboard for utility homeowners. Admins upload real meter data via a password-protected panel. Homeowners see personalized energy scores, leaderboards, challenges, and badges — all running as a static site with zero backend required.

---

## 📁 What's in This Kit

```
bidgely-kit/
├── index.html              ← Homeowner gamification dashboard
├── admin.html              ← Admin panel (login + CSV upload)
└── sample-data/
    ├── enrollment.csv      ← Sample: 15 homes
    ├── consumption.csv     ← Sample: daily kWh (75 days × 15 homes)
    └── ac-appliances.csv   ← Sample: appliance breakdown (75 days × 15 homes)
```

> **Works out of the box** — the homeowner dashboard uses built-in sample data until real CSVs are uploaded by an admin.

---

## 🚀 How to Deploy on GitHub Pages (Step by Step)

### Step 1 — Create a free GitHub account
Go to [github.com](https://github.com) and sign up. It's free.

### Step 2 — Create a new repository
1. Click the **+** button in the top-right corner → **New repository**
2. Name it: `bidgely-energy-games` (or any name you like)
3. Set visibility to **Public**
4. Click **Create repository**

### Step 3 — Upload your files
1. On your new repository page, click **Add file → Upload files**
2. Drag and drop ALL files from this kit:
   - `index.html`
   - `admin.html`
   - The `sample-data/` folder (drag the whole folder)
3. At the bottom, click **Commit changes**

### Step 4 — Enable GitHub Pages
1. Go to your repository's **Settings** tab (top menu)
2. Scroll down to **Pages** in the left sidebar
3. Under **Source**, select:
   - Branch: `main`
   - Folder: `/ (root)`
4. Click **Save**
5. Wait about 1–2 minutes

### Step 5 — Get your live URL
GitHub will show you a URL like:
```
https://YOUR-USERNAME.github.io/bidgely-energy-games/
```
Share `index.html` with homeowners and `admin.html` with your team.

---

## 🔐 Admin Panel

**URL:** `https://YOUR-USERNAME.github.io/bidgely-energy-games/admin.html`

**Default login:**
- Username: `admin`
- Password: `bidgely2026`

> You can change the password inside the admin panel after logging in.

---

## 📊 Uploading Real Data

Inside the admin panel, upload three CSV files in order:

### File 1: Enrollment (`enrollment.csv`)
One row per home. Required columns:

| Column | Description | Example |
|--------|-------------|---------|
| `meter_id` | Unique ID for this meter | `M001` |
| `name` | Homeowner name | `John D.` |
| `address` | Street address | `12 Oak Street` |
| `baseline_daily_kwh` | Normal daily usage (kWh) | `35` |
| `zip_code` | Zip code (optional) | `94025` |
| `home_type` | House / Condo / Apartment (optional) | `House` |
| `sq_footage` | Square footage (optional) | `1800` |
| `enrolled_date` | Date enrolled (optional) | `2025-01-15` |

### File 2: Consumption History (`consumption.csv`)
One row per meter per day. Required columns:

| Column | Description | Example |
|--------|-------------|---------|
| `meter_id` | Must match enrollment file | `M001` |
| `date` | Date in YYYY-MM-DD format | `2026-03-01` |
| `total_kwh` | Total kWh consumed that day | `28.4` |

### File 3: Appliance Breakdown (`ac-appliances.csv`)
One row per meter per day. Required columns:

| Column | Description | Example |
|--------|-------------|---------|
| `meter_id` | Must match enrollment file | `M001` |
| `date` | Date in YYYY-MM-DD format | `2026-03-01` |
| `peak_kwh` | Usage during peak hours | `12.3` |
| `offpeak_kwh` | Usage during off-peak hours | `16.1` |
| `ac_kwh` | Air conditioning usage (optional) | `5.2` |
| `heating_kwh` | Heating usage (optional) | `8.1` |
| `washer_kwh` | Washer usage (optional) | `0.8` |
| `dryer_kwh` | Dryer usage (optional) | `1.2` |
| `ev_kwh` | Electric vehicle charging (optional) | `4.0` |

> **Important:** The `meter_id` values must be identical across all three files. If a meter appears in consumption but not in enrollment, it will be ignored.

---

## 🎮 Dashboard Features

| Feature | Description |
|---------|-------------|
| **Energy Score** | 0–100 score combining usage reduction, off-peak shifting, and carbon savings |
| **Daily Streak** | Consecutive days where usage was below the household baseline |
| **Leaderboard** | 4 categories: Overall, AC Warriors, Night Shifters, Carbon Crushers |
| **Challenges** | 5 auto-generated challenges based on each user's appliance data |
| **Badges** | 12 badges with progress tracking: earned, in-progress, and locked |
| **Points** | Automatically redeemable for bill credits (e.g. 1,000 pts = $1.00) |

---

## 🏠 How Homeowners Use It

1. Go to the site URL
2. Select their home from the dropdown
3. Explore their personal dashboard

> No password needed for homeowners in this demo version. For a production deployment with real user authentication, a backend server would be required.

---

## ⚙️ Technical Notes

- **No backend required** — all data is stored in the browser's localStorage
- **Data is per-device** — each browser stores its own copy; uploading on one device won't sync to others
- **For production use**, consider integrating with a real API/database and adding proper authentication
- The site works fully offline after the first load

---

## 🆘 Troubleshooting

**The site shows a blank page or error:**
Make sure all files are uploaded and GitHub Pages is enabled (Step 4 above). It can take a few minutes to go live.

**I uploaded CSVs but the dashboard still shows sample data:**
Check that the `meter_id` values in your CSVs exactly match between enrollment, consumption, and appliances files. Column names must match exactly (case-sensitive).

**I forgot the admin password:**
Open your browser's developer tools (F12), go to Application → Local Storage, and delete the `bidgely_admin_pw` key. The default password (`bidgely2026`) will be restored.

**Data isn't showing for some homeowners:**
Make sure their `meter_id` appears in both the enrollment file and the consumption/appliance files.

---

*Built with HTML, CSS, and vanilla JavaScript. No frameworks, no build step, no server.*
