# CLAUDE.md — AceTV+ Website Build Runbook

This file is the build spec for Claude Code. Read it fully before acting, then execute the steps in order.

## What this project is

AceTV+ is a media network landing site. The flagship vertical is sports (AceTV+ Sports), with screen and comedy shown as the expanding network. The entire site is a single static `index.html` file. There is no framework, no bundler, and no build step. Everything (HTML, CSS, JS) lives inline in `index.html`.

Do not refactor, rewrite, or "improve" the markup or styles. The design is approved. Your only job is to get it into version control and onto Vercel with a shareable preview link.

## Objective

1. Put this project under git.
2. Create a GitHub repository named `acetv` in the user's PERSONAL account (not an organization). Public.
3. Deploy to Vercel as a project named `acetv`.
4. Return the live preview URL so the user can share it with his brother for review.

## Prerequisites (verify, do not assume)

Run these checks first. If any fail, tell the user exactly what to authenticate and stop.

```bash
gh auth status        # GitHub CLI must be logged in
vercel whoami         # Vercel CLI must be logged in
git --version
```

If `gh` or `vercel` is not installed:
```bash
# GitHub CLI: https://cli.github.com
# Vercel CLI:
npm i -g vercel
```

## Project files (already present in this folder)

- `index.html` — the complete site (do not edit)
- `vercel.json` — static hosting config
- `README.md` — repo readme
- `.gitignore`
- `CLAUDE.md` — this file

## Build steps

### 1. Initialize git and commit

```bash
git init
git add .
git commit -m "AceTV+ Sports site: initial build"
git branch -M main
```

### 2. Create the GitHub repo in the PERSONAL account

Important: this must land in the user's personal account, NOT an org. Do not pass an org owner. Confirm the target account first:

```bash
gh api user --jq .login        # prints the personal username; the repo must be created under THIS account
```

Then create and push. The `--source=.` plus no `OWNER/` prefix creates it under the authenticated personal user:

```bash
gh repo create acetv --public --source=. --remote=origin --push --description "AceTV+ Sports — the future of sports media. We're all we got."
```

If `gh` reports the name is taken on the personal account, use `acetv-site` and tell the user the repo name had to change.

Verify it is personal, not org:
```bash
gh repo view --json owner,nameWithOwner --jq '.nameWithOwner'   # should be <personal-username>/acetv
```

### 3. Deploy to Vercel as project `acetv`

This is a static site. Framework preset is "Other", no build command, output is the repo root.

```bash
vercel link --yes --project acetv        # creates/links a Vercel project named acetv
vercel deploy --prod --yes               # production deploy
```

If prompted for settings, use:
- Framework Preset: Other
- Build Command: (leave empty)
- Output Directory: (leave empty / root)
- Root Directory: ./

Capture the production URL that `vercel deploy --prod` prints.

### 4. Return the result

Print a short summary with:
- The GitHub repo URL (`https://github.com/<username>/acetv`)
- The Vercel production URL (the link to send to the brother)
- The Vercel project dashboard URL

## Acceptance criteria

- [ ] `index.html` is unchanged from what was provided
- [ ] Repo `acetv` exists under the personal GitHub account, is public, and `main` is pushed
- [ ] Vercel project `acetv` is connected to the repo and a production deploy succeeded
- [ ] A working preview URL is returned that loads the site (intro animation plays, hero reads "LOVE THE GAME. NOT THE NOISE.")

## Notes for later (do NOT block the deploy on these)

These are placeholders in `index.html` to swap once the user has real values. Leave them as-is for now:
- `GTM-XXXXXXX` — Google Tag Manager container ID
- Email capture in the `cap()` function — needs a Beehiiv endpoint via an n8n webhook
- `youtube.com/@acetv`, Instagram, TikTok, Discord links — placeholders
- `press@acetv.plus` / `hello@acetv.plus` — placeholder inboxes
- Media kit download — needs the actual PDF

## Hard rules

- Do not edit `index.html` content, copy, or styles.
- Do not create the repo under any organization. Personal account only.
- Do not add a build step, framework, or dependencies. It is a static file.
- Do not use em-dashes or en-dashes in any commit message, README, or output.
