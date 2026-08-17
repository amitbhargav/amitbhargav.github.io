# amitbhargav.github.io

Personal portfolio site for **Amit Bhargav** — Technical Program Manager & Delivery Manager.
Single-page, single-file, zero build step. Deployed on GitHub Pages.

**Live:** https://amitbhargav.github.io

---

## What's in here

```
.
├── index.html   # the entire site — HTML, CSS, and JS in one file
└── README.md
```

That's it. No `npm install`, no framework, no build pipeline. Open `index.html` in a
browser and it works; push it to GitHub Pages and it's live.

## Sections

The page is a single-page app with client-side routing via `show(id)` — sections
never reload, they're `<div class="panel">` blocks toggled with a class:

| Panel | Content |
|---|---|
| Home | Headline, career snapshot, KPI band |
| Products | Yuktora & FirePathAI (live AI products) + flagship enterprise programs |
| Experience | Full work history timeline |
| Approach | "How I operate" principles + competency bars |
| Skills | Core competencies by category |
| Credentials | Certifications + education |
| Contact | Links, quick-info card |

Keyboard `←/→` or `↑/↓` also moves between sections. Every full page load (including
a browser refresh) always lands on Home — `panel-home` carries the `on` class in the
markup itself, and no "last viewed section" is persisted anywhere.

## Features

- **Single fixed accent theme** (bordeaux) — colors live as CSS custom properties in
  `:root` / `[data-theme="bordeaux"]`. There's no in-page switcher; to change the
  palette, edit the `--acc` / `--acc2` / `--acc3` values directly.
- **Animated KPI counters** and **competency bars** that run once per panel view.
- **Onboarding intro** — a full-screen greeter shown before the dashboard on a
  visitor's first load. A.I. types itself in, asks *"what brings you by today?"*,
  and reveals a 7-tile nav grid (one tile per section) with 1–2 tiles flagged
  "recommended" based on the visitor's answer (hiring / builder / just exploring).
  "Skip straight to the site" is always available. Shown once per browser session
  via `sessionStorage['ai_intro_seen']` — a fresh tab always sees it again.
- **A.I. — Amit Intelligence assistant** — a floating chat widget (bottom-right)
  that answers common recruiter questions (budgets, team size, AI products,
  certifications, availability) from a keyword-matched knowledge base baked into
  the page, with a typing-animation reply style and an enthusiastic voice.
  - 100% client-side, text-only — no API key, no backend, no external calls, no
    microphone/speech permissions — so it works everywhere with zero setup.
  - To extend it, add entries to the `JV_KB` array near the bottom of `index.html`
    — each entry is `{ k: [keywords], a: 'answer' }`.
- Fully responsive — sidebar collapses to a horizontal top nav under 860px.

## Updating content

Everything lives in `index.html`. A few anchor points if you're editing by hand:

- **Header/meta:** `<title>`, `<meta name="description">`, and the `og:*` tags at the top.
- **Experience timeline:** look for `<!-- EXPERIENCE -->`, one `.exp-row` per job.
- **Certifications:** look for `<!-- CREDENTIALS -->`, one `.cert` block per credential.
  New certs from LinkedIn can be added here in the same markup pattern.
- **A.I. assistant answers:** the `JV_KB` array in the `<script>` block.
- **Onboarding intro copy/routing:** the `INTRO_NAV` and `INTRO_REPLIES` objects,
  just above the `initIntro()` function.

Keep resume and site content in sync — the assistant widget's answers and the
Experience/Credentials panels are only as accurate as what's typed here.

## Deploying

This repo is already a GitHub Pages site (`https://amitbhargav.github.io`), so any
push to the default branch goes live automatically within a minute or two:

```bash
git add index.html
git commit -m "Update content"
git push
```

No Pages settings, Actions workflow, or build step required — GitHub serves the
root `index.html` directly.

## Local preview

```bash
# any static server works, e.g.
python3 -m http.server 8000
# then open http://localhost:8000
```

Or just double-click `index.html`. To re-see the onboarding intro during local
testing, open dev tools → Application → Session Storage → delete `ai_intro_seen`,
then refresh (or just use a fresh incognito/private tab).
