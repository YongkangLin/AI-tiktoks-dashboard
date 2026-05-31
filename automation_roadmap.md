# Automation Roadmap

The repo now automates story package generation, monetization review, batch queue creation, silent rough-cut previews, and local fallback final MP4 assembly. Production-quality AI story videos still need provider integrations for image/video generation, premium voice, licensed audio, and upload.

## Automated Now

- Original show templates with recurring characters, conflicts, locations, twists, hooks, CTAs, and hashtags.
- Hidden-power Narrative Engine with archetype rotation, hook variants, dedup, and quality checks.
- Object-character series generator with lore, comment bait, search captions, audio signature prompts, and visual prompts.
- Object-character production package generation for the standard audit, visual, assembly, queue, and analytics pipeline.
- Character bible generation for every package, including locked visual prompts, locked voice prompts, and expected reference-sheet paths.
- Quality gate generation for every package, enforcing character consistency, voice consistency, mouth/dialogue sync, animation vitality, dialogue specificity, story value, and hook strength.
- Episode generation for 61+ second vertical short-drama structure.
- `script.md`, `storyboard.csv`, `prompts.json`, `metadata.json`, and `production_checklist.md` per episode.
- `monetization_audit.md` and `monetization_audit.json` per episode.
- `batch_manifest.csv` and `batch_manifest.json` per generation run.
- Optional `preview.mp4` rough cuts with `--render-preview` when `ffmpeg` is installed.
- Optional `exports/final.mp4` assembly with captions, synthetic music, and local narration when TTS is available using `--assemble-final`.
- Episode asset folders: `assets/images`, `assets/video`, `assets/audio`, and `exports`.
- Provider interface in `providers.py` with `local_fallback` implemented.
- Credential-gated ElevenLabs narration provider with local video assembly.
- Visual asset planning from `prompts.json` into scene-level image/video jobs.
- Reference image planning for `assets/references/*_sheet.png` before scene generation.
- ComfyUI API-format workflow dry-run and `/prompt` submission path.
- ComfyUI output collection into package image/video asset paths.
- Sora scene-video submission and collection adapter, dry-run by default and credential-gated for execution.
- Final assembly regenerates previews from collected scene visual assets when present.
- Publish queue generation for safe manual upload or future official API posting, blocked when character visuals or the quality gate are incomplete.
- Official TikTok Content Posting API submission planner and client in `tiktok.py`.
- Credential-gated TikTok Direct Post or upload-to-inbox execution from a ready publish queue.
- Season continuity bible generation so cliffhangers have planned next-episode payoffs.
- Multi-format test planning with early risk caps so no single plot gets overfunded before metrics.
- CSV-based metrics import and analytics scoring.
- Analytics-driven iteration planning with concrete next-batch commands.
- `--run-e2e` operator command for a full local generate-assemble-queue-monitor prep pass.
- `--run-campaign` review-gated campaign command for batch generation, local final MP4s, visual plans, publish queue, metrics template, and TikTok dry-run files.
- Locked story JSON import for turning a human-approved story such as `docs/story_episode_001.json` into the same package, MP4 review, queue, dashboard, and readiness flow.

## Not Automated Yet

- Final AI image generation without a running ComfyUI server, cloud image provider, workflow template, and checkpoint.
- Final AI video generation or character-consistent animation without a configured provider such as Kling, Runway, Veo, Luma, Sora, or ComfyUI.
- Licensed music selection.
- Final edit assembly with actual AI visuals, lip sync where required, motion polish, and licensed music.
- Direct TikTok public posting without a valid access token, creator privacy selection, and approved/audited app.
- Any TikTok live post before local review of `campaign_run.md`, final MP4s, and publish queue.
- YouTube Shorts or Reels upload through approved official APIs.
- Automated analytics pull from platform dashboards.

## Recommended Next Build Order

1. Generate the first multi-format test plan with 2 episodes per format.
2. Generate short continuity bibles for the test slate, then only expand the winner.
3. Generate reference sheets for the first recurring cast and store them under `assets/references`.
4. Run scene video generation with a provider that supports references: Kling, Runway, Veo, Luma, Sora while available, or ComfyUI workflows.
5. Add lip-sync and vitality review for shots where characters speak on camera.
6. Improve final edit quality with motion, transitions, lower thirds, and richer caption templates.
7. Replace synthetic music with licensed music providers.
8. Add TikTok OAuth refresh and creator-info privacy option checks.

See `docs/open_source_stack.md` for the current open-source integration shortlist and `docs/series_studio_pipeline.md` for the provider-neutral show factory.

## Monetization Positioning

Treat this as an AI-assisted microdrama studio, not a bulk posting bot. The defensible operating model is original IP, human review, clear disclosure, consistent quality, and cross-platform distribution.
