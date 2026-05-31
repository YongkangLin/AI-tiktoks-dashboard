# Paid Video API Decision

As of May 31, 2026, the local character animatic should be treated as a storyboard and QA scaffold only. It proves continuity, timing, captions, review gates, and dashboard flow, but it cannot hit the premium humanoid-fruit look by itself. Production episodes should use paid image/video APIs plus a facial-performance layer.

## Decision

Primary paid path:

1. Character stills and reference sheets: Ideogram API first.
2. Controlled edits, expression sheets, and outfit variants: OpenAI Images.
3. Scene video: Kling v3 Omni or Runway image-to-video from approved stills.
4. Facial performance and close-up confessionals: Runway Act-Two or LivePortrait.
5. Backup/high-polish tests: Sora 2 Pro and Veo 3.1.
6. Cheap B-roll/transition fallback: Luma Ray 2.

The local dashboard images are now explicitly storyboard placeholders. The paid visual target is stored in `reference/ideal_examples/`, including the two user-provided MOV examples, extracted stills, a contact sheet, a manifest, and a paid API style card.

The first paid test should be one 30-45 second Fruit Crush Villa scene, not a full episode. Spend on three shots:

- Establishing villa entrance with two fruit characters moving.
- Close-up confessional with facial performance and mouth movement.
- Two-character poolside conflict with body motion and reaction cut.

If those three shots pass the viewer-feedback gate, expand to a 90-120 second episode.

## Image Generation Decision

Use Ideogram API as the first paid image provider because the main failure mode is character quality and consistency, not script scaffolding. The examples the user approved require humanoid fruit characters with glossy fruit texture, expressive eyes and mouths, detailed wardrobe, jewelry, hands, and luxury-villa lighting. Those stills become the source of truth for all downstream video shots.

Use OpenAI Images as the edit and iteration provider after the first Ideogram sheets exist. It should handle expression variants, outfit variants, continuity fixes, and scene-specific keyframes without changing the locked character identity.

The first credentials to wire are:

- `IDEOGRAM_API_KEY` for paid character stills.
- `OPENAI_API_KEY` for image edits and fallback generation.
- `RUNWAYML_API_SECRET` or `KLING_API_KEY` for image-to-video motion.

## Provider Comparison

| Provider | Best use | Why it matters for humanoid fruit drama | Main weakness |
|---|---|---|---|
| Kling v3 Omni | Primary scene renderer | Strong fit for image/element references, multi-shot scenes, start/end frames, motion control, and 9:16 social video. Good candidate for the Fruit Love Island-style look. | API details and output collection must be validated with a paid key. |
| Runway Gen-4.5 / Act-Two / Characters | Facial performance and character acting | Act-Two can drive facial expressions and body movement from a reference video. Characters can be created from a single image, including animated mascots and stylized brand characters. | More expensive than lightweight renderers; best used on hero shots and confessionals. |
| Sora 2 Pro | Backup premium renderer | Supports image references, reusable non-human character assets, 1080x1920 output, 16-20 second clips, extensions, edits, and batch video jobs. | Human-likeness restrictions can block references that look too human; expensive at pro quality. |
| Veo 3.1 | Realism/high-fidelity alternate | Supports reference images and high-fidelity video; useful when we want cinematic realism and fewer cartoon artifacts. | Less direct control over reusable recurring cast than a dedicated character-reference flow. |
| Luma Ray 2 | B-roll and cheap motion tests | Fast image-to-video/keyframe flow, 9:16 support, loop support, and extensions. | No dedicated reusable character asset system for serialized cast consistency. |
| LivePortrait | Facial expression transfer | Open-source portrait animation from a source image and driving video. Good for fruit confessional close-ups, blinks, eye darts, lip motion, and reaction faces. | Not a full scene renderer; mostly face/head performance, needs compositing or a provider scene underneath. |

## Why Kling First

For our specific format, the bottleneck is not generic cinematic video. It is consistent absurd characters across many shots. Kling v3/Omni is the best first paid target because its model matrix explicitly supports image-to-video, multi-shot video, start/end frame, element control for video character elements and multi-image elements, and motion control. That maps directly to our saved `character_bible.json`, reference-sheet jobs, scene keyframes, and `visual_asset_plan.json`.

