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
├── index.html              # Entire website — single file
├── photo.jpg               # Profile photo (About section)
├── robots.txt              # Tells search crawlers to index the site
├── sitemap.xml             # Helps Google discover and rank the page
├── README.md               # This file
└── assets/
    ├── favicon.ico         # Browser tab icon
    ├── favicon-96x96.png   # High-res favicon
    ├── apple-touch-icon.png# iOS home screen icon
    └── site.webmanifest    # PWA manifest for Android/Chrome
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
| `--bg` | `#f5f0e8` | Page background (cream/parchment) |
| `--bg2` | `#ede8de` | Card backgrounds, inputs |
| `--bg3` | `#e4ddd0` | Hover states |
| `--ink` | `#1a1612` | Primary text |
| `--ink3` | `#5e5650` | Muted/secondary text |
| `--rust` | `#c4521a` | Accent color — buttons, links, highlights |
| `--border` | `#d8d0c4` | Card and section borders |

#### Dark Theme
| Variable | Hex | Usage |
|---|---|---|
| `--bg` | `#0f0e0c` | Page background |
| `--card-bg` | `#1c1a16` | Card backgrounds |
| `--ink` | `#f0ece4` | Primary text |
| `--rust` | `#e06b30` | Accent (slightly brighter for dark bg) |
| `--border` | `#2e2a24` | Borders |

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
<meta> tags        → SEO title, description, OG social preview
Google Fonts       → Loaded non-blocking (preload trick to avoid render blocking)
Favicon links      → Points to /assets/ folder
CSS variables      → All theme colors defined here as :root variables
```

### 2. `<body>` — All visible content
The page is divided into these sections top to bottom:

| Section | ID | Description |
|---|---|---|
| Social Bar | `#social-bar` | Fixed top bar — LinkedIn, GitHub, Resume links |
| Navigation | `#nav` | Sticky nav with dark mode toggle + hamburger |
| Hero | `#hero` | Full-height intro with title, stats, availability pill |
| Ribbon | — | Auto-scrolling skills marquee ticker |
| Projects | `#projects` | 3 project cards with tech pills and achievement badges |
| Skills | `#skills` | 4-box grid — Frontend, Backend, Databases, IoT |
| About | `#about` | Two-column layout — photo + bio |
| Experience | `#experience` | Timeline list — jobs and education |
| FAQ | `#faq` | Accordion — 5 questions about working with me |
| Contact | `#contact-sec` | CTA headline + email + Formspree contact form |
| Footer | — | Copyright line |

### 3. `<script>` — All interactivity (vanilla JS only)
```
Custom cursor      → Follows mouse, expands on hover (desktop only)
Nav stuck state    → Adds backdrop blur when user scrolls past 40px
Scroll reveal      → IntersectionObserver fades sections in on scroll
FAQ accordion      → toggleFaq() opens/closes answer panels
Dark mode          → Reads/writes localStorage, respects system preference
Hamburger menu     → Animates to X, slides in mobile drawer
Contact form       → Formspree AJAX submission with validation
```

---

## ✨ Features Breakdown

### Dark Mode
- Toggled via button in nav (☀/☽ icon)
- Uses `data-theme` attribute on `<html>` element
- Persists across sessions via `localStorage`
- Auto-detects system preference on first visit via `prefers-color-scheme`
```js
if(window.matchMedia('(prefers-color-scheme: dark)').matches)
  html.setAttribute('data-theme','dark');
```

### Custom Cursor
- Only activates on desktop (pointer:fine + hover:hover media query)
- Completely disabled on mobile/touch to prevent the "stuck cursor" bug
```js
if(window.matchMedia('(hover:hover) and (pointer:fine)').matches){
  // cursor code here
}
```

### Scroll Reveal Animations
- Uses `IntersectionObserver` API — no library needed
- Elements start `opacity:0; transform:translateY(24px)`
- Get `.on` class when 8% visible → fade + slide up
- Stagger delays via `.reveal-d1`, `.reveal-d2`, `.reveal-d3` classes

### Responsive Layout
- **Mobile** (`<480px`): Single column, hamburger nav, stacked stats
- **Tablet** (`480–900px`): Single column, hamburger nav
- **Desktop** (`>900px`): Full two-column layouts, visible nav links
- All font sizes use `clamp(min, preferred, max)` — fluid scaling

### Skills Marquee Ribbon
- Pure CSS animation — `animation: slide 28s linear infinite`
- Content duplicated in HTML to create seamless infinite loop
- No JavaScript needed

### FAQ Accordion
- `max-height: 0` → `max-height: 300px` transition trick
- Only one item open at a time
- Smooth `+` to `×` icon rotation via CSS transform

---

## 📬 Contact Form — Formspree

