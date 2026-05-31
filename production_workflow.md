# Production Workflow

Use this workflow after generating episode packages with the CLI.

## 1. Plan A Small Format Slate

Avoid over-investing in one plot before the audience gives signal. Start by planning 2 episodes per format across fruit dating-reality, luxury-object drama, and object-character experiments:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --plan-format-tests --episodes-per-format 2 --out outputs/format_tests
```

This writes `format_test_plan.json` and `format_test_plan.md` with risk caps, generation commands, and scale thresholds. Do not expand a plot until 24h and 72h metrics pass the threshold.

## 2. Plan Season Continuity

Generate the season plot before producing videos:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --plan-season --show fruit_crush_villa --episodes 2 --out outputs/fruit_crush_villa
```

This writes `season_bible.json` and `season_bible.md`. Use it to make sure every cliffhanger has a planned part-two payoff before scene generation starts.

## 3. Generate Packages

For the review-gated campaign runner:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --run-campaign --campaign-format object --episodes 3 --out outputs/campaigns
```

This creates a timestamped run folder with local character-animatic MP4s, visual asset plans, publish queue, metrics template, TikTok dry-run submission files, `review_request.html`, `campaign_run.md`, and `e2e_readiness.md`. It does not post to TikTok. Trial mode blocks upload until the MP4 is reviewed; real mode can skip manual review but still requires final MP4s, character visuals, and monetization-audit readiness.

```bash
python3 -m ai_story_pipeline --show fruit_crush_villa --episodes 2 --seed week-01
```

For the non-human/object-character format, generate production-compatible packages directly:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --generate-object-packages 10 --object-series appliance_breakup --out outputs/object_week-01
```

For a local end-to-end object-character pass with final MP4s, publish queue, and monitoring template:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --generate-object-packages 3 --object-series appliance_breakup --run-e2e --out outputs/object_week-01
```

Review `script.md`, `character_bible.md`, and `quality_gate.md` first. Keep episodes with clear hooks, obvious emotion, simple visual actions, locked character identities, and a specific reason to finish.

If `ffmpeg` is available, create rough cuts before spending production credits:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --show fruit_crush_villa --episodes 3 --seed week-01 --render-preview
```

Use `batch_manifest.csv` to select the strongest hooks and safest monetization-audit scores.

