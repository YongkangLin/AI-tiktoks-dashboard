# Open-Source Stack To Speed Up Production

Use mature open-source building blocks instead of pulling a random "TikTok bot" repo. The goal is original, policy-aware AI microdrama production, so the stack should help with assets, editing, voice, captions, analytics, and repeatability without encouraging spam automation.

## Recommended Pull-Ins

| Layer | Best Fit | Why It Helps | Integration Priority |
| --- | --- | --- | --- |
| AI visual workflow | ComfyUI | Node/API backend for repeatable reference sheets, keyframes, and video workflows, useful for character-consistent scene assets. | High |
| Programmatic video rendering | Remotion | React-based video templates, good for polished captions, branded layouts, and scalable rendering. | Medium |
| Local video assembly | FFmpeg | Already integrated; reliable for final muxing, audio, captions, preview renders, and validation. | Already used |
| Python video helpers | MoviePy | Faster to prototype edits in Python, but less necessary while FFmpeg commands are simple. | Low |
| Local TTS | Kokoro or Piper | Can replace the current local `say` fallback with usable offline narration. | High |
| Caption QA | whisper.cpp | Useful after real narration exists, to verify generated voice and captions match. | Medium |
| Video edit templates | Shotstack or Creatomate alternatives via Remotion | Useful once captions, lower thirds, confessionals, zooms, and cliffhanger end cards need to be repeatable. | Medium |

## What To Avoid

- Do not vendor a "TikTok uploader" bot that depends on cookies, browser scraping, or unofficial APIs.
- Do not use open-source repos that bundle copyrighted clips, celebrity voices, or franchise templates.
- Do not copy a full Fruit Love Island clone. Use category learning, not protected names or lookalike branding.
- Do not add GPL/AGPL dependencies directly into core code unless we are comfortable with the license obligations.

## Practical Integration Order

1. Use the ComfyUI visual asset planner to generate `reference_image` jobs from `character_bible.json`.
2. Generate scene keyframes from `prompts.json` only after reference identity is stable.
3. Add scene video generation workflows after keyframe identity is stable.
4. Add Kokoro or Piper as a local TTS provider that consumes `assets/audio/voiceover.txt` and writes a real narration file.
5. Keep FFmpeg as the assembler until the edit requirements outgrow it.
6. Consider Remotion after the visual style is proven, especially if we need richer motion graphics, reusable caption templates, and branded series packaging.

## Source References

- Remotion: https://github.com/remotion-dev/remotion
- ComfyUI: https://github.com/comfy-org/ComfyUI
- MoviePy: https://github.com/Zulko/moviepy
- Piper TTS: https://github.com/rhasspy/piper
- whisper.cpp: https://github.com/ggml-org/whisper.cpp
- FFmpeg docs: https://www.ffmpeg.org/ffmpeg.html
- FFmpeg legal/licensing: https://ffmpeg.org/legal.html
