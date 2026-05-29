# Kabelo's Tasty Bakery

Marketing website for **Kabelo's Tasty Bakery**, a home bakery in Centurion, South Africa,
specialising in custom cakes, cupcakes, scones, biscuits and other homemade treats.

It is a lightweight, dependency-free static site: one HTML file, one stylesheet and one
JavaScript file. Navigation between Home, Gallery, About and Contact is handled client-side
with hash routing (`#home`, `#gallery`, `#about`, `#contact`), so the whole experience loads
as a single page. Orders are placed through WhatsApp.

## Project structure

```
.
├── index.html          # All four views (Home, Gallery, About, Contact)
├── css/styles.css      # All styling + responsive + accessibility layer
├── js/main.js          # Routing, mobile menu, hero carousel, gallery masonry, contact->WhatsApp
├── assets/
│   ├── banners/        # Hero slides + page-hero backgrounds (WebP)
│   ├── gallery/        # Gallery photos (optimised JPEG)
│   ├── icons/          # SVG icons
│   ├── logo/           # Logo (WebP) + favicon-96.png
│   ├── products/       # Signature product images (WebP)
│   └── og-image.jpg    # 1200x630 social-share preview image
├── netlify.toml        # Publish dir + caching + security headers
├── robots.txt
└── sitemap.xml
```

## Run locally

No build step or dependencies are required. Serve the folder with any static server, e.g.:

```bash
# Python
python3 -m http.server 8080

# or Node
npx serve .
```

Then open <http://localhost:8080>. (Opening `index.html` directly via `file://` also works,
but a local server is recommended so relative asset paths behave like production.)

## Deploy (Netlify)

1. Connect this repository to Netlify (or drag-and-drop the folder).
2. No build command is needed. Publish directory is the repo root (set in `netlify.toml`).
3. After the first deploy, update the placeholder domain (see below).

## Before going live — update the domain

A placeholder domain (`https://kabelostastybakery.co.za/`) is used in a few places.
Replace it with your real deployed URL in:

- `index.html` — `<link rel="canonical">`, Open Graph / Twitter `og:url` & `og:image`,
  and the JSON-LD `url`/`image`
- `robots.txt` — `Sitemap:` line
- `sitemap.xml` — `<loc>`

## Image optimisation

Photos were converted to WebP and resized to display dimensions; gallery JPEGs were
recompressed. If you add new images, optimise them before committing. A convenient option:

```bash
# WebP from a PNG/JPG, resized to a sensible max width
npx --yes sharp-cli -i input.png -o output.webp resize 1280 -- webp --quality 80
```

Keep hero/product images around 700-1280px wide and gallery photos around 900px wide.

## Accessibility & performance notes

- Visible keyboard focus, a skip-to-content link, and `prefers-reduced-motion` support are included.
- The hero carousel pauses on hover/focus and when the browser tab is hidden.
- Images use `width`/`height` to avoid layout shift and `loading="lazy"` below the fold.
