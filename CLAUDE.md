# AI Video Automation — OPMEDIA

## Stack
- Higgsfield MCP (installed at https://mcp.higgsfield.ai/mcp)
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
