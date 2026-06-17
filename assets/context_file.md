# 🧑‍💻 Aman Gupta — Developer Portfolio

> A single-page personal portfolio website built with pure HTML, CSS, and vanilla JavaScript. No frameworks, no build tools, no dependencies — just clean, fast, hand-crafted code.

**Live site:** [amanguptadevportfolio.vercel.app](https://amanguptadevportfolio.vercel.app)

---

## 📸 Preview

| Light Mode | Dark Mode |
|---|---|
| Cream/parchment theme | Dark ink theme |

---

## 🗂️ Project Structure

```
portfolio_final/
├── index.html                        # Entire website — single file
├── robots.txt                        # Tells search crawlers to index the site
├── sitemap.xml                       # Helps Google discover and rank the page
├── README.md                         # This file
└── assets/
    ├── profile.jpg                   # Profile photo (About section)
    ├── Aman_Gupta_Resume.pdf         # Downloadable resume
    ├── favicon.ico                   # Browser tab icon (all browsers)
    ├── favicon-96x96.png             # High-res favicon
    ├── apple-touch-icon.png          # iOS home screen icon
    ├── site.webmanifest              # PWA manifest — links all icons
    ├── web-app-manifest-192x192.png  # Android / Google Search icon
    └── web-app-manifest-512x512.png  # High-res PWA install icon
```

---

## 🎨 Design System

### Fonts
| Font | Usage | Source |
|---|---|---|
| Playfair Display | Headings, hero title, section titles | Google Fonts |
| Outfit | Body text, labels, buttons, nav | Google Fonts |

### Color Palette

#### Light Theme
| Variable | Hex | Usage |
|---|---|---|
| `--cream` | `#f5f0e8` | Page background (cream/parchment) |
| `--cream2` | `#ede8de` | Card backgrounds, inputs |
| `--cream3` | `#e4ddd0` | Hover states |
| `--ink` | `#1a1612` | Primary text |
| `--ink3` | `#5e5650` | Muted/secondary text (WCAG AA compliant) |
| `--ink4` | `#b0a898` | Dimmed text — dates, labels |
| `--rust` | `#c4521a` | Accent — buttons, links, highlights |
| `--border` | `#d8d0c4` | Card and section borders |

#### Dark Theme
| Variable | Hex | Usage |
|---|---|---|
| `--cream` | `#120f0c` | Page background |
| `--cream2` | `#1c1814` | Card backgrounds |
| `--ink` | `#f0ebe3` | Primary text |
| `--ink3` | `#8a8078` | Muted text |
| `--rust` | `#e06030` | Accent (brighter for dark bg) |
| `--border` | `#2e2920` | Borders |

### Design Principles
- **Warm editorial aesthetic** inspired by Ryan Sullivan Framer template
- **Grain texture overlay** via SVG noise filter on `body::after`
- **Cream + rust** color pairing — professional but personal
- All spacing uses `clamp()` for fluid responsive scaling

---

## 🏗️ Architecture — How the Page is Built

The entire site is **one HTML file** (`index.html`) with three sections:

### 1. `<head>` — Meta, fonts, favicon, SEO
```
<meta> tags          → SEO title, description, OG social preview
Google Fonts         → Loaded non-blocking (preload trick)
Favicon links        → Points to /assets/ folder
CSS variables        → All theme colors defined as :root variables
Structured Data      → JSON-LD schema for Google Knowledge Graph
Google Analytics     → G-DH4PJ8NLVC tracking
Google Verification  → Search Console ownership verification
```

### 2. `<body>` — All visible content

| Section | ID | Description |
|---|---|---|
| Navigation | `#nav` | Sticky nav with dark mode toggle + hamburger |
| Hero | `#hero` | Two-column: title+stats left, terminal card right |
| Ribbon | — | Auto-scrolling skills marquee ticker |
| Projects | `#projects` | 3 project cards with tech pills and achievement badges |
| Skills | `#skills` | 4-box grid — Frontend, Backend, Databases, IoT |
| About | `#about` | Two-column layout — photo + bio |
| Experience | `#experience` | Timeline list — jobs and education |
| FAQ | `#faq` | Accordion — 5 questions about working with me |
| Contact | `#contact-sec` | CTA headline + Formspree contact form |
| Footer | — | Copyright line |

### 3. `<script>` — All interactivity (vanilla JS only)
```
scrollRestoration    → Forces page to top on every refresh
Custom cursor        → Follows mouse on desktop only
Nav stuck state      → Backdrop blur when scrolled past 40px
Scroll reveal        → IntersectionObserver fade-in animations
Terminal animation   → Hero right card typewriter effect
3D tilt              → Mouse parallax on terminal card
FAQ accordion        → toggleFaq() open/close panels
Dark mode            → localStorage + system preference
Hamburger menu       → Mobile drawer animation
Contact form         → Formspree AJAX with full validation
```

---

## ✨ Features Breakdown

### Dark Mode
- Toggled via animated sun/moon toggle button in nav
- Uses `data-dark` attribute on `<html>` element
- Persists across sessions via `localStorage`
- Auto-detects system preference on first visit
```js
applyTheme(localStorage.getItem('theme') === 'dark');
```

### Scroll to Top on Refresh
Browsers remember scroll position by default — this fixes it:
```js
if('scrollRestoration' in history) history.scrollRestoration = 'manual';
window.scrollTo(0, 0);
```
Place this as the **first two lines** of your script block.

### Custom Cursor
- Only activates on desktop (hover:hover + pointer:fine)
- Completely disabled on mobile/touch — prevents stuck cursor bug
```js
if(window.matchMedia('(hover:hover) and (pointer:fine)').matches){
  // all cursor code here — never runs on touch devices
}
```

### Hero Terminal Card
- Animated typewriter terminal on the right side of hero
- Lines appear with staggered delays using `setTimeout`
- Progress bar animates from 0% → 100% as terminal fills
- Status badges fade in when build completes
- 3D tilt effect on mouse move using `perspective()` + `lerp()`
- Uses `requestAnimationFrame` for smooth GPU animation

### Scroll Reveal Animations
- `IntersectionObserver` API — no library needed
- Elements start `opacity:0; transform:translateY(28px)`
- Get `.on` class when 10% visible → fade + slide up
- Stagger delays via `.reveal-d1`, `.reveal-d2`, `.reveal-d3`

### Responsive Layout
- **Mobile** (`<860px`): Single column, hamburger nav, stacked hero
- **Desktop** (`>860px`): Two-column hero, visible nav links
- All font sizes use `clamp(min, preferred, max)` — fluid scaling

### Skills Marquee Ribbon
- Pure CSS animation — `animation: slide 28s linear infinite`
- Content duplicated in HTML for seamless infinite loop
- Zero JavaScript needed

### FAQ Accordion
- `max-height: 0` → `max-height: 300px` CSS transition
- One item open at a time
- `+` rotates to `×` via CSS transform

---

## 📬 Contact Form — Formspree

**Service:** [Formspree](https://formspree.io) · Free tier · 50 submissions/month
**Endpoint:** `https://formspree.io/f/meedwbdb`

### Why Formspree over EmailJS
- Formspree never requests OAuth access to Gmail inbox
- EmailJS requires Gmail OAuth (send permission) — privacy concern
- Formspree forwards to your email like a postal service — no credentials needed

### How it works
1. User fills Name, Email, Message → clicks Send
2. JS intercepts submit → sends `fetch()` POST to Formspree
3. Formspree forwards email to `amangupta7203@gmail.com`
4. No backend, no database, no server needed

### Security measures
| Protection | Method |
|---|---|
| Bot spam | Honeypot field `name="_gotcha"` hidden from humans |
| Input flooding | `maxlength` — 100/150/2000 chars |
| Invalid email | Regex `/^[^\s@]+@[^\s@]+\.[^\s@]+$/` |
| Double submit | `sending` boolean flag |
| Network errors | `try/catch` with user-friendly messages |

---

## 🚀 Deployment

**Platform:** [Vercel](https://vercel.com) (free tier)

### How it works
1. Code in GitHub: `amanguptadev12/amangupta_portfolio`
2. Vercel connected to repo — auto-deploys on every push
3. No build step — static HTML deploys in ~30 seconds

### Deploy
```bash
git add .
git commit -m "your message"
git push
```

### Required files at root
```
index.html   ← entry point
robots.txt   ← allows Google to crawl
sitemap.xml  ← helps Google index faster
```

---

## 📊 Lighthouse Scores (Mobile, Slow 4G)

| Category | Score | Status |
|---|---|---|
| Performance | 58–60 | 🔴 TBT high — terminal animation causes main thread blocking |
| Accessibility | 94 | 🟢 Good |
| Best Practices | 100 | ✅ Perfect |
| SEO | 100 | ✅ Perfect |

### Optimisations applied
- Google Fonts loaded with `preload` + `media="print"` trick
- Custom cursor disabled on touch (fixes mobile stuck cursor bug)
- `loading="lazy"` + `decoding="async"` on profile photo
- `width` + `height` attributes on images prevent layout shift
- `scrollRestoration = 'manual'` prevents scroll position memory

### Known performance issue
Terminal animation progress bar uses `width` CSS property which causes forced reflow.
**Fix (pending):** Replace with `transform: scaleX()` — GPU composited, no reflow:
```css
/* WRONG — causes forced reflow */
.hr-prog-fill { transition: width .6s; }

/* RIGHT — GPU composited */
.hr-prog-fill { transform-origin: left; transition: transform .6s; }
```

---

## 🔍 SEO Setup

### Meta tags (single set — no duplicates)
```html
<meta name="description" content="...">      ← One description only
<meta name="keywords" content="...">         ← One keywords tag only
<meta name="author" content="Aman Gupta">
<meta name="robots" content="index, follow">
<meta name="google-site-verification" content="...">
```

### ⚠️ Common mistake — duplicate meta tags
Having more than one `description` or `keywords` tag causes Google to ignore all of them.
Always search `Ctrl+F → name="description"` and confirm only one result exists.

### Open Graph
```html
<meta property="og:title">       ← WhatsApp/LinkedIn preview title
<meta property="og:description"> ← Preview description
<meta property="og:image">       ← photo.jpg used as preview image
<meta property="og:url">         ← canonical URL
<meta property="og:locale">      ← en_IN for Indian English
```

### Twitter Card
```html
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title">
<meta name="twitter:description">
<meta name="twitter:image">
```

### JSON-LD Structured Data
Tells Google you are a Person with job title, location, email, social profiles.
Can trigger a Knowledge Panel for your name in Google Search.
```json
{
  "@type": "Person",
  "name": "Aman Gupta",
  "jobTitle": "Full-Stack Developer",
  "sameAs": ["linkedin.com/in/amangdev", "github.com/amanguptadev12"]
}
```

### Files
```
robots.txt   → User-agent: * / Allow: /
sitemap.xml  → https://amanguptadevportfolio.vercel.app/
```

### Google Search Console
- Verified via `google-site-verification` meta tag ✅
- Sitemap submitted ✅
- URL inspection + Request Indexing done ✅
- New sites take **1–4 weeks** to appear in Google results

---

## 🖼️ Favicon Setup

All files in `/assets/`:

| File | Size | Used by |
|---|---|---|
| `favicon.ico` | 15 KB | All browsers (fallback) |
| `favicon-96x96.png` | 17 KB | High-res browser tabs |
| `apple-touch-icon.png` | 48 KB | iOS home screen |
| `web-app-manifest-192x192.png` | 53 KB | Android / Google Search results |
| `web-app-manifest-512x512.png` | 251 KB | PWA install icon |
| `site.webmanifest` | 1 KB | Links all icons — name, theme color |

### ⚠️ Two mistakes to avoid

**Mistake 1 — Wrong icon paths in webmanifest:**
```json
// WRONG — file not found, Google shows globe icon
"src": "/web-app-manifest-192x192.png"

// CORRECT — includes /assets/ prefix
"src": "/assets/web-app-manifest-192x192.png"
```

**Mistake 2 — Corrupt/empty icon files:**
If `web-app-manifest-192x192.png` is 0 bytes, Google shows globe even with correct paths.
Always verify the file is accessible and non-empty:
```
https://amanguptadevportfolio.vercel.app/assets/web-app-manifest-192x192.png
```
Should display your photo — not a blank page.

---

## 🛠️ Key Decisions Explained

### Why single HTML file?
- Zero build tooling = instant deploy anywhere
- No npm, no webpack, no React — nothing to break or update
- Easy to hand off, version, or fork

### Why Formspree over EmailJS?
- Formspree: no OAuth, no inbox access, forwards like email
- EmailJS: requires Gmail OAuth send permission — privacy concern

### Why Vercel over Netlify?
- Faster CDN for India-region visitors
- Zero-config GitHub auto-deploy
- Both free — Vercel slightly better performance

### Why CSS variables for theming?
- Toggle `data-dark` on `<html>` — all 15+ colors update instantly
- No JS color switching needed
- Easy to reskin — change variables, entire site recolors

### Why IntersectionObserver over AOS/GSAP?
- Native browser API — zero bundle overhead
- Works on all modern browsers
- No library to maintain or update

### The cursor mobile bug
```js
// WRONG — cursor element still exists in DOM on mobile
@media(pointer:fine){ #cur{ display:block } }

// CORRECT — JS never runs on touch devices
if(window.matchMedia('(hover:hover) and (pointer:fine)').matches){
  // cursor code here
}
```

---

## 📦 Third Party Services

| Service | Purpose | Free Tier |
|---|---|---|
| Google Fonts | Playfair Display + Outfit | Free |
| Formspree | Contact form forwarding | 50/month |
| Vercel | Hosting + auto-deploy | Free |
| Google Analytics | Traffic tracking (G-DH4PJ8NLVC) | Free |
| Google Search Console | SEO + indexing | Free |
| realfavicongenerator.net | Favicon package | Free |
| squoosh.app | Image compression | Free |

---

## 🔮 Future Improvements

- [ ] Fix terminal progress bar — replace `width` with `transform: scaleX()`
- [ ] Convert `assets/profile.jpg` to WebP (save ~60 KiB, improve LCP)
- [ ] Add GitHub links on each project card
- [ ] Add actual project screenshots to replace gradient thumbnails
- [ ] Fix contrast on `.muted` hero title and `span.ft` footer text
- [ ] Add `<main>` landmark for better accessibility score
- [ ] Add `vercel.json` for cache control headers
- [ ] Custom domain (e.g. `amangupta.dev`)

---

## ✅ Completed Improvements

- [x] Dark mode toggle with animated sun/moon button
- [x] Mobile hamburger menu with drawer
- [x] Custom cursor — desktop only, touch disabled
- [x] Scroll to top on refresh (`scrollRestoration = 'manual'`)
- [x] Contact form with Formspree + full validation + honeypot
- [x] Favicon — all sizes including 192px and 512px for Google Search
- [x] Fixed webmanifest icon paths (`/assets/` prefix)
- [x] Replaced corrupt favicon files
- [x] SEO 100 — meta description, keywords, OG, Twitter Card, JSON-LD
- [x] Google Analytics integrated
- [x] Google Search Console verified + sitemap submitted
- [x] Removed duplicate meta description and keywords tags
- [x] Profile photo with `loading="lazy"` + `decoding="async"`
- [x] Non-blocking Google Fonts loading

---

## 👤 Author

**Aman Gupta**
B.Tech CSE — United College of Engineering and Research, Prayagraj (2023–2027)
📧 amangupta7203@gmail.com
🔗 [linkedin.com/in/amangdev](https://linkedin.com/in/amangdev)
💻 [github.com/amanguptadev12](https://github.com/amanguptadev12)
🌐 [amanguptadevportfolio.vercel.app](https://amanguptadevportfolio.vercel.app)

---

*Built from scratch in one conversation. No templates, no frameworks, no shortcuts.*
