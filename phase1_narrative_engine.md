# Phase 1 Narrative Engine

Phase 1 validates story quality before automating HeyGen, TikTok posting, or scheduling. The current Narrative Engine implements the hidden-power genre from the product spec.

## Implemented

- Archetype rotation:
  - A: The Hidden Boss
  - B: The Disguised Prodigy
  - C: The Quiet Giant
  - D: The Test
  - E: Role Reversal
- Setting rotation with no duplicate setting inside one generation run.
- Hook pattern rotation with no same hook type twice in a row.
- Five hook variants per script for A/B testing.
- Variation axes:
  - protagonist gender
  - tone
  - reveal mechanism
  - antagonist type
  - protagonist reaction
  - setting wealth level
  - duration target
  - POV framing
- Dedup history for archetype + setting + reveal combinations across the last 30 generated scripts.
- Quality gate with score and notes.

## Generate Scripts

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --generate-scripts 5 --scripts-out outputs/hidden_power_scripts
```

Outputs:

- `narrative_scripts.json`
- `narrative_scripts.md`
- `outputs/script_history.json`

## API Upgrade Path

The local generator is deterministic and runs without API keys. For Claude or GPT scriptwriting, keep this module as the rotation, dedup, and validation layer, then pass selected archetype/setting/variation constraints into the model call.

Required key for a Claude integration:

- `ANTHROPIC_API_KEY`

Required key for an OpenAI integration:

- `OPENAI_API_KEY`

Do not automate posting until generated scripts pass human review for at least one manual batch.

## Object-Character Series

The addendum adds non-human/object-character drama because the human hidden-power format is more saturated. The local generator now supports object-character episodes with:

- Original object-role hybrid characters.
- Italianized rhythmic names.
- Relationship/lore hooks.
- Series mysteries.
- Search-style captions.
- Team-based comment bait.
- Lore-drop comment for the first hour after posting.
- Loopable original audio signature prompt.
- Visual and thumbnail prompts for consistent character identity.

Generate a test batch:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --generate-object-episodes 3 --object-out outputs/object_series
```

Object-character tests should start at 15-30 seconds, then expand to 60-90 seconds only after audience investment exists.

To run object-character episodes through the full production package pipeline, use:

```bash
PYTHONPATH=src python3 -m ai_story_pipeline --generate-object-packages 3 --out outputs/object_week-01
```

This writes normal episode packages with `script.md`, `prompts.json`, `storyboard.csv`, `monetization_audit.*`, and a batch manifest. The package runtime defaults to 61 seconds so monetization-oriented audits can pass while preserving the object-character lore, team comments, visual prompts, and loop cliffhangers.
