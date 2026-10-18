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
_Updated 2026-10-17 (evening) from the Mac: phone layout fixes and a designed resume PDF._
- **Live:** the "A1 Clinic" look (name-first hero, bone/forest/copper, Fraunces + Inter, cutout
  photo on a sage-to-forest gradient, motion throughout) plus the hiring extras another session
  added the same day (hiring-manager panel, link preview `og.jpg`, favicons, inline SVG line
  icons, hidden-until-ready observation-hours and references sections).
- **Phone (this session):** photo comes first at 250px with one badge (ring and second badge
  hidden), stats in a 2x2 grid, and a hamburger menu (`.nav-toggle` + `#menu` overlay with
  staggered Fraunces links). Tested at 375px: no horizontal scroll, menu opens, closes, jumps.
- **Resume PDF:** `Samara-Mehta-Resume.pdf` is now the designed one-page resume generated from
  `resume-src/resume.html` with headless Chrome (see `resume-src/README.md`). `resume-src` is in
  `.assetsignore` so only the PDF is served. No phone number in it. Includes availability
  (from May 2027, all seven days, ~40 min commute).
- **Resume link appears once only** (Vishal, 2026-10-17): the contact card beside Email and
  LinkedIn. Not in the nav, phone menu, hero or hiring panel.
- **Content source of truth:** the Sept 2026 resume; email samara.mehta@gmail.com only.
- **Photo:** originals in `~/Downloads/Samara-Mehta-headshot-4x5-transparent.png`; regenerate
  `photo.webp` with `cwebp -q 86 -alpha_q 90 -exact -m 6 <png> -o photo.webp`.
- **Design history:** artifacts "Samara Opening Lab" (round 1), "Samara Opening Round 2",
  "Samara Site Round 3" (four structures, all rejected; extras folded into the live site).
- **Still waiting on Samara:** observation hours per setting, certification expiry dates, one
  reference quote (unhide the hours and references sections when they arrive); confirm
  "Expected graduation 2027" and the LinkedIn link.
- **Local preview:** `samara-site` in `~/dev/.claude/launch.json` (port 8765).
- **Not deployed yet:** nothing.
