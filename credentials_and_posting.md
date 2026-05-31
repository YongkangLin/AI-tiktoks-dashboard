# Credentials And Posting

The local pipeline can generate packages, assemble local fallback videos, write a publish queue, and analyze metrics without API keys. Direct posting and production AI media generation require provider credentials.

## Current Safe Posting Mode

The default posting provider is `manual_queue`.

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --run-e2e --episodes 3 --out outputs/week-01
```

This writes `publish_queue.csv` and `publish_queue.md`. Upload from that queue manually until official posting credentials are available.

For a full local campaign batch that still requires review before any TikTok execution:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --run-campaign --campaign-format object --episodes 3 --out outputs/campaigns
```

The campaign runner writes `campaign_run.md`, `review_request.html`, `e2e_readiness.md`, final MP4 paths, a publish queue, metrics template, and TikTok dry-run files. In `--review-mode trial`, it never performs live TikTok posting and requires MP4 review. In `--review-mode real`, it can post without manual review only when `--tiktok-execute` and valid TikTok credentials are provided.

Check a run's posting readiness:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --check-e2e-readiness outputs/campaigns/daily/YOUR_RUN_ID
PYTHONPATH=src python3 -m ai_story_pipeline --check-e2e-readiness outputs/campaigns/daily/YOUR_RUN_ID --require-tiktok-credentials
```

After you review and accept a trial MP4, approve the run to rebuild upload-ready artifacts without live posting:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --approve-campaign-run outputs/campaigns/daily/YOUR_RUN_ID --dashboard-out docs --tiktok-row-limit 1
```

The approval command refreshes `quality_review.json`, `quality_gate.md`, `publish_queue.csv`, `tiktok_submissions/tiktok_submissions.json`, `e2e_readiness.md`, and the dashboard. TikTok execution still requires a separate real-mode command with `--tiktok-execute`.

To prove the real-mode path without live posting, run the same story in real mode without `--tiktok-execute`; this skips the manual review gate and writes dry-run TikTok payloads:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --run-campaign --campaign-format story --story-json docs/story_episode_001.json --episodes 1 --out outputs/real_mode_dry_run --campaign-run-id story-episode-001-real --provider local_character_animatic --review-mode real --tiktok-row-limit 1
```

## TikTok Direct Posting Requirements

For direct TikTok posting, use TikTok's official Content Posting API rather than cookie-based browser bots.

Expected environment variables:

- `TIKTOK_CLIENT_KEY`
- `TIKTOK_CLIENT_SECRET`
- `TIKTOK_ACCESS_TOKEN`
- `TIKTOK_OPEN_ID`

Expected TikTok app capabilities:

- Content Posting API approval.
- OAuth flow for the posting account.
- `video.upload` for upload-to-inbox style flows.
- `video.publish` for direct post flows when approved.
- Creator privacy options should be queried before production Direct Post execution.
- Unverified or unaudited clients should test with `SELF_ONLY` privacy first.

Prepare a dry-run submission plan from a ready queue:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-tiktok-queue outputs/week-01/publish_queue.csv
```

Execute one ready queue row through Direct Post after setting `TIKTOK_ACCESS_TOKEN`:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-tiktok-queue outputs/week-01/publish_queue.csv --tiktok-execute --tiktok-mode direct_post --tiktok-privacy-level SELF_ONLY
```

After a live submit, fetch TikTok publish status from the returned `publish_id` values:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --fetch-tiktok-statuses outputs/week-01/tiktok_submissions/tiktok_submissions.json
PYTHONPATH=src python3 -m ai_story_pipeline --fetch-tiktok-statuses outputs/week-01/tiktok_submissions/tiktok_submissions.json --tiktok-status-execute
```

The first status command is a dry run that verifies which jobs have publish IDs. The second requires `TIKTOK_ACCESS_TOKEN` and calls TikTok's status endpoint.

