# Byters Lead Finder

A sleek, modern lead generation tool for Indian local businesses. Scraps JustDial for businesses without websites, generates WhatsApp pitches using AI, and tracks pitched leads in Supabase.

## 🎨 Design

- **Theme**: Dark, minimal, dev-tool aesthetic
- **Colors**: 
  - Background: `#0F0F14`
  - Cards: `#1A1A23`
  - Borders: `#32323F`
  - Accent: `#0A84FF` (electric blue)
- **Font**: System UI / Inter
- **Principles**: Clean, minimal, fast — no clutter

## 🚀 Features

### 1. Search Bar (Top)
- City dropdown: Kolkata, Mumbai, Delhi, Bangalore, Chennai, Hyderabad
- Category dropdown: Salon, Cafe, Gym, Interior Designer, Photographer
- Large blue "Find Leads" button

### 2. Stats Row (Below Search)
- **X leads found** - Total leads from search
- **X already pitched** - Previously contacted
- **X new today** - Fresh leads (green accent)

### 3. Results Grid
Per business card:
- **Business name** (bold)
- **Category badge** (colored pill)
- **Template matched** (e.g., "Salon template")
- **Status badge**: Green "New lead" or Grey "Already pitched"
- **📲 Send on WhatsApp** button → opens wa.me link in new tab
  - On click → saves to Supabase + turns badge grey

### 4. Empty States
- **Initial state**: "Search a city and category to find leads"
- **No results**: "No new leads found. Try another category."

### 5. Loading State
- Skeleton cards while scraping/fetching

## ⚠️ Important: Project Structure

This repo has **two separate parts**. They run independently:

| Part | Location | Runs With |
|------|----------|-----------|
| **Frontend** (React dashboard) | `src/` | `npm run dev` (Vite) |
| **Backend engine** (AI pipeline) | `engine/` | `node engine/job.js` (Node.js only) |

> The `engine/` folder is **NOT** part of the React app. Never import from `engine/` in `src/` — they are separate.

---

## 🚀 Setup (for anyone cloning this repo)

### Step 1 — Install frontend dependencies
```bash
npm install
```

### Step 2 — Create your `.env` file
```bash
cp .env.example .env
```
Then open `.env` and fill in your real credentials (ask the repo owner for these values):
```
VITE_GROQ_KEY=your_groq_api_key_here
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key_here
```

> ⚠️ **The `.env` file is secret — it is gitignored and was NOT pushed to GitHub.** You must create it manually.

### Step 3 — Run the frontend
```bash
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

### Step 4 (optional) — Run the backend engine
The `engine/` folder is a standalone Node.js pipeline. Run it **separately** in a terminal:
```bash
node --env-file=.env engine/job.js
```
> Requires Node.js 18+



## 📝 WhatsApp Message Template

```
Hi, I'm Abir from Byters. I made a free demo website for {biz_name}. 
I can make it live in 2 days for just ₹5,000. 
Interested? Here's a preview: [demo link]
```

## 🗄 Database Schema (Supabase)

### Table: `pitched_leads`

| Column | Type | Description |
|--------|------|-------------|
| id | text | Unique lead ID (e.g., jd_001) |
| name | text | Business name |
| category | text | Business category |
| phone | text | Phone number |
| pitched_at | timestamptz | When pitched (default: now()) |

## 🔍 API Integration (Future)

### JustDial Scraper
- Fetch businesses by city + category
- Filter: businesses with no website
- Returns business name, phone, category

### Groq LLM
- Match business to appropriate template
- Generate WhatsApp pitch message
- Templates: Salon, Cafe, Gym, Interior Designer, Photographer

### Supabase
- Check if lead already pitched (avoid duplicates)
- Save new pitched leads
- Query pitched leads count

## 🎯 Design Decisions

1. **Dark Theme**: Less eye strain for dev tools, modern aesthetic
2. **No CSS Framework**: Full control, smaller bundle, faster load
3. **Electric Blue Accent**: High contrast, pops against dark background
4. **Minimal Cards**: Focus on data, not decoration
5. **Skeleton Loading**: Perceived performance, smooth UX

## 📱 Responsive

- Mobile-first design
- Grid adapts from 1 column (mobile) to 4 columns (desktop)
- Touch-friendly buttons and selects

## 🔧 Future Enhancements

1. Backend scraper for JustDial
2. Groq AI integration for template matching
3. Real Supabase database for persistent storage
4. Lead history page
5. Export to CSV
6. Bulk pitch feature
7. Template editor
8. A/B testing for messages

## 📄 License

MIT