For a local character-animatic MP4 with generated captions, narration, music, and visible recurring characters:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --show fruit_crush_villa --episodes 1 --seed week-01 --assemble-final
```

This creates `exports/final.mp4`, `exports/captions.srt`, `assets/audio/voiceover.txt`, `assets/audio/music_bed.m4a`, `assets/references/*_sheet.png`, `assets/images/scene_###.png`, and `asset_manifest.json` inside the episode package. When local TTS is available, it also writes a usable `assets/audio/voiceover.aiff`; otherwise the final video is assembled with captions and music. This is still a review animatic until a production video provider supplies better motion.

For a local character animatic MP4 with visible recurring characters:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --show fruit_crush_villa --episodes 1 --seed week-01 --assemble-final --provider local_character_animatic --write-publish-queue --review-mode trial
```

This writes deterministic `assets/references/*_sheet.png`, `assets/images/scene_###.png`, `local_character_assets.md`, and `exports/final.mp4`. In trial mode the publish queue still waits for human review of the MP4. In real mode, the queue can skip manual quality review but still requires a final MP4, character visuals, and a passing monetization audit.

To summarize a campaign run into one operator status:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --check-e2e-readiness outputs/campaigns/daily/YOUR_RUN_ID
```

Use `--require-tiktok-credentials` when you want the report to treat missing `TIKTOK_ACCESS_TOKEN` as a live-posting blocker.

After watching the MP4 in trial mode, approve the run only if it meets the bar:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --approve-campaign-run outputs/campaigns/daily/YOUR_RUN_ID --dashboard-out docs
```

This marks every package's `quality_review.json` checks as passed, refreshes `quality_gate.md`, rebuilds `publish_queue.csv`, writes TikTok dry-run payloads for ready rows, refreshes `e2e_readiness.md`, and updates the dashboard. It still does not post to TikTok.

To build a browser dashboard for the run:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --write-dashboard outputs/campaigns/daily/YOUR_RUN_ID --dashboard-out docs
```

This writes `docs/index.html`, `docs/dashboard/data.json`, and copied review assets for a GitHub Pages-style progress view.

For provider narration, set `ELEVENLABS_API_KEY` and `ELEVENLABS_VOICE_ID`, then run:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --show fruit_crush_villa --episodes 1 --seed week-01 --assemble-final --provider elevenlabs_voice
```

This keeps local scene-card video assembly but writes `assets/audio/voiceover_elevenlabs.mp3` and uses it in `exports/final.mp4`.

## 4. Build Character References

Create one reference sheet per recurring character:

- Front-facing full-body view.
- Three facial expressions.
- One close-up face crop.
- Simple white or transparent background.
- No logos, copyrighted characters, or celebrity likenesses.

Reuse these references for every image and video generation pass.

Every package writes `character_bible.json`, `character_bible.md`, `continuity_plan.json`, and `continuity_plan.md`. The visual plan includes `reference_image` jobs for `assets/references/*_sheet.png`. Generate those before scene clips so fruit, appliance, food-noir, and other themes keep recognizable characters.

## 5. Generate Scene Assets

For each scene in `prompts.json`:

- Generate one still image or keyframe.
- Generate a short motion clip from the video prompt.
- Keep character identity consistent.
- Reject outputs with unreadable text, distorted faces, logos, or watermark artifacts.

Build a provider-neutral visual asset plan from an episode package:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --plan-visual-assets "$PACKAGE_DIR"
```

Dry-run a ComfyUI image workflow submission:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-comfyui-plan "$PACKAGE_DIR/visual_asset_plan.json" --comfyui-workflow-template examples/comfyui_image_workflow_template.json
```

Dry-run reference-sheet jobs first:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-comfyui-plan "$PACKAGE_DIR/visual_asset_plan.json" --comfyui-asset-type reference_image --comfyui-workflow-template examples/comfyui_image_workflow_template.json
```

Dry-run Sora scene video jobs:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-sora-plan "$PACKAGE_DIR/visual_asset_plan.json" --sora-job-limit 2
```

Execute Sora only after `OPENAI_API_KEY` is set and the visual prompt/reference approach has been reviewed:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-sora-plan "$PACKAGE_DIR/visual_asset_plan.json" --sora-execute --sora-job-limit 2
```

To execute, start ComfyUI, set `COMFYUI_BASE_URL` if it is not `http://127.0.0.1:8188`, update the example workflow with a checkpoint installed in your ComfyUI instance, then add `--comfyui-execute`.

After submitted jobs finish, collect outputs into the package asset folders:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --collect-comfyui-outputs "$PACKAGE_DIR/comfyui_submissions/comfyui_submissions.json" --comfyui-collect-execute
```

If ComfyUI writes files locally and the API `/view` route is unavailable, add `--comfyui-output-root /path/to/ComfyUI/output`. Final assembly automatically rebuilds `preview.mp4` from `assets/images/scene_###.png`, `assets/images/scene_###.jpg`, or `assets/video/scene_###.mp4` when those files exist.

## 6. Quality Gate

The viewer-feedback gate is mandatory:

- Designs and characters must be consistent.
- Voices must remain stable and intentional.
- Mouth movement must match dialogue, or speaking mouths should be hidden.
- Animation must have reactions, camera energy, and no lifeless drift.
- Dialogue must be specific to the characters and conflict.
- Story must create a reason to finish.

Refresh the gate after collecting visuals and assembling:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --write-quality-gate "$PACKAGE_DIR"
```

Edit `quality_review.json` only after watching the episode. The publish queue will not mark an item ready unless the gate status is `ready_for_upload_actions`.

## 7. Voice And Captions

- Use the generated narrator and dialogue lines from `script.md`.
- Keep narration quick enough for mobile pacing but clear enough for captions.
- Burn captions into the video with high contrast.
- Keep captions away from platform UI zones.

## 8. Edit Structure

Target this shape:

- 0 to 3 seconds: accusation, reveal, or visual shock.
- 4 to 12 seconds: explain the stakes.
- 13 to 35 seconds: escalation and character reactions.
- 36 to 55 seconds: choice or twist.
- 56 seconds onward: cliffhanger and comment prompt.

## 9. Fruit Dating-Reality Parody

For Fruit Love Island-style content, build `Fruit Crush Villa`, an original fruit dating-reality parody. Do not use the protected show name, branding, catchphrases, logo, or production identity.

Use original title directions such as `Fruit Crush Villa`, `Berry Beach`, `Juice Island`, `The Orchard House`, or `Ripe for Love`. Start with six fruit characters, one recurring villa set, confessionals, challenges, betrayals, recouplings, and audience-vote comment bait. The same pipeline applies to appliance drama, food noir, luxury objects, and other themes.

## 10. Publish And Learn

Build and review the publish queue:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --build-publish-queue outputs/week-01/batch_manifest.csv
```

Prepare a TikTok Direct Post dry run:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-tiktok-queue outputs/week-01/publish_queue.csv --tiktok-mode direct_post
```

Execute only after `TIKTOK_ACCESS_TOKEN` is set, the TikTok app has the required Content Posting API scope, and `--review-mode real` is intentionally selected:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-tiktok-queue outputs/week-01/publish_queue.csv --tiktok-execute --tiktok-mode direct_post --tiktok-privacy-level SELF_ONLY --review-mode real
```

During trial mode, do not run `--tiktok-execute` until the final MP4s, `quality_gate.md`, and `publish_queue.md` have been reviewed.

Store each post in a spreadsheet or database with:

- Episode package path.
- Posted title.
- Runtime.
- Hook type.
- First 3 seconds hold rate.
- Average watch time.
- Completion rate.
- Comments per 1,000 views.
- Follows per 1,000 views.

Use the best-performing conflicts and characters to update `src/ai_story_pipeline/templates/shows.json`.

## 11. Analyze Metrics

Create a metrics template:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --write-metrics-template outputs/metrics_template.csv
```

After publishing, fill in the metrics CSV from TikTok, YouTube Shorts, or Reels analytics, then run:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --analyze-metrics outputs/metrics.csv --manifest outputs/batch_manifest.csv
```

The report ranks episodes as `scale`, `iterate`, `pause`, or `needs_more_data`.

## 12. Plan The Next Iteration

Use the analytics report to create the next production plan:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --plan-iteration outputs/analytics_report/analytics_report.json --next-episodes 6
```

The planner writes `iteration_plan.md` with concrete `--run-e2e` commands for the next batch, prioritizing patterns that scored best on retention, engagement, follower conversion, qualified views, and revenue.
