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

## Seedance 2.0 — Confirmed UGC Workflow (BEST METHOD)

Put the script directly in the prompt in single quotes. Seedance reads it and generates audio where the character says those exact words. No ElevenLabs upload, no ffmpeg merge needed.

**Prompt format:**
```
[Character description] looking directly into camera, speaking naturally and saying: '[SCRIPT HERE]' [Visual style descriptors — UGC selfie, iPhone front camera, photorealistic, etc.]
```

**Example:**
```
Young platinum blonde woman looking directly into camera, speaking naturally and saying: 'I was making $500 a month on OF, ready to quit. Found OFO — it shows you what content works, builds your posting calendar, keeps you consistent. Went from $500 to $10k a month. Don't sleep on this.' Authentic UGC selfie style, natural mouth movement, nodding, gesturing, bright window light, casual kitchen setting, iPhone front camera, photorealistic
```

**Settings:** `start_image` (LILY's face), `duration: 15`, `resolution: 1080p`, `aspect_ratio: 9:16`, `generate_audio: true` (default — leave it)

**Key constraint:** Keep script short enough to fit in 15 seconds naturally (~30 words max)

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

## ElevenLabs

- **API key:** `sk_830443f01d92bc37019c0bc4266bae0a2b4103ba665dcc6c`
- **LILY voice ID:** `iOrg95b9JxGREjsg2T06` (saved as "Lily — locked", category: generated)
- **Workflow for realistic UGC:** Generate TTS with LILY voice → upload to Higgsfield OR merge locally with ffmpeg
- **ffmpeg merge command:** `ffmpeg -stream_loop 2 -i visual.mp4 -i voice.mp3 -map 0:v -map 1:a -c:v libx264 -preset fast -crf 18 -c:a aac -b:a 192k -t <audio_duration> output.mp4`
- **Voice Design:** Use `/v1/text-to-voice/create-previews` to generate custom voices; previews expire between sessions — save immediately. If expired, regenerate and check account for saved voices at `/v1/voices`.
- **Recommended TTS settings:** `stability: 0.4, similarity_boost: 0.85, style: 0.3, use_speaker_boost: true, model: eleven_multilingual_v2`

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
3. **LILY Soul avatar trained** — soul_id: `99c033cb-fbcc-4dfd-9cc0-5f1340b5eaf0`, 18 images submitted, status: ready
4. **OFO UGC campaign (MS version)** — `ugc_lily_ofo.mp4` with custom MS avatar `44c343b1-693c-4b82-80df-750c5043f460`
5. **OFO UGC campaign (realistic version FINAL)** — `lily_ofo_FINAL.mp4`: seedance_2_0 visual (15s looped to 30s) + ElevenLabs "Lily — locked" voice. **This is the deliverable.**

### What still needs to be done (pick up here next session)
- [ ] **Review `lily_ofo_FINAL.mp4`** — open in Finder, watch it, confirm you're happy with the voice sync
- [ ] **Next campaign** — decide which brand/brief to run LILY in next (MOTION, another OF-adjacent brand, etc.)
- [ ] **Soul Cinema test** — try `generate_video(model='soul_cinema_studio', soul_id='99c033cb...')` for a cinematic LILY video

### Key decisions made
- Skipping Publer, Klaviyo, Motion Blur, Shopify for now — just Higgsfield + Claude Code + GitHub
- No Vercel/Next.js needed for this project — pure automation pipeline
- Raw video files are gitignored; only output URLs/markdown files get committed
- Avatar training images: always use 15-20 images, single consistent setting preferred (penthouse worked well), iPhone 16 Pro aesthetic prompt produces best results
- **Realistic UGC workflow:** seedance_2_0 (visual, start_image from LILY) + ElevenLabs TTS (LILY voice) → ffmpeg merge. More realistic than Marketing Studio. Use this for premium deliverables.
- **ElevenLabs voice preview IDs expire** — always check `/v1/voices` first; saved voices persist

### Reference URLs
- GitHub repo: https://github.com/massmediagenius/ai-video-automation
- Higgsfield MCP docs: https://higgsfield.ai/mcp
- Higgsfield CLI docs: https://higgsfield.ai/cli
- Guide this was built from: Koda Academy "AI Content Farm System — Higgsfield MCP × Claude Code" by @timkoda_
