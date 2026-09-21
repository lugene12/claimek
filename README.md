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
├── start.html          # Quick start draft: gitignored and unlinked until its screenshots exist
├── changelog.html      # Release notes at /changelog, linked from every footer
├── style.css            # Shared stylesheet for all pages
├── favicon.svg           # Browser-tab icon, referenced at site root
├── assets/
│   ├── claimek-mark.svg              # Square mark, own dark rounded background baked in
│   ├── claimek-mark-transparent.svg  # Same mark, no background — for placing on other surfaces
│   ├── claimek-lockup.svg            # Full wordmark lockup (used in READMEs, decks, etc.)
│   ├── og-image.svg                  # Open Graph card source, 1200×630
│   ├── og-image.png                  # Rasterized OG card — what Facebook/Messenger/link
│   │                                   previews actually load; social crawlers don't render SVG
│   ├── hero-demo.png                 # Real capture of the extension, hero image above 680px
│   ├── demo-sourced.png              # Mockup: fact-checker-sourced flag card, 2560×1440
│   └── demo-automated.png            # Mockup: automated-check flag card, 2560×1440
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

Nothing is outstanding. Legal name (Lugene G. Luistro), contact/DPO email
(`lugene12@gmail.com`), jurisdiction city (Calamba City), the "Last updated" and
"Effective" dates, and the server-log-retention and minimum-age statements in
`privacy.html` are all filled in. No `[PLACEHOLDER]`-style spans remain, though
the `.placeholder` class stays in `style.css` for future drafts.

Every "Add to Chrome" button and footer link points at the published listing,
`https://chromewebstore.google.com/detail/ipkdkdedconlpipcabenngkbnaniocbk`. That
URL appears in `index.html`, `privacy.html`, `terms.html`, `start.html`,
`changelog.html`, and `404.html`, so changing it means changing all six.

## Hero demo

`assets/hero-demo.png` is a real capture of the extension running, shown in the
hero above 680px wide. Below that breakpoint it is hidden and the hand-built CSS
mockup in `index.html` (`.mobile-demo`) is shown instead, because the screenshot
is a 1280px-wide desktop browser window whose panel text is unreadable on a
phone. Both show the same idea, so if the product's UI changes, update both.

`index.html`'s "Under the hood" section deliberately stops at a high-level
architecture description and tech-stack chips, with no link out to source code.
The actual product implementation stays in separate, private repositories.