We should still keep Runway in the loop because the critique we got was about lifeless animation, generic dialogue, and mouth mismatch. Runway Act-Two or Characters is better suited for controlled acting beats: a confessional, a shocked reaction, a character looking away, or a mouth-synced line. This is where the "freaky human expression" style comes from.

## Production Shot Recipe

For each recurring character:

1. Generate a high-quality full-body reference still:
   - anthropomorphic fruit head
   - human-like but clearly non-human body
   - expressive eyes and mouth
   - outfit, jewelry, hands, posture, skin/peel texture
   - simple background
2. Generate a 2-4 second neutral performance clip:
   - blink
   - small head turn
   - half-smile
   - one hand gesture
3. Use the still plus performance clip as the reusable reference source.
4. Generate scene clips in short chunks, 3-10 seconds each.
5. Keep each shot to one clear action:
   - "Stella steps back and raises one hand."
   - "Marco looks guilty, then glances at Bella."
   - "Bella whispers into the camera in a confessional."
6. Assemble clips locally with FFmpeg/Shotstack/Creatomate.
7. Only lip-sync visible mouths on close-ups; hide or minimize mouths in wide shots.

## Prompt Shape

Use this shape for paid video shots:

```text
Vertical 9:16 premium AI animated reality-show scene.
Use the provided character references exactly.
Characters: Stella Strawberry and Mango Marco.
Setting: tropical fruit villa pool at sunset, warm cinematic lighting, shallow depth of field.
Action: Stella steps backward, raises one hand, and looks hurt. Marco smiles, then his expression drops when Bella enters frame.
Camera: slow reality-TV push-in, handheld but stable, reaction-cut energy.
Style: humanoid fruit characters with detailed peel/skin texture, expressive eyes and mouths, human-like hands and wardrobe, not human likeness, no copyrighted show branding.
Motion: natural breathing, eye darts, head turns, hand gestures, clothing movement.
Avoid: static pose, lifeless drift, melted hands, inconsistent faces, extra characters, logos, watermarks, unreadable text.
```

## Spend Cap

Do not buy a full season before one paid render test passes.

Recommended first spend:

- 3 Kling v3/Omni test shots.
- 1 Runway Act-Two or LivePortrait confessional close-up.
- 1 Sora 2 Pro or Veo 3.1 comparison shot only if access is ready.

Pick the provider based on:

- Character match to reference.
- Expression quality.
- Body/hand motion.
- Mouth/dialogue match.
- Story clarity without reading captions.
- Cost per usable second.

## Repo Integration Target

The first paid-provider code path is the Runway adapter because it can already automate local reference upload, image-to-video task creation, polling, and MP4 collection from the same `visual_asset_plan.json` used by the local animatic. Run it as:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-runway-plan "$PACKAGE_DIR/visual_asset_plan.json" --runway-job-limit 2
PYTHONPATH=src python3 -m ai_story_pipeline --submit-runway-plan "$PACKAGE_DIR/visual_asset_plan.json" --runway-execute --runway-job-limit 2
PYTHONPATH=src python3 -m ai_story_pipeline --collect-runway-outputs "$PACKAGE_DIR/runway_submissions/runway_submissions.json" --runway-collect-execute
```

The next code milestone is a `kling.py` adapter parallel to `runway.py` and `sora.py`:

- Read `visual_asset_plan.json`.
- Select video jobs only.
- Submit short scene jobs to Kling Omni.
- Store `task_id`, request payload, status, and provider output URLs.
- Collect MP4s into `assets/video/scene_###.mp4`.
- Reassemble `exports/final.mp4`.
- Refresh `quality_gate.json`, `review_request.html`, and `docs/index.html`.

Required credentials:

- `KLING_API_KEY` for Kling paid tests.
- `RUNWAYML_API_SECRET` for Runway facial-performance tests.
- `OPENAI_API_KEY` for Sora fallback.
- `GOOGLE_APPLICATION_CREDENTIALS` or Gemini key for Veo fallback.
- `LUMA_API_KEY` for Luma fallback.
