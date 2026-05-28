# OFO — Day in the Life Campaign
**LILY (custom avatar) | $50k/month OF Creator | 2026-05-28**

## Concept
"DAY IN THE LIFE of a OF creator who makes $50,000 a month thanks to the OFO app"
9-scene DITL series using seedance_2_0 script-in-prompt workflow. Each scene 8s, 9:16.

---

## Generated Scenes

| # | Scene | Job ID | Resolution | CDN URL |
|---|-------|--------|------------|---------|
| 1 | Bed hook — "This is what my life looks like now. Let me show you." | `ea07a73f-7201-4f9b-a4fb-bd3d88bb1c7d` | 1080p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_042647_ea07a73f-7201-4f9b-a4fb-bd3d88bb1c7d.mp4 |
| 2 | Bathroom skincare — "Every morning starts the same. Skin, coffee, check OFO." | `560b479c-628a-4818-ac06-0bc8e8fc435b` | 1080p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_042655_560b479c-628a-4818-ac06-0bc8e8fc435b.mp4 |
| 3 | Penthouse walk — "This is the penthouse. Floor to ceiling windows, Miami views. OF paid for this." | `79916b08-f9b8-426d-9355-c6e63877d9fa` | 1080p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_042704_79916b08-f9b8-426d-9355-c6e63877d9fa.mp4 |
| 4 | Kitchen — "OFO builds my posting calendar. I wake up and already know exactly what to post." | `caa2956e-2fe0-458d-b43f-73df7faef482` | 1080p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_042713_caa2956e-2fe0-458d-b43f-73df7faef482.mp4 |
| 5 | Workout — "Workout, post, make money. That is the whole job." | `257de686-48a6-44ca-9fc7-1386d6d6dbcb` | 1080p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_042722_257de686-48a6-44ca-9fc7-1386d6d6dbcb.mp4 |
| 6 | Bed shoot — "OFO shows me what content is already proven to perform. I just shoot it." | `907f3b77-a2f3-4770-b8c0-289b011cdf34` | 1080p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_042731_907f3b77-a2f3-4770-b8c0-289b011cdf34.mp4 |
| 7 | OFO app on phone — "This is the app. It shows you what works, builds your calendar, keeps you consistent." | `4242fb12-d9ba-47f4-b2e6-7e4b6a5f947e` | 720p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_043518_4242fb12-d9ba-47f4-b2e6-7e4b6a5f947e.mp4 |
| 8 | Ring light setup — "I used to make $500 a month. Now I am at $50k. The difference was finding OFO." | `d0a61c4c-c48e-4e8b-87c1-11f5b12ad436` | 720p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_043527_d0a61c4c-c48e-4e8b-87c1-11f5b12ad436.mp4 |
| 9 | Outro — "If you are on OF and not using OFO, you are leaving serious money on the table. Do not sleep on it." | `00cd82f0-08ef-4665-96a2-8fed57e4d855` | 720p | https://d8j0ntlcm91z4.cloudfront.net/user_3E2miy88dQ4jNWmsRfpnOHkC6RL/hf_20260528_043535_00cd82f0-08ef-4665-96a2-8fed57e4d855.mp4 |

## Specs
- Model: seedance_2_0
- Aspect ratio: 9:16
- Duration: 8s per scene (72s total across all 9 clips)
- Audio: native seedance (script quoted in prompt)
- Avatar: LILY kitchen start_image
- Scenes 1-6: 1080p | Scenes 7-9: 720p (URL passed instead of UUID on second batch — use UUID next time)

## Notes
- All 9 clips use script-in-prompt workflow — no ElevenLabs, no ffmpeg
- Scenes 7-9 came out 720p because LILY's start_image was passed as a CDN URL rather than an uploaded UUID; always media_upload first for 1080p
- Full DITL series ready to edit together in CapCut/Premiere
