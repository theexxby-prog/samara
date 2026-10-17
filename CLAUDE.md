# samara

Samara's one-page portfolio site. The whole site is `index.html`, with inline CSS and no
build step.

| | |
|---|---|
| Live | https://samara.mehtahouse.cc |
| GitHub | theexxby-prog/samara (public) |
| Mac folder | ~/dev/samara |
| Deploys by | push to `main`. Cloudflare Workers Builds builds and deploys every push. No manual `wrangler deploy` |
| Cloudflare | Worker `samara`, static assets only (`assets.directory` is the repo root). No D1, R2, KV or DO |
| Read also | none |

## Rules
- A push to `main` is a production deploy. There is no staging step.
- The Worker serves the repo folder itself as the website. Anything in the folder is
  public unless `.assetsignore` lists it. Add every new non-site file (docs, config,
  scripts) to `.assetsignore` in the same commit. It already covers `.git`, the
  config files, `.claude` and `CLAUDE.md`.
- Don't run `wrangler deploy` by hand. Workers Builds owns the deploys, and a manual
  deploy from a stale copy would overwrite the live site.
- This is not Samara's rent and utility portal. That is the separate repo
  `rent-utility-tracker` (house.mehtahouse.cc).
- The repo is public. Nothing personal goes in it beyond what the site already shows.

## Session handoff (every session, on any device)

Vishal works on this repo from the Mac terminal, the Claude desktop and phone apps, and
cloud sessions at claude.ai/code. A cloud session sees only this repo, not the Mac's
`~/.claude` files or memory. So anything the next session needs goes in this file, and
`main` on GitHub is the single source of truth.

**Start**
1. The SessionStart hook (`.claude/hooks/session-start.sh`) prints a sync report. If it
   says this copy is behind, run `git pull --ff-only` before touching anything. If it
   lists another branch or an open PR, tell Vishal and ask whether to merge it first.
2. Read **Current state** at the bottom of this file.

**Finish** (every session that changed anything, before saying you're done)
1. Rewrite **Current state**: the date, where you worked (Mac, cloud or phone), what
   changed, what is live, what isn't deployed or tested yet, and what's next. Keep it
   short and current, not a diary: the `_Updated …_` line is always the first line and is
   rewritten every time; the section stays under about 25 lines; anything older than the
   last two sessions moves to `CHANGELOG.md` (or is deleted; git has it). Lasting rules
   and lessons go in the sections above it.
2. Get the work onto `main`:
   - Mac: commit and `git push origin main`.
   - Cloud: you can push only your own `claude/...` branch. Push it, then
     `gh pr create --fill` and `gh pr merge --squash --delete-branch`, unless Vishal
     asked to review first.
3. If it needs a deploy you couldn't run (cloud sessions can't reach Cloudflare), list
   it under "Not deployed yet" so the next Mac session ships it.

## Current state
_Updated 2026-10-17 from the Mac (hiring extras added to the live look; round-3 structures rejected)._
- **Live:** the "A1 Clinic" look Samara chose after two Lab rounds (name-first hero, one italic
  line, bone/forest/copper, Fraunces + Inter, her cutout `photo.webp` on a sage-to-forest
  gradient, motion throughout, all off under `prefers-reduced-motion`). Added 2026-10-17:
  - **For hiring managers** panel in Contact: available from May 2027, any day of the week,
    commute up to about 40 minutes from Jersey City, certifications, languages, resume link.
  - **Resume (PDF)**: `Samara-Mehta-Resume.pdf`, the Sept 2026 resume with the phone number
    redacted (PyMuPDF redaction, text really removed). Linked from the hero, the nav, the
    hiring panel and a third contact card. Regenerate from a new resume by redacting the
    phone again; never commit the version with the phone.
  - **Link preview**: `og.jpg` (1200x630, her photo, name and line, made with Pillow from
    `photo.webp` and the Google-hosted Fraunces/Inter TTFs), `favicon.svg`, `favicon-64.png`,
    `apple-touch-icon.png`, Open Graph and Twitter meta, canonical URL.
  - **Line icons** (inline SVG `<symbol>` sheet at the top of `<body>`, `.ico` class) replace
    every emoji. Add new icons to the sheet; never put emoji back.
  - **Hidden, ready to publish:** `#hours` (clinical observation hours table per setting)
    and `#references` (two supervisor quotes). Both carry a `hidden` attribute and TODO text.
    When Samara supplies the numbers, names and quotes (with permission), fill them in and
    remove `hidden`; add nav links if wanted.
- **Design history:** artifacts "Samara Opening Lab" (round 1), "Samara Opening Round 2"
  (picks: A1, headline H3) and "Samara Site Round 3" (four whole-site structures: Card,
  Dossier, Story, Board). Vishal rejected all four round-3 structures on 2026-10-17; keep the
  existing page structure and the A1 look. Don't revert to the earlier teal or coffee pages.
- **Content source of truth:** Samara's resume "Samara Mehta - Resume (Sept 2026)". Don't
  invent numbers or roles. Email is samara.mehta@gmail.com (never samara@mehtahouse.cc).
- **Photo:** originals in `~/Downloads/Samara-Mehta-headshot-4x5-transparent.png` (and the
  grey-background JPG). Regenerate with `cwebp -q 86 -alpha_q 90 -exact -m 6 <png> -o photo.webp`.
  The hero falls back to "SM" initials if the image is missing.
- **Left off the public site on purpose:** phone number (also stripped from the PDF).
- **Still to confirm with Samara:** "Expected graduation 2027", the LinkedIn link
  `linkedin.com/in/samara-mehta`, certification expiry dates, observation hours per setting
  with supervisor names, reference quotes, part-time availability before May 2027.
- **Local preview:** `samara-site` in `~/dev/.claude/launch.json` (python http.server on this
  folder, port 8765). Tested desktop 1024 and phone 375 widths on 2026-10-17.
- **Not deployed yet:** nothing.
