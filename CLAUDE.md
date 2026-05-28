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

## Trained Soul Avatars

| Name | Soul ID | Type | Training images | Status | Notes |
|------|---------|------|-----------------|--------|-------|
| LILY | `99c033cb-fbcc-4dfd-9cc0-5f1340b5eaf0` | soul_2 | 18 Miami penthouse shots | **ready** | Platinum blonde, petite curvy, reference: `4e8c164e-91bc-4679-ae39-f2e0b927d261` |

### LILY — training image job IDs (18 images)
Kitchen (beige leggings + sports bra): `39ee7285`, `d256abf8`, `7695e4e5`, `6b57e292`
Balcony (white denim shorts + tank): `ab008b9c`, `7c4dbe2b`, `c9933373`
Bedroom (sage green bralette + shorts): `20d32526`, `4d899c6f`, `c568bf37`
Window sill (chocolate brown tights): `70fb3135`, `04cca573`, `2e54b59e`
Living room (black biker shorts + white crop): `3c2bba1b`, `0343d3eb`, `ec0c5456`, `3e9746c8`
Dining area (caramel brown set): `dae423e4`

> Once LILY is `ready`, use her with: `generate_image(model='soul_2', soul_id='<LILY_soul_id>', prompt='...')`
> Or video: `generate_video(model='soul_cinema_studio', soul_id='<LILY_soul_id>', prompt='...')`

---

## Completed Campaigns

### MOTION Limitless Pouches — Blue Raspberry UGC (2026-05-27)
- **Brief:** `campaigns/motion-ugc-bluerazz/`
- **Winners:** `campaigns/motion-ugc-bluerazz/winners.md`
- **Product media_id:** `f16e0790-895b-4536-9cd5-d201fcba84ff`
- **Product image media_id:** `4f973707-9a4c-4f83-aaca-2e605c1109c5`
- Erik (male) CDN: `hf_20260527_214845_d77412e7-dd38-459c-8e19-482875db0925.mp4`
- Adriana (female) CDN: `hf_20260527_215021_3a629691-3a0c-4af8-9571-9fb88b22fc83.mp4`

---

## Session state — 2026-05-28

### What was completed this session
1. **MOTION UGC campaign verified** — 2 videos (Erik + Adriana) downloaded locally, logged in `campaigns/motion-ugc-bluerazz/winners.md`
2. **LILY avatar reference images generated** — 20 Miami penthouse lifestyle shots (nano_banana_2), iPhone 16 Pro aesthetic, 5 scenes × varied outfits. Reference image media_id: `4e8c164e-91bc-4679-ae39-f2e0b927d261`
3. **LILY Soul avatar training kicked off** — 18 user-approved images submitted to `show_characters(action='train', name='LILY', type='soul_2')`. Training takes ~10 min.

### What still needs to be done (pick up here next session)
- [ ] **Confirm LILY soul_id** — run `show_characters(action='list')` to get her soul_id once training completes (~10 min from 2026-05-28)
- [ ] **Update LILY soul_id** in the Trained Soul Avatars table above
- [ ] **Test LILY** — generate a test image with `soul_2` model + her soul_id
- [ ] **First real campaign with LILY** — decide what brand/brief to run her in (e.g. MOTION, lifestyle brand, etc.)
- [ ] **NSFW note:** When using LILY with reference image, avoid swimwear/bikini prompts — use athletic sets, shorts, dresses instead

### Key decisions made
- Skipping Publer, Klaviyo, Motion Blur, Shopify for now — just Higgsfield + Claude Code + GitHub
- No Vercel/Next.js needed for this project — pure automation pipeline
- Raw video files are gitignored; only output URLs/markdown files get committed
- Avatar training images: always use 15-20 images, single consistent setting preferred (penthouse worked well), iPhone 16 Pro aesthetic prompt produces best results

### Reference URLs
- GitHub repo: https://github.com/massmediagenius/ai-video-automation
- Higgsfield MCP docs: https://higgsfield.ai/mcp
- Higgsfield CLI docs: https://higgsfield.ai/cli
- Guide this was built from: Koda Academy "AI Content Farm System — Higgsfield MCP × Claude Code" by @timkoda_
