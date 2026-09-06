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

## Conventions

- **Update this CLAUDE.md in the same turn as any change to site behavior** — a
  new automation, a new page, a changed navigation pattern, whatever. Same rule
  the other three Claimek repos follow.
- Any content change that touches naming of third-party vendors (e.g. the AI
  provider) or links to the private product repos should stay generic — see
  "Before this goes live" in `README.md` for the reasoning already applied to
  `index.html`, `privacy.html`, and `terms.html`.
