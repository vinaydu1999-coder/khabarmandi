# सतासीराज ख़बर मंडी 📰
### SatashiRaj Khabar Mandi — Bilingual Hindi-English News Portal

> **Live Site:** https://strkhabar.pages.dev  
> **Founded by:** Kunwar Sheel Vardhan Pratap Singh  
> **In association with:** Vinay Chaurasiya

---

## 📁 File Structure

```
satashiraj-news/
│
├── index.html          ← Main SPA — all screens, SEO meta, embedded logo
│
├── js/
│   ├── seo.js          ← SEO engine (slugs, meta tags, sitemap, OG, JSON-LD)
│   └── app.js          ← Full app logic (articles, auth, admin, writer portal)
│
├── logo.jpg            ← Satasiraj building logo image
├── og-default.svg      ← Default Open Graph share image
├── sitemap.xml         ← Static sitemap (update via Admin → SEO Tools)
├── robots.txt          ← Search engine crawl rules
├── _headers            ← Cloudflare Pages HTTP cache/security headers
├── _redirects          ← Cloudflare Pages SPA URL routing
├── .gitignore          ← Git ignore rules
└── README.md           ← This file
```

---

## 🚀 Deploy to Cloudflare Pages

### Step 1 — Push to GitHub

```bash
git init
git add .
git commit -m "SatashiRaj Khabar Mandi — initial deploy"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/satashiraj-news.git
git push -u origin main
```

### Step 2 — Connect to Cloudflare Pages

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com) → **Pages** → **Create a project**
2. Click **Connect to Git** → Select your GitHub repo
3. Build settings:
   - **Framework preset:** `None`
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/` *(root)*
4. Click **Save and Deploy**

### Step 3 — Your site is live! ✅

Every time you push to GitHub → Cloudflare auto-redeploys in ~30 seconds.

---

## 🔥 Features

### 📝 Article Publishing
- Write in **Hindi** or **English**
- Rich text editor with bold, italic, underline
- Image upload via ImgBB CDN
- Category selection (10 categories)
- District field for Local News
- Writer submit → Admin approve workflow

### 💡 Thought of the Day
- Writers submit daily quotes/thoughts
- Admin approves → shows in gold banner above news
- Auto-selects today's approved thought by date

### 🔍 SEO (Auto-generated per article)
- SEO-friendly URL slugs (Hindi transliteration)
- Canonical URLs
- NewsArticle JSON-LD structured data
- Open Graph tags (WhatsApp, Telegram previews)
- Twitter Card meta tags
- Google News compatible timestamps
- Live SEO score preview in write form (0–100%)
- Character counters for title (30–65) and summary (80–160)
- Keyword & headline suggestions per category

### 🗺️ Sitemap Tools (Admin → SEO Tools)
- Download `sitemap.xml` with all articles
- Includes Google News sitemap extension
- SEO audit table for all published articles
- One-click "Fix Missing Slugs"

### 👥 User System
- Admin account (full control)
- Writer accounts (submit articles, thoughts)
- Writer request approval workflow
- Pending/Approved/Rejected states

---

## 🔧 Firebase Setup

### Firestore Rules
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /articles/{id} {
      allow read: if resource.data.status == 'published';
      allow read, write: if request.auth != null;
    }
    match /thoughts/{id} {
      allow read: if resource.data.status == 'approved';
      allow read, write: if request.auth != null;
    }
    match /users/{id} {
      allow read, write: if request.auth != null;
    }
    match /writerRequests/{id} {
      allow read, write: if request.auth != null;
    }
    match /settings/{id} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

### Required Firestore Indexes
| Collection | Field 1 | Field 2 | Scope |
|---|---|---|---|
| `thoughts` | `status` ASC | `createdAt` DESC | Collection |
| `articles` | `status` ASC | `createdAt` DESC | Collection |

### Collections Used
| Collection | Purpose |
|---|---|
| `articles` | News articles |
| `thoughts` | Thought of the Day |
| `users` | Admin / writer accounts |
| `writerRequests` | New writer signup requests |
| `settings` | viewMultiplier, site config |

---

## 📡 Google Search Console Setup

1. Go to https://search.google.com/search-console
2. Add property: `https://strkhabar.pages.dev`
3. Verify via HTML meta tag
4. Submit sitemap: `https://strkhabar.pages.dev/sitemap.xml`

### Update Sitemap After Publishing Articles
1. Admin Dashboard → **SEO Tools** tab
2. Click **"⬇ Download sitemap.xml"**
3. Replace `sitemap.xml` in this repo
4. `git add sitemap.xml && git commit -m "Update sitemap" && git push`
5. Cloudflare auto-redeploys ✅

---

## 📱 Google News Eligibility

- ✅ NewsArticle schema on every article
- ✅ `datePublished` timestamp on all articles
- ✅ Author byline required
- ✅ Category navigation
- ✅ Bilingual Hindi + English
- ✅ Open Graph + Twitter Cards
- ✅ Sitemap with `news:` extension
- ✅ Fast (Cloudflare CDN)
- ✅ HTTPS
- ⬜ Apply at: https://publishercenter.google.com

---

## 📋 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML/CSS/JS (Single Page App) |
| Database | Firebase Firestore |
| Auth | Firebase Authentication |
| Image Upload | ImgBB API |
| Hosting | Cloudflare Pages |
| Fonts | Google Fonts (Noto Serif Devanagari, Playfair Display) |

---

## 📞 Contact

**Founder:** Kunwar Sheel Vardhan Pratap Singh  
**Associate:** Vinay Chaurasiya  
**Site:** https://strkhabar.pages.dev
