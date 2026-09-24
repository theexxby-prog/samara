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
   short and current, not a diary. Lasting rules and lessons go in the sections above it.
2. Get the work onto `main`:
   - Mac: commit and `git push origin main`.
   - Cloud: you can push only your own `claude/...` branch. Push it, then
     `gh pr create --fill` and `gh pr merge --squash --delete-branch`, unless Vishal
     asked to review first.
3. If it needs a deploy you couldn't run (cloud sessions can't reach Cloudflare), list
   it under "Not deployed yet" so the next Mac session ships it.

## Current state
_Updated 2026-09-24 from the Mac (housekeeping session: added this handoff setup)._
- **Live:** the April 2026 portfolio design. `.assetsignore` (2026-09-22) is working:
  `/wrangler.jsonc`, `/.gitignore` and `/.git/HEAD` all return 404 on the live site.
- **Not deployed yet:** nothing. This commit only adds docs and the hook, and they are
  kept off the site by `.assetsignore`.
- **Open / next:** nothing pending.