Use upload-to-inbox instead of Direct Post when the app only has `video.upload`:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-tiktok-queue outputs/week-01/publish_queue.csv --tiktok-execute --tiktok-mode inbox_upload
```

The direct-post payload marks AI-generated content with `is_aigc: true`.

Do not add `--tiktok-execute` until the generated MP4s, captions, audio, monetization audit, and publish queue have been reviewed locally.

Official references:

- https://developers.tiktok.com/products/content-posting-api/
- https://developers.tiktok.com/doc/content-posting-api-reference-upload-video
- https://developers.tiktok.com/doc/content-posting-api-reference-direct-post
- https://developers.tiktok.com/doc/content-posting-api-reference-get-video-status
- https://newsroom.tiktok.com/en-us/direct-post

## AI Media Provider Keys

For production-quality output, pick one image/video stack and one voice stack first.

Recommended starting options:

- Script API: `ANTHROPIC_API_KEY` or `OPENAI_API_KEY`
- Avatar video: `HEYGEN_API_KEY` and `HEYGEN_AVATAR_ID`
- Local visuals: `COMFYUI_BASE_URL`
- Cloud visuals: `RUNWAYML_API_SECRET`, `OPENAI_API_KEY` for Sora while available, `REPLICATE_API_TOKEN`, `KLING_API_KEY`, `LUMA_API_KEY`, `GOOGLE_APPLICATION_CREDENTIALS`, or `PIKA_API_KEY`
- Voice: `ELEVENLABS_API_KEY` and `ELEVENLABS_VOICE_ID`, `OPENAI_API_KEY`, Kokoro, or Piper

Generate object-character packages before visual/provider work:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --generate-object-packages 3 --object-series appliance_breakup --out outputs/object_week-01
```

Use local ComfyUI for scene keyframe planning and submission:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --plan-visual-assets "$PACKAGE_DIR"
PYTHONPATH=src python3 -m ai_story_pipeline --submit-comfyui-plan "$PACKAGE_DIR/visual_asset_plan.json" --comfyui-asset-type reference_image --comfyui-workflow-template examples/comfyui_image_workflow_template.json
PYTHONPATH=src python3 -m ai_story_pipeline --submit-comfyui-plan "$PACKAGE_DIR/visual_asset_plan.json" --comfyui-workflow-template examples/comfyui_image_workflow_template.json
```

`--submit-comfyui-plan` is dry-run by default. To execute, start ComfyUI and add `--comfyui-execute`. The workflow template must be saved in ComfyUI API format and can use placeholders such as `{{PROMPT}}`, `{{NEGATIVE_PROMPT}}`, `{{SCENE}}`, and `{{JOB_ID}}`.

Collect completed ComfyUI outputs:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --collect-comfyui-outputs "$PACKAGE_DIR/comfyui_submissions/comfyui_submissions.json" --comfyui-collect-execute
```

The collector reads each submitted job's `prompt_id`, fetches ComfyUI history, and writes the first matching output to the `target_path` from `visual_asset_plan.json`.

Use Runway for paid image-to-video scene tests:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-runway-plan "$PACKAGE_DIR/visual_asset_plan.json" --runway-job-limit 2
PYTHONPATH=src python3 -m ai_story_pipeline --submit-runway-plan "$PACKAGE_DIR/visual_asset_plan.json" --runway-execute --runway-job-limit 2
PYTHONPATH=src python3 -m ai_story_pipeline --collect-runway-outputs "$PACKAGE_DIR/runway_submissions/runway_submissions.json" --runway-collect-execute
```

`--submit-runway-plan` is dry-run by default. Execution requires `RUNWAYML_API_SECRET`. The adapter uploads the local scene image or first character reference as a Runway ephemeral upload, starts `/v1/image_to_video`, stores task IDs, and collects completed MP4s back to `assets/video/scene_###.mp4`.

Use Sora for optional scene-video dry runs or execution:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --submit-sora-plan "$PACKAGE_DIR/visual_asset_plan.json" --sora-job-limit 2
PYTHONPATH=src python3 -m ai_story_pipeline --submit-sora-plan "$PACKAGE_DIR/visual_asset_plan.json" --sora-execute --sora-job-limit 2
PYTHONPATH=src python3 -m ai_story_pipeline --collect-sora-outputs "$PACKAGE_DIR/sora_submissions/sora_submissions.json" --sora-collect-execute
```

`--submit-sora-plan` is dry-run by default and requires `OPENAI_API_KEY` only when `--sora-execute` is used.

Use ElevenLabs narration in the local assembly path:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --show fruit_crush_villa --episodes 1 --assemble-final --provider elevenlabs_voice
```

Optional ElevenLabs overrides:

- `ELEVENLABS_MODEL_ID` defaults to `eleven_multilingual_v2`
- `ELEVENLABS_OUTPUT_FORMAT` defaults to `mp3_44100_128`

Use preset or properly licensed/consented voices only. Do not clone a voice unless you have the required rights and consent.

Do not commit real keys. Put them in a local `.env` file or your shell environment.

## Monitoring

Creator Rewards and platform analytics are not guaranteed to be fully available through public APIs. The current monitoring path is CSV-based:

1. Export or copy metrics from TikTok/Shorts/Reels dashboards.
2. Fill `metrics_template.csv`.
3. Run `--analyze-metrics`.
4. Use `analytics_report.md` to decide what to scale, iterate, or pause.
