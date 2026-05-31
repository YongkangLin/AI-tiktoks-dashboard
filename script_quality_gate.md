# Script Quality Gate

Every script must pass a separate critic review before paid image or video generation.

## Mandatory Sub-Agent Review

For each script, spawn a sub-agent whose only job is to challenge whether the episode is worth producing. The critic must not rewrite by default. It should return a verdict, concrete blockers, and the smallest fixes needed before production.

Required critic prompt:

```text
Review SCRIPT_PATH against the AI TikTok Automation Addendum.
You are the mandatory plot/retention critic for this script. Do not edit files.
Return:
1. pass/fail verdict for paid video generation
2. plot logic holes
3. character/lore consistency for recurring non-human or object series
4. 2026 retention fit: 3-second hook, 10-15s visual spike, no dead air, loop ending, 70% completion design
5. visual/thumbnail readiness for expressive readable humanoid fruit/object characters
6. caption, comment bait, lore-drop, and original audio readiness
7. smallest concrete fixes needed before video generation
Be blunt and practical.
```

## Pass Criteria

- The first 3 seconds contain an immediate conflict or visual proof.
- Seconds 10-15 contain the strongest visual spike or emotional reaction.
- The episode follows the Duanju micro-structure: hook, one escalation movement, midpoint reversal, final cliffhanger.
- The first and last 2-3 seconds are decisive: no slow intro, no soft outro.
- There are roughly two major turns per minute.
- No shot plan depends on a shot lasting more than 5 seconds unless it contains active reaction or new evidence.
- No scene exists only to explain rules; every scene must contain conflict, clue, joke, or character reversal.
- The cliffhanger has a specific next-episode payoff and does not dodge the promised answer.
- The ending is loopable: cut mid-reaction, mid-motion, or into a sound that can restart the opening.
- Each recurring character has locked fruit/object identity, visual silhouette, desire, secret, voice direction, and on-camera behavior.
- Visual prompts are specific enough for paid generation: face, fruit/object texture, body, outfit, expression, action, camera move, and lighting.
- Posting package exists: search-style caption, comment bait, account lore-drop comment, and repeatable audio cue.

## Duanju Lens

Use [duanju_story_model.md](duanju_story_model.md) as the pacing reference. Our goal is a Duanju-style retention machine with original humanoid fruit/object characters: not a slow cartoon episode, not a generic TikTok skit, and not an unresolved mystery dump.

## Output Artifact

Save each critic result under:

```text
docs/script_reviews/<script_slug>_review.md
```

The script cannot move to paid render until the review blockers are either fixed or explicitly accepted.
