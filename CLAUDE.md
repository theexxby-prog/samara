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
_Updated 2026-10-17 from the Mac (opening rebuilt from Samara's final picks; photo added)._
- **Live:** the "A1 Clinic" look Samara chose after two Lab rounds: hero with her name as
  the headline, one italic line ("Kinesiology student at UMass Amherst. Certified EMT."),
  bone/forest/copper palette, Fraunces + Inter, her cutout photo (`photo.webp`, 116 KB,
  transparent, 1200x1500) on a sage-to-forest gradient in a rounded frame with two floating
  badges and a copper ring. Motion: staggered hero entrance, drifting blobs, count-up
  numbers, highlight-swipe on the role line, pointer tilt on the photo (mouse only),
  nav shrink on scroll, scroll reveals, timeline line that draws itself, hover lifts on
  every card. All of it is off under `prefers-reduced-motion`.
- **Content source of truth:** Samara's resume "Samara Mehta - Resume (Sept 2026)". Don't
  invent numbers or roles. Email is samara.mehta@gmail.com (never samara@mehtahouse.cc).
- **Photo:** original files in `~/Downloads/Samara-Mehta-headshot-4x5-transparent.png` (and
  the grey-background JPG). Regenerate `photo.webp` with
  `cwebp -q 86 -alpha_q 90 -exact -m 6 <png> -o photo.webp`. The hero falls back to "SM"
  initials if the image is missing.
- **Design history:** Claude artifacts "Samara Opening Lab" (round 1: A Clinic, B Bold, C
  Minimal, D Soft) and "Samara Opening Round 2" (A1, A2, C1, C2 + headline list). Picks:
  A1 everything, headline H3. Keep the look; don't revert to the earlier teal or coffee pages.
- **Availability (Vishal, 2026-10-17):** from summer 2027 (school ends May 2027) she is free
  all seven days; commute up to 30 minutes, 35-40 is fine. Shown as three pills in the
  contact section. Still unknown: part-time availability before May 2027.
- **Left off the public site on purpose:** phone number, resume PDF.
- **Still to confirm with Samara:** "Expected graduation 2027" and the LinkedIn link
  `linkedin.com/in/samara-mehta`.
- **Local preview:** `samara-site` in `~/dev/.claude/launch.json` (python http.server on
  this folder, port 8765). Tested desktop 1280 and phone 375 widths on 2026-10-17.
- **Not deployed yet:** nothing.
