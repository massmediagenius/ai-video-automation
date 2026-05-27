# AI Video Automation — OPMEDIA

## Stack
- Higgsfield MCP (installed at https://mcp.higgsfield.ai/mcp)
- Higgsfield CLI v0.1.40 at `~/.npm-global/bin/higgsfield`
- Claude Code as the orchestration layer
- GitHub for version control (auto-push on every big change)

## Project structure
- `briefs/` — campaign briefs (use template.md as starting point)
- `campaigns/` — one folder per campaign with prompt logs + output references
- `outputs/` — scored results, winners, links to generated assets

## How to run a campaign
1. Copy `briefs/template.md` → `briefs/[brand]-[date].md`, fill it out
2. Tell Claude: "Run the brief at briefs/[file].md"
3. Claude routes to Higgsfield MCP, generates content, scores with Virality Predictor
4. Winners land in `outputs/[campaign]/winners.md`

## Models reference
| Task | Model |
|------|-------|
| Hero editorial frames | Soul Cinema |
| UGC actor variations | Soul 2.0 |
| 1080p 9:16 video | Seedance 2.0 |
| Text-in-image / logos | Nano Banana Pro |
| Lip-sync / image-to-video | Kling 3.0 |
| Narrative video | Veo 3.1 |
| Virality scoring | Virality Predictor |

## Virality Predictor rules
- Always generate 3–5× more variations than needed
- Score everything in one batch
- Keep top 20% only
- Paid ads: ship 85+ scores only
- Organic: 70+ threshold

## Git
- Auto-push hook fires after every significant change (new campaign, new outputs, brief updates)
- Never commit raw video files (*.mp4, *.mov are gitignored)
- Commit output URLs/links as markdown files instead

---

## Session state — 2026-05-27

### What was completed this session
1. **Higgsfield MCP installed** — `claude mcp add --transport http --scope user higgsfield https://mcp.higgsfield.ai/mcp` — added to user-level Claude config (`~/.claude.json`). Verify with `claude mcp list`.
2. **Higgsfield CLI installed** — `npm install -g @higgsfield/cli` via `~/.npm-global`. Version 0.1.40. `~/.npm-global/bin` added to PATH in `~/.zshrc`.
3. **Project scaffolded** at `/Users/mcp/Documents/ai-video-automation/`
   - `.gitignore` — excludes .env, node_modules, raw video files
   - `CLAUDE.md` — this file
   - `briefs/template.md` — campaign brief template
   - `.claude/settings.json` — auto-push hook (Stop hook)
4. **GitHub repo created and pushed** — https://github.com/massmediagenius/ai-video-automation
5. **Auto-push hook wired** — `.claude/settings.json` Stop hook: on every Claude session end, if there are uncommitted changes → `git add -A` → commit with timestamp → `git push origin main`

### What still needs to be done (pick up here next session)
- [ ] **`higgsfield auth login`** — USER must run this in terminal (opens browser OAuth). Command: `higgsfield auth login`
- [ ] **Install Higgsfield skills into Claude Code** — `npx skills add higgsfield-ai/skills` (run after auth)
- [ ] **Run first test campaign** — create a brief in `briefs/`, tell Claude to run it, verify Higgsfield MCP responds
- [ ] Decide which client/brand to run the first real campaign for (MOTION, Kyle.teacher, or new client)

### Key decisions made
- Skipping Publer, Klaviyo, Motion, Shopify for now — just Higgsfield + Claude Code + GitHub
- No Vercel/Next.js needed for this project — pure automation pipeline
- Raw video files are gitignored; only output URLs/markdown files get committed

### Reference URLs
- GitHub repo: https://github.com/massmediagenius/ai-video-automation
- Higgsfield MCP docs: https://higgsfield.ai/mcp
- Higgsfield CLI docs: https://higgsfield.ai/cli
- Guide this was built from: Koda Academy "AI Content Farm System — Higgsfield MCP × Claude Code" by @timkoda_
