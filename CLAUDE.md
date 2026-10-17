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
_Updated 2026-10-17 from the Mac (rebuilt the site around the Sept 2026 resume)._
- **Live (once Workers Builds finishes this push):** the clinical/kinesiology version of the
  site. The old April 2026 page was a coffee-shop themed barista portfolio (CAFE'INN); every
  section was rewritten from the Sept 2026 resume: hero (pre-DPT, EMT-B, entry-level clinical
  role), about, experience (Nee's PT aide, NUMC EMT intern, LIU athletic training; The Works
  Cafe demoted to one line), skills, a new leadership section, education with coursework,
  contact (email + LinkedIn only; GitHub card removed). Palette moved from espresso/caramel to
  teal/ink; fonts (Playfair Display + Inter) and layout structure kept.
- **Source of truth for content:** Samara's resume, "Samara Mehta - Resume (Sept 2026)". When
  she sends a new one, update the site from it; don't invent numbers or roles.
- **Deliberately left off the public site:** her phone number and the resume PDF (the PDF
  carries the phone). Add a resume download only if Samara wants it public.
- **Assumptions to confirm with Samara:** "Expected graduation 2027" (Vishal's words, not on
  the resume); LinkedIn link is the resume's `linkedin.com/in/samara-mehta` (the old site used
  `samara-mehta-13272528a`); email stays `samara@mehtahouse.cc` (resume lists her gmail).
- **Local preview:** `python3 -m http.server` on the folder (registered as `samara-site` in
  `~/dev/.claude/launch.json`); tested desktop and 375px phone widths on 2026-10-17.
- **Not deployed yet:** nothing after this push.
- **Open / next:** confirm the three assumptions above with Samara; a Samara-approved photo
  for the hero would help.
