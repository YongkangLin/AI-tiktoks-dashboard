# Series Studio Pipeline

This project should behave like a small animated-series studio, not a text-video generator. The target format is original recurring character drama: fruit dating-reality, appliance breakup, food noir, luxury-object drama, or any other theme with locked characters and serialized lore.

## Core Feedback Gate

Every theme must pass the same viewer-feedback bar before upload:

- Voices are consistent and recognizably mapped to each character.
- Designs and silhouettes do not drift between shots.
- Dialogue matches mouth movement, or mouths are not visible during speech.
- Animation feels alive: reactions, camera motion, timing, and no dead-air drifting.
- Dialogue is specific to this cast and conflict, not generic recap filler.
- The story gives viewers a reason to finish: desire, betrayal, joke, mystery, twist, or cliffhanger.
- The first three seconds create immediate curiosity.

The repo now writes `quality_gate.json`, `quality_gate.md`, and `quality_review.json` for every package. A video cannot enter the publish-ready queue until character visuals exist for every scene and the quality review checks are marked as passing.

## Provider-Neutral Stack

| Job | Recommended providers | Repo role |
|---|---|---|
| Scripts, episode ideas, dialogue | OpenAI Responses API | Generate plots, cold opens, confessionals, shot lists, captions, lore comments. |
| Character references | OpenAI Images, Ideogram, Leonardo, Midjourney | Create reusable reference sheets for each character. |
| Scene video | Kling, Runway, Veo, Luma, Sora while available, ComfyUI | Generate 5-10 second vertical shots from reference images. |
| Voices | ElevenLabs, OpenAI TTS, Cartesia, Resemble | Keep a stable narrator and stable per-character voice profiles. |
| Lip sync | HeyGen, D-ID, Sync Labs, Tavus | Use only when characters visibly speak on camera. |
| Music and SFX | ElevenLabs SFX/Music, Beatoven, Stable Audio, licensed libraries | Build repeatable show audio signatures. |
| Editing/rendering | FFmpeg, Remotion, Shotstack, Creatomate, Cloudinary | Assemble clips, captions, zooms, lower thirds, music, end cards. |
| Posting | TikTok Content Posting API, YouTube Data API | Post only after local review and platform disclosure checks. |

Sora is an optional visual provider path, not the only backbone. The stronger long-term design is provider-neutral: reference assets first, then scene clips from whichever provider gives the most consistent characters.

## Fruit Dating-Reality Format

Do not use protected show names, branding, catchphrases, logos, or production style. Build an original fruit dating-reality parody with its own title, rules, set, narrator style, and lore.

Title directions:

- `Fruit Crush Villa`
- `Berry Beach`
- `Juice Island`
- `The Orchard House`
- `Ripe for Love`

Core format:

- Six to eight fruit characters live in a tropical juice-bar villa.
- Every episode has a cold open, one confessional, one social challenge, one betrayal or reveal, and one cliffhanger.
- Audience comments are invited as team votes or suspicion checks.
- The set, narrator, catchphrases, and episode rules must be original.

Example cast:

- Stella Strawberry: sweet on camera, strategic in confessionals.
- Mango Marco: confident new arrival with suspicious timing.
- Bella Blueberry: gossip queen who notices every tiny clue.
- Perry Peach: hopeless romantic who forgives too fast.
- Benny Banana: comic host/narrator with chaotic recaps.
- Gina Grape: dramatic wildcard who knows old villa secrets.

Episode 1 shape:

1. Cold open: Stella catches Mango entering the villa with a hidden bracelet.
2. Confessional: Bella says the bracelet belongs to someone already coupled.
3. Challenge: fruits pick partners for a smoothie-bar game.
4. Betrayal: Perry chooses Stella, but Mango already wrote her name.
5. Cliffhanger: Benny announces someone is getting juiced tomorrow.

## Continuity First

Generate the season plot before producing individual scene videos. Viewers will tolerate cliffhangers; they get annoyed when the account never pays them off.

Do not over-invest in one plot before the audience votes with retention, shares, comments, and follow-through. Start with a small format slate:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --plan-format-tests --episodes-per-format 2 --out outputs/format_tests
```

This writes `format_test_plan.json` and `format_test_plan.md`, capping early production at 2 episodes per format until 24h and 72h metrics justify scaling.

The season bible should define:

- Episode-by-episode conflict and relationship changes.
- What each episode pays off from the prior cliffhanger.
- The new cliffhanger each episode opens.
- What the next episode must answer before adding new drama.
- Stable cast, voice, and reference-image rules for the entire run.

Command:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --plan-season --show fruit_crush_villa --episodes 2 --out outputs/fruit_crush_villa
```

This writes `season_bible.json` and `season_bible.md`. Treat it as the source of truth before generating videos.

## Asset Order

1. Generate the season bible.
2. Generate `script.md`, `storyboard.csv`, `prompts.json`, `character_bible.json`, and `continuity_plan.json`.
3. Generate all `assets/references/*_sheet.png`.
4. Generate scene keyframes in `assets/images/scene_###.png` using the reference sheets.
5. Generate scene clips in `assets/video/scene_###.mp4` using the keyframes and reference sheets.
6. Generate stable narrator and character voices in `assets/audio`.
7. Lip-sync only shots with visible speaking mouths.
8. Assemble final MP4 with captions, music, zooms, lower thirds, and cliffhanger end card.
9. Refresh `quality_gate.json`; do not post unless status is `ready_for_upload_actions`.

## Commands

Generate packages and reference-aware visual plans:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --generate-object-packages 3 --object-series appliance_breakup --out outputs/object_week-01
PYTHONPATH=src python3 -m ai_story_pipeline --plan-visual-assets "$PACKAGE_DIR" --visual-provider sora
```

Dry-run Sora scene jobs:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-sora-plan "$PACKAGE_DIR/visual_asset_plan.json" --sora-job-limit 2
```

Dry-run ComfyUI reference sheets first:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-comfyui-plan "$PACKAGE_DIR/visual_asset_plan.json" --comfyui-asset-type reference_image --comfyui-workflow-template examples/comfyui_image_workflow_template.json
```

Refresh the quality gate:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --write-quality-gate "$PACKAGE_DIR"
```

The same flow applies to fruit dating-reality, appliance drama, food noir, luxury objects, celestial-office sitcoms, or any future theme. The theme changes; the quality gate does not.
