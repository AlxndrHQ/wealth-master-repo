# Wealth Master Repo — control center

## Shared context (read first)
This project's current state and decision log live in Google Drive, shared with Gemini:
**AI Collaboration › Claude Projects › Wealth Master Repo**
- **Wealth Master Repo · Summary**: what it is, links, current state, open items. Read before working; rewrite it in place when the state changes.
- **Wealth Master Repo · Decisions**: newest-first log of what was decided and why. Add an entry (date · decision, then Why / Rejected / Revisit if / Decided by) whenever something is decided; never edit old entries.
- **Discussions/** and **Assets/** in that folder hold research, chat exports and files.
The folder's "00 Index" explains the system. Code stays here and on GitHub; the "why" lives in Drive.

This repo is two things:
1. **The master index** (`index.html`, live at https://alxndrhq.github.io/wealth-master-repo/): a front door that links to every project.
2. **The place to give update requests.** When the user asks for a change ("update X on Y", "add Z to all the sites"), go into the right project folder(s), make the change, commit, push, and confirm the live site updated.

## Projects

All folders are siblings of this one, under `/Users/stevenjr./Documents/Documents - Steven's M4P/`. Repos are under github.com/AlxndrHQ, and Pages are at `https://alxndrhq.github.io/<repo>/`.

| Site | Local folder | Repo | How it builds and deploys |
|---|---|---|---|
| Algos & Capital (flagship) | `Historical Wealth Mind Map` | historical-wealth-mind-map | Static `index.html` + `data.json`, published from `main` |
| Old Money | `European Wealth` | european-wealth-map | Static; see `European Wealth Handoff.md` |
| The Triangle Trade | `Slavery Web` | triangle-trade-mind-map | Static; `index.html` embeds a copy of `data.json`, so keep both in sync |
| HBCU Legacy Web | `HBCU Legacy Web` | hbcu-legacy-mind-map | Edit `sources/*.json`, then run `python3 tools/build.py` (never hand-edit `data.json`) |
| Black Business Directory | `Black Business Directory /black-business-directory` (the outer folder name has a trailing space and is not a repo) | black-business-directory | Static; data is embedded between `/*DATA-START*/` and `/*DATA-END*/` in `index.html`, plus `places.json` |
| Ground Truth | `Real Estate Map` | pg-county-land-map | GitHub Actions deploys only `web/`. Read its `CLAUDE.md` and `HANDOFF.md` first |
| Semiconductor Earnings | `Semiconductor Earnings Discussion` | Semiconductor-Earnings-Discussion | Vite + React + Tailwind. Actions runs `npm ci && npm run build` and deploys `dist/`. The Finnhub key is in the repo secret `VITE_FINNHUB_KEY`. Automated, see below |

The six D3 sites share one design system (Iowan serif, JetBrains Mono, bronze accent, `theme` localStorage key). A change to shared style or the header should usually go to all six. The semiconductor site has its own dark, Obsidian-style design.

## Automation (Semiconductor Earnings)

- **Every night at 07:00 UTC (GitHub Action, `deploy.yml`):** `scripts/update-earnings.mjs` pulls each company's latest EPS and revenue against estimates, plus its next report date, from Finnhub into `src/data/live-earnings.json`. If the file changed, it commits as `github-actions[bot]` and redeploys. SK Hynix and Nanya aren't on Finnhub's free plan.
- **Every Friday at 23:00 UTC (Claude routine, Opus, https://claude.ai/code/routines/trig_01LB8jrTEUSxBab7cxk2FQCa):** rewrites the `earnings` write-ups in `companies.js` for companies that reported a new quarter, updates confirmed report dates, and pushes to `main`.
- Both commit to `main`, so always `git pull --rebase` before pushing there. Never hand-edit `live-earnings.json`.

## How to make updates

- Read the target project's README and any `CLAUDE.md` or handoff notes before editing.
- Run `git status` first. If there are uncommitted changes you didn't make, don't sweep them into your commit. Tell the user, and ask whether to include them.
- Use one commit per project, and keep the message specific to that project.
- After pushing, wait for the Pages build to finish and check that the live URL returns 200.
- When a project is added, renamed or removed, update the `GROUPS` array in `index.html` and the table in `README.md` here.
- For a multi-site change, report the result per site: what changed, the commit, and live or not.
