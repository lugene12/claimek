# claimek.com

Marketing and legal site for [Claimek](https://claimek.com), a free Chrome extension
that reads YouTube captions in real time, flags claims worth checking, and shows
what fact-checking groups have already said about them (English, Filipino, and
Taglish). The product itself lives elsewhere — this repo is just the public
marketing/legal site.

Static HTML/CSS, no build step, no framework, no `package.json`. Deployed as-is via
GitHub Pages.

## Structure

```
claimek/
├── index.html         # Landing page — product pitch, how it works, privacy summary
├── privacy.html        # Privacy Policy
├── terms.html          # Terms of Service
├── 404.html            # Custom not-found page (served automatically by GitHub Pages)
├── style.css            # Shared stylesheet for all pages
├── favicon.svg           # Browser-tab icon, referenced at site root
├── assets/
│   ├── claimek-mark.svg              # Square mark, own dark rounded background baked in
│   ├── claimek-mark-transparent.svg  # Same mark, no background — for placing on other surfaces
│   ├── claimek-lockup.svg            # Full wordmark lockup (used in READMEs, decks, etc.)
│   ├── og-image.svg                  # Open Graph card source, 1200×630
│   └── og-image.png                  # Rasterized OG card — what Facebook/Messenger/link
│                                       previews actually load; social crawlers don't render SVG
├── CNAME                # Custom domain pin for GitHub Pages (claimek.com)
├── robots.txt
└── sitemap.xml
```

Every page links the same `favicon.svg` at `/favicon.svg` and the same brand assets
under `/assets/` — keep new assets there rather than at the repo root.

## Navigation anchors

The nav's "How it works" and "Under the hood" links point at sections that only
exist on the landing page (`#how`, `#build`). On `index.html` they're plain
same-page anchors; on every other page (`privacy.html`, `terms.html`, `404.html`)
they're `/#how` and `/#build` so they route back to the landing page first. If a
new sub-page is added, its nav must use the `/#…` form — a bare `#…` anchor from a
sub-page silently does nothing, since the browser looks for the section on the
current page instead of navigating home.

## Deployment

Pushing to `main` publishes directly via GitHub Pages — there is no CI step and no
build. The `CNAME` file pins the custom domain (`claimek.com`); removing it would
fall back to the default `*.github.io` URL. `404.html` is served automatically by
GitHub Pages for any unmatched path, so it needs no routing configuration.

## Before this goes live

Legal name (Lugene G. Luistro), contact/DPO email (`lugene12@gmail.com`),
jurisdiction city (Calamba City), and the "Last updated"/"Effective" dates are
filled in. The following still need real answers before launch — search for
`[PLACEHOLDER]`-style spans (dashed underline via the `.placeholder` class in
`style.css`) to find them:

- **Server log retention** and **minimum-age statement** — flagged inline in
  `privacy.html §5` and `§7` as needing confirmation from whoever owns the
  server-side logging config once the backend has a real deployment target
  (nothing is deployed yet, so there's no retention policy to state honestly).
- **Chrome Web Store links** — every "Add to Chrome" button and the footer link
  currently point at the generic `chromewebstore.google.com` root rather than the
  live listing URL.

`index.html`'s "Under the hood" section deliberately stops at a high-level
architecture description and tech-stack chips, with no link out to source code.
The actual product implementation stays in separate, private repositories.
