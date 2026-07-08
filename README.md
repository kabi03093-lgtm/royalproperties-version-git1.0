# Royal Properties — Website

> **This build has been audited and made GitHub-hosting-ready.** Every internal link, image reference, and asset path was checked (including case-sensitive path resolution, since GitHub Pages is case-sensitive unlike some local dev setups) — no broken links or missing files were found. Added for hosting: `.nojekyll`, `.gitignore`, and a GitHub Actions workflow (`.github/workflows/deploy.yml`) that auto-deploys to GitHub Pages on push. See "Deploying to GitHub Pages" below.

A complete, multi-page front-end website for **Royal Properties** (Kanchipuram), built around the brand on your business card and the page structure from your notes.

## What's included

All 13 public-facing pages, plus a demo admin panel:

- `index.html` — Home (hero, search, featured properties, why-us, stats, testimonials, blog, FAQ, map)
- `about.html` — About Us (story, MD profile, why-us, stats)
- `properties.html` — Full listings with location / type / budget / price filters and category chips
- `property-details.html` — Single property page (gallery, amenities, agent card, enquiry + site-visit form, related properties)
- `services.html` — Services offered + buying process
- `gallery.html` — Filterable image gallery with lightbox
- `testimonials.html` — Customer reviews
- `blog.html` + 6 full blog articles — buying guides, market watch, legal explainers
- `faq.html` — Accordion FAQ
- `contact.html` — Enquiry form, map, office details
- `privacy-policy.html`, `terms-conditions.html`, `404.html`
- `admin/login.html`, `admin/dashboard.html` — demo admin screens (manage properties, enquiries, site visits)
- `robots.txt`, `sitemap.xml`

## Structure

```
royal-properties/
├── index.html, about.html, properties.html, ... (all public pages)
├── css/
│   ├── style.css      ← core design system (colors, hero, cards, footer, etc.)
│   └── pages.css       ← inner-page additions (filters, gallery, admin, forms)
├── js/
│   └── main.js          ← nav, scroll reveal, FAQ accordion, filters, lightbox, demo forms
├── images/
│   └── favicon.svg
├── admin/
│   ├── login.html
│   └── dashboard.html
├── robots.txt
└── sitemap.xml
```

## How to view it

Just open `index.html` in a browser — no build step needed. To view it as a real site (so relative links behave exactly like production), run a local server from this folder, e.g.:

```
python3 -m http.server 8000
```
then visit `http://localhost:8000`.

## Deploying to GitHub Pages

This repo is ready to host as-is — everything is plain HTML/CSS/JS with relative links, so it works from a repo root or a project sub-path without changes.

1. Push this folder's contents to a GitHub repository (e.g. `royal-properties`), with `index.html` at the repo root.
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, choose one of:
   - **Deploy from a branch** → branch `main`, folder `/ (root)` — simplest option, no extra setup needed.
   - **GitHub Actions** — this repo already includes `.github/workflows/deploy.yml`, which builds and deploys automatically on every push to `main`. Select "GitHub Actions" as the source and the first push will deploy it.
4. Your site will be live at `https://<your-username>.github.io/<repo-name>/`.
5. A `.nojekyll` file is included so GitHub Pages serves the files as-is (skips Jekyll processing).

**Before going live, update the placeholder domain:**
`sitemap.xml` and `robots.txt` currently point to `https://www.royalproperties.com/`. Once you know the final domain (a custom domain or your `github.io` URL), update the `<loc>` entries in `sitemap.xml` and the `Sitemap:` line in `robots.txt` to match.

## What's real vs. demo right now

This is a **front-end only** build — every page, form and layout you asked for is here and fully responsive, but there's no backend yet. Specifically:

- **Forms** (enquiry, site visit, contact, newsletter) show a confirmation toast but don't save data anywhere yet.
- **Admin login/dashboard** are visual mockups with sample data — there's no real authentication or database behind them.
- **Search/filter** on the properties page filters the 9 sample listings client-side; a real version needs a database of listings.

## Turning this into the full production system

Your original brief also specced a full **Java 21 + Spring Boot + MySQL** backend (REST APIs, Spring Security with BCrypt, role-based auth, property/enquiry/gallery/blog management, image upload, pagination/search/filtering) — that's a separate, much larger backend project (proper folder structure, entities, DTOs, controllers, services, repositories, security config, database schema, deployment). It's genuinely a multi-week build for a real production system, not something to compress into one pass.

Good next step: pick **one vertical slice** first — e.g. "Properties" (entity → repository → service → REST API → connect the properties.html page to real data) — and I'll build that end-to-end with you, then repeat for enquiries, site visits, gallery, blog, and admin auth. That gets you something testable early instead of a huge pile of untested code at once. Just say the word and we can start on the database design + Spring Boot skeleton.