**Service used:** [Formspree](https://formspree.io) (free tier — 50 submissions/month)

### How it works
1. User fills Name, Email, Message → clicks Send
2. JavaScript intercepts submit, sends `fetch()` POST to Formspree endpoint
3. Formspree receives data → forwards email to `amangupta7203@gmail.com`
4. No backend, no database, no server needed

### Security measures built in
| Protection | How |
|---|---|
| Bot spam | Honeypot field (`name="_gotcha"`, hidden from humans) |
| Input flooding | `maxlength` on all fields (100/150/2000 chars) |
| Invalid email | Regex validation before submission |
| Rapid resubmit | `sending` boolean flag blocks double-clicks |
| Network errors | `try/catch` with user-friendly error messages |

### Form endpoint
```
action="https://formspree.io/f/YOUR_FORM_ID"
```

---

## 🚀 Deployment

**Platform:** [Vercel](https://vercel.com) (free tier)

### How deployment works
1. Code lives in GitHub repo: `amanguptadev12/amanagupta_portfolio`
2. Vercel is connected to the GitHub repo
3. Every `git push` to `main` branch → Vercel auto-deploys in ~30 seconds
4. No build step needed — static HTML deploys instantly

### Deploy manually
```bash
git add .
git commit -m "your message"
git push
```

### Files Vercel needs at root
```
index.html      ← required (entry point)
robots.txt      ← tells Google to crawl the site
sitemap.xml     ← helps Google index faster
```

---

## 📊 Lighthouse Scores (Mobile, Slow 4G)

| Category | Score | Notes |
|---|---|---|
| Performance | 85 | LCP 3.1s — fonts non-blocking, no heavy assets |
| Accessibility | 93 | Contrast fixed, main landmark added |
| Best Practices | 100 | Perfect |
| SEO | 90 | Meta description added, sitemap present |

### Known optimisations applied
- Google Fonts loaded with `preload` + `media="print"` trick (saves ~110ms)
- Custom cursor disabled on touch devices
- Images served from same origin (no external CDN latency)
- No JavaScript frameworks — zero bundle overhead

---

## 🔍 SEO Setup

```html
<meta name="description" content="...">     ← Controls Google snippet text
<meta property="og:title">                  ← WhatsApp/LinkedIn preview title
<meta property="og:image">                  ← Social share preview image
<meta property="og:url">                    ← Canonical URL
```

```
robots.txt   → Allow: / (all pages crawlable)
sitemap.xml  → Lists the URL for Google to index
```

---

## 🛠️ If You Build This Again — Key Decisions Explained

### Why single HTML file?
- Zero build tooling = instant deploy anywhere
- No npm, no webpack, no React — nothing to break or update
- Easy to hand off, version, or fork

### Why Formspree over EmailJS?
- Formspree never requests OAuth access to your Gmail inbox
- EmailJS requires Gmail OAuth (send permission) — privacy concern
- Formspree just forwards to your email address like a postal service

### Why Vercel over Netlify?
- Both are free and excellent for static sites
- Vercel has faster global CDN for India-region visitors
- Auto-deploys from GitHub with zero configuration

### Why CSS variables for theming?
- Dark mode with zero JavaScript for color switching
- Just toggle `data-theme` on `<html>` — all colors update instantly
- Easy to reskin — change 10 variables, entire site recolors

### Why IntersectionObserver for scroll animations?
- No GSAP, no ScrollMagic, no AOS library needed
- Native browser API — zero performance cost
- Works on all modern browsers

### The cursor mobile bug fix
```css
/* WRONG — display:none still lets element exist in DOM */
@media(pointer:fine){ #cur{ display:block } }

/* RIGHT — cursor JS never runs on touch devices */
if(window.matchMedia('(hover:hover) and (pointer:fine)').matches){
  // all cursor code here
}
```

---

## 📦 Third Party Services Used

| Service | Purpose | Free Tier |
|---|---|---|
| Google Fonts | Playfair Display + Outfit fonts | Free |
| Formspree | Contact form email forwarding | 50/month |
| Vercel | Hosting + auto-deploy | Free |
| realfavicongenerator.net | Generated favicon package | Free |
| squoosh.app | Image compression | Free |

---

## 🔮 Future Improvements

- [ ] Add actual project screenshots to replace gradient thumbnails
- [ ] GitHub links on each project card
- [ ] Lighthouse Performance 85 → 90+ (serve WebP images)
- [ ] Add `<main>` landmark for better accessibility
- [ ] Consider adding a blog section (Hashnode or Dev.to embed)
- [ ] Custom domain (e.g. `amangupta.dev`)

---

## 👤 Author

**Aman Gupta**
B.Tech CSE — United College of Engineering and Research, Prayagraj (2023–2027)
📧 amangupta7203@gmail.com
🔗 [linkedin.com/in/amangdev](https://linkedin.com/in/amangdev)
🌐 [amanguptadevportfolio.vercel.app](https://amanguptadevportfolio.vercel.app)

---

*Built from scratch in one conversation. No templates, no frameworks, no shortcuts.*
