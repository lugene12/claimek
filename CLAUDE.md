# Claimek — Info Site

Public marketing/legal site for Claimek, deployed via GitHub Pages at
[claimek.com](https://claimek.com). Static HTML/CSS, no build step, no framework,
no `package.json`. See `README.md` for file structure, deployment, and the
placeholders still open before launch.

The product itself (the Chrome extension and its backend) lives in separate,
private repositories — this repo intentionally never names or links them. See
the "Before this goes live" note in `README.md` and the "Under the hood" section
of `index.html` for how that boundary is kept.

## Automation

**A git hook auto-bumps the "Last updated" date in `privacy.html` and
`terms.html`.** `.git/hooks/pre-commit` checks whether either file is staged in
the commit; if so, it rewrites that file's "Last updated" date to today and
re-stages it before the commit completes. `privacy.html`'s "Effective" date is
left untouched — only "Last updated" is automatic, since "Effective" marks when
a specific revision took effect, not when it was last touched.

This is why editing either file and committing is enough — there's no need to
hand-edit the date, and doing so manually will just get overwritten by the hook
to the actual commit date anyway.

**This hook is local-only.** `.git/hooks/` is never tracked or pushed by git, so
a fresh clone of this repo (a new machine, a CI runner, anyone else checking it
out) won't have it. If that ever matters, the fix is to either commit the script
elsewhere in the repo (e.g. `scripts/pre-commit`) with a setup note in `README.md`
telling people to symlink/copy it into `.git/hooks/`, or migrate to a tracked hook
manager — neither has been done, since today this is a solo repo on one machine.

## The quick start page

**Status: draft, not published (2026-09-21).** The page is written but its three
screenshots aren't captured yet, so it is held back rather than shipped with
placeholder images. `.gitignore` keeps `start.html` and `assets/step-*.png` out
of every commit, and all links to it were removed. To publish: capture the
screenshots over the placeholders, delete those two `.gitignore` lines, re-add
`<a href="/start">Quick start</a>` as the first link in the footer of
`index.html`, `privacy.html`, `terms.html`, `404.html`, and `changelog.html`,
restore the one-sentence pointer to it at the end of the "How it works" section,
and put `/start` back in `sitemap.xml`. The CSS (`.gstep` and friends, plus
`.meter-note a`) was left in place, so nothing there needs restoring.

`start.html` at `/start` is the onboarding guide. **It is deliberately not in the
top nav.** A visible "Tutorial" link tells a visitor the product needs learning,
which contradicts the "Nothing to configure" promise in the hero and costs
installs. It is linked from every page footer and from the end of the "How it
works" section, so it is found after interest exists, not before.

Its job is to defuse the four moments that read as "broken" and cause uninstalls:
a video with no captions, a skipped category, a tab that was open before install,
and a paused check. Each is framed as expected behaviour with the panel naming it,
never as the user's mistake. The page also states up front that a quiet panel is
the good outcome, which is the same empty-state reasoning the extension's own
panel copy follows. Keep that framing if you edit it.

`assets/step-1-install.png`, `step-2-panel.png`, and `step-3-captions.png` are
placeholders rendered from inline SVG, sized 1280x420 and 1280x620. Real captures
overwrite them at the same filenames, so no markup changes.

## Hero demo and store links

**The hero carries two demos, and both have to stay true.** `assets/hero-demo.png`
is a real screenshot of the extension running, shown above 680px wide. Below that
the CSS mockup in `index.html` (`.mobile-demo`) takes over, because the screenshot
is a 1280px-wide desktop window whose panel text is unreadable on a phone. A change
to the product's UI makes both stale, not just one.

**The published listing URL is repeated in four files** — `index.html`,
`privacy.html`, `terms.html`, and `404.html` — as
`https://chromewebstore.google.com/detail/ipkdkdedconlpipcabenngkbnaniocbk`.
There's no shared include, so changing it means changing all four.

## Release notes

`changelog.html` (`/changelog`) is the public, user-facing record of what each
extension release changed, linked from every footer alongside a `Contact` mailto.
It exists because a fact-checking tool is judged on whether anyone is still
minding it, and a dated list of fixes is the cheapest proof there is. That cuts
both ways: **a changelog whose newest entry is months old reads as abandoned,
which is worse than not having the page** — so add an entry whenever users would
notice a change, and skip releases they would not.

**The trigger is the extension's zip build, not the release going live.** Owner's standing instruction (2026-09-20): building a submission zip bumps `manifest.json`'s version *and* adds that version's entry here, in the same turn, before the zip is handed over. Waiting until approval means writing the entry from memory days later.

Three rules for entries:
- **Plain language, user's point of view.** What they will see differently, never
  prompt wording, selectors, or internals a competitor would find useful.
- **Own the mistakes.** "We flagged some correct figures as misleading. Fixed."
  A checker that admits its own errors gains more credibility than it loses.
- **Never announce an unapproved build as shipped.** Chrome reviews every update,
  so a new version sits under a "Submitted for review" line until it is live.

Server-side changes (backend prompts, scoring) carry no extension version, so give
them their own dated entry when they deploy, rather than folding them into a
version the user's Chrome has not received.

## Conventions

- **Update this CLAUDE.md in the same turn as any change to site behavior** — a
  new automation, a new page, a changed navigation pattern, whatever. Same rule
  the other three Claimek repos follow.
- Any content change that touches naming of third-party vendors (e.g. the AI
  provider) or links to the private product repos should stay generic — see
  "Before this goes live" in `README.md` for the reasoning already applied to
  `index.html`, `privacy.html`, and `terms.html`.
