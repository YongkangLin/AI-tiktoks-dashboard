# Fruit Crush Villa Writer Dashboard

## Production Summary

- **Show:** Fruit Crush Villa
- **Episode:** 1
- **Title:** The Necklace He Denied
- **Runtime target:** 60 seconds, with an 18-second FYP test cut
- **Format:** Original humanoid-fruit dating-reality microdrama
- **Pacing model:** Duanju-style vertical episode: conflict first, proof object, midpoint turn, cliffhanger
- **Visual target:** Premium glossy 3D humanoid fruit characters, inspired by the approved reference pack but not copying any protected show, logo, or creator
- **Status:** Writer lock for paid image-to-video generation

## One-Sentence Plot

Stella Strawberry secretly met Mango Marco during last night's private villa audition, where he gave her half of a seed-heart necklace; today Marco enters holding Pina Pineapple's hand and denies knowing Stella, until Bella Blueberry exposes the matching necklace and Benny Banana accidentally reveals there is an audition tape.

## Why The Plot Makes Sense

- Marco and Stella are not exes with vague history. They met last night during a private chemistry audition.
- Marco denies her because Benny promised the audition footage would stay hidden if Marco followed the entrance twist.
- Pina is not the villain yet. She thinks Marco honestly chose her for his entrance.
- Stella has one proof object: her half of the seed-heart necklace.
- Bella has one behavior clue: Marco keeps touching the hidden matching necklace.
- Benny creates the Part 2 hook by naming the hidden audition tape in public.

## Continuity Bible

### Stella Strawberry

- **Visual lock:** Red strawberry fruit head with visible seed texture, green leaf hair swept to one side, large green eyes, expressive brows, glossy lips, human-like body and hands.
- **Wardrobe:** Red sequined villa dress, delicate gold chain, half seed-heart necklace engraved `S`.
- **Personality:** Sweet on first read, surgical when embarrassed. She does not yell after the first shock; she gets quieter.
- **Signature line:** "Nice to meet me?"
- **Continuity rule:** Her necklace is visible from Shot 04 onward. She never knows about Benny's tape until Benny slips.

### Mango Marco

- **Visual lock:** Tall golden mango fruit head, warm orange-yellow skin, side leaf detail, athletic human-like body, expressive dark eyes, charming mouth that over-smiles when lying.
- **Wardrobe:** Open tropical shirt, white linen pants, gold chain, hidden matching seed-heart necklace engraved `M`.
- **Personality:** Performs confidence for cameras, but panic leaks through his hands.
- **Signature tell:** Touches his necklace whenever Stella mentions last night.
- **Continuity rule:** Marco is guilty of denial, not of planning the whole production setup. His fear of Benny matters.

### Pina Pineapple

- **Visual lock:** Pineapple fruit head with tall green crown, golden textured skin, hoop earrings, sharp eyes, polished resort glamour.
- **Wardrobe:** Lime-gold villa dress, stacked bracelets, confident entrance styling.
- **Personality:** Smug until the proof appears, then confused and embarrassed.
- **Story role:** Public betrayal image. She should not become a second plotline in Episode 1.
- **Continuity rule:** Pina believes Marco came in with her voluntarily.

### Bella Blueberry

- **Visual lock:** Round blueberry-purple fruit head, glossy blue skin, bright eyes, violet leaf accents or short curled hair, compact expressive body.
- **Wardrobe:** Cobalt cropped jacket, silver jewelry, small phone in hand.
- **Personality:** Gossip detective. Fast, amused, precise.
- **Signature action:** Notices tiny physical details before everyone else.
- **Continuity rule:** Bella exposes the clue; she does not already know the whole secret.

### Benny Banana

- **Visual lock:** Tall banana fruit head, bright yellow peel shape, human-like host body, broad show smile that snaps into panic.
- **Wardrobe:** Cream host suit, green pocket square, cue cards, hidden earpiece.
- **Personality:** Polished producer-host, allergic to unscripted truth.
- **Signature tell:** Smiles too long before giving an order.
- **Continuity rule:** Benny knows about the audition tape and is trying to keep it buried.

## Prompt Foundation

Use this prefix on every video prompt:

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use the approved character references exactly. Humanoid fruit characters with clear fruit silhouettes, expressive eyes, eyebrows, mouths, human-like bodies and hands, detailed fruit texture, wardrobe, jewelry, tropical luxury villa at sunset, cinematic shallow depth of field, reality-TV push-in and reaction-cut energy.
```

Use this negative prompt on every still or video job:

```text
Avoid flat mascot art, sticker style, realistic human faces, uncanny human skin, horror, gore, extra characters, inconsistent fruit heads, warped hands, melted jewelry, unreadable props, baked-in subtitles, logos, watermarks, TikTok UI, copied show branding, celebrity likeness, random text.
```

Important prop note:

```text
Do not rely on the video model to render tiny necklace text. Generate the necklace as a clean visible prop, then add the exact engraving as an edited overlay: S + M - 11:47 PM.
```

## Episode Generator Settings

- **Canvas:** Vertical 9:16.
- **Export target:** 1080x1920 final MP4.
- **Generation order:** Character stills first, ensemble reference second, image-to-video clips third, edit layer last.
- **Clip length:** 3-5 seconds per frame card.
- **Cut style:** Hard Duanju cuts; no dissolves.
- **Motion style:** Natural breathing, eye darts, head turns, mouth movement, hand gestures, clothing movement.
- **Text layer:** Add captions, timestamps, and necklace engraving in post.
- **Audio cue:** Bright villa sting, silence on "Nice to meet me?", low bass hit on "11:47 p.m."
- **Loop design:** Cut Benny's "Stella, don't" back to Marco's first denial.
- **Reject criteria:** Reject clips where Stella or Marco's necklace disappears, Pina looks informed too early, or any fruit head changes shape between cuts.

## Reference Photos To Use

- `docs/dashboard/assets/ideal_examples/chat_reference_images/chat_refs_contact_sheet.jpg`
- `docs/dashboard/assets/ideal_examples/chat_reference_images/chat_ref_2026-05-31_01.png` through `chat_ref_2026-05-31_07.png` for fruit faces, body acting, jewelry, and villa lighting.
- `docs/dashboard/assets/ideal_examples/chat_reference_images/chat_ref_2026-05-31_08.png` through `chat_ref_2026-05-31_10.png` for the wider object-character charm lane.
- Use the photos as style anchors only. Do not copy source watermarks, visible creator handles, or any protected branding.

## Character Reference Still Prompts

### Stella Strawberry Full-Body Reference

```text
Vertical 9:16 premium 3D animated character reference for Fruit Crush Villa. Stella Strawberry, a humanoid strawberry woman with glossy red strawberry fruit head, tiny seed texture, green leaf hair swept to one side, large green expressive eyes, eyelids, eyebrows, detailed mouth, human-like shoulders, arms, hands, and confident posture. Red sequined villa dress, delicate gold chain with half seed-heart necklace, soft warm sunset pool lighting, tropical luxury villa background, charming non-human character design, consistent front-facing full body.
```

### Mango Marco Full-Body Reference

```text
Vertical 9:16 premium 3D animated character reference for Fruit Crush Villa. Mango Marco, a tall humanoid mango man with golden orange mango fruit head, subtle leaf detail, expressive dark eyes, charming overconfident smile, athletic human-like body and hands. Open tropical floral shirt, white linen pants, gold chain with hidden half seed-heart necklace under collar, polished villa bombshell styling, sunset pool background, glossy fruit texture, readable silhouette, non-human but emotionally expressive.
```

### Pina Pineapple Full-Body Reference

```text
Vertical 9:16 premium 3D animated character reference for Fruit Crush Villa. Pina Pineapple, a glamorous humanoid pineapple woman with golden pineapple fruit head, tall green crown leaves, hoop earrings, sharp expressive eyes, confident smile, human-like body and hands. Lime-gold resort dress, stacked bracelets, tropical villa pool at sunset, premium glossy 3D animation, elegant but slightly absurd, clear pineapple silhouette.
```

### Bella Blueberry Full-Body Reference

```text
Vertical 9:16 premium 3D animated character reference for Fruit Crush Villa. Bella Blueberry, a compact humanoid blueberry woman with round glossy blue-purple fruit head, bright forensic eyes, expressive brows, violet leaf accents, human-like body and hands. Cobalt cropped jacket, silver jewelry, small phone in hand, playful detective expression, sunset villa lounge background, premium glossy 3D style, charming non-human character.
```

### Benny Banana Full-Body Reference

```text
Vertical 9:16 premium 3D animated character reference for Fruit Crush Villa. Benny Banana, a tall humanoid banana host with bright yellow banana fruit head, expressive eyes, wide polished smile, human-like body and hands. Cream host suit, green pocket square, cue cards, tiny earpiece, tropical villa ceremony set at sunset, glossy 3D animation, charming but secretly nervous.
```

### Ensemble Consistency Reference

```text
Vertical 9:16 premium 3D animated ensemble reference for Fruit Crush Villa. Stella Strawberry, Mango Marco, Pina Pineapple, Bella Blueberry, and Benny Banana standing together by the sunset villa pool. Each character keeps their exact fruit head shape, outfit, jewelry, body scale, and expression style. Reality-show ceremony lighting, clear spacing, full bodies visible, no extra characters, no logos, no captions.
```

## 60-Second Script Lock

### Beat 1: Public Denial, 0:00-0:07

**Visual:** Marco enters holding Pina's hand. Stella is waiting by the pool and recognizes him instantly.

```text
Benny: New bombshell in the villa... Mango Marco.
Stella: Marco?
Marco: I have never met that strawberry in my life.
```

**Caption:** He said he never met her.

### Beat 2: Pina Claims Him, 0:07-0:15

**Visual:** Pina pulls Marco closer. The room turns toward Stella.

```text
Pina: That's awkward. He came in with me.
Marco: Stella, right? Nice to meet you.
Stella: Nice to meet me?
```

**Caption:** Nice to meet me?

### Beat 3: Stella Shows Her Half, 0:15-0:25

**Visual:** Stella lifts her half of the seed-heart necklace.

```text
Stella: Then why am I wearing your promise?
Marco: A lot of people wear necklaces.
Stella: Not from last night's audition.
```

**Caption:** Then why am I wearing your promise?

### Beat 4: Marco's Tell, 0:25-0:34

**Visual:** Marco laughs too loudly and touches the necklace under his collar.

```text
Marco: Every mango has charm.
Bella: Then why are you hiding yours?
Marco: I'm not hiding anything.
```

**Caption:** Why are you hiding yours?

### Beat 5: The Engraving, 0:34-0:46

**Visual:** Bella flips Marco's necklace outward. Add clean edited overlay for the tiny text.

```text
Bella: It says S plus M.
Pina: That could mean anything.
Bella: It also says... 11:47 p.m.
```

**Caption:** S + M. 11:47 p.m.

### Beat 6: Benny Slips, 0:46-0:55

**Visual:** Benny's host smile breaks. He signals to the camera crew and accidentally names the hidden tape.

```text
Benny: Cut Camera Three. Not the audition tape.
Stella: Why?
Bella: Because he knew.
```

**Caption:** Benny knew.

### Beat 7: Cliffhanger, 0:55-1:00

**Visual:** Stella turns away from Marco and faces Benny. Marco looks more afraid of Benny than of Stella.

```text
Stella: Roll the audition tape.
Benny: Stella, don't.
CUT.
```

**Caption:** Part 2 opens on the tape.

## Frame-By-Frame Paid Video Prompt Pack

Generate each shot as a 3-5 second image-to-video clip from approved stills. Keep one clear action per shot. Add captions and tiny prop text in edit, not inside the generated video.

### Shot 01: Marco Enters With Pina, 0:00-0:04

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Mango Marco, Pina Pineapple, and Stella Strawberry exactly. Tropical luxury villa pool at sunset. Marco enters through palm shadows holding Pina's hand while Stella waits by the pool and recognizes him. Stella's face changes from hopeful to stunned, Marco's smile stays too polished, Pina looks proud. Fast reality-TV push from Stella's reaction to Marco and Pina, natural walking motion, hand contact, blinking, clothing movement, no captions or logos.
```

### Shot 02: The Denial Close-Up, 0:04-0:07

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Mango Marco and Stella Strawberry exactly. Tight close-up on Marco's mango face as he gives a fake charming smile and publicly denies knowing Stella. Stella is blurred behind him, frozen by the pool. Camera does a small handheld push-in as Marco's eyes dart for one frame. Story beat: he is lying in front of everyone. No embedded subtitles, no logos.
```

### Shot 03: Pina Pulls Him Closer, 0:07-0:11

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Pina Pineapple, Mango Marco, and Stella Strawberry exactly. Pina tightens her grip on Marco's arm and steps half a pace in front of him, trying to claim the entrance moment. Stella remains visible between them in the background. Pina's expression shifts from smug to slightly unsure as she sees Stella's face. Medium two-shot, resort pool lights, clear hand acting, no extra characters.
```

### Shot 04: Nice To Meet Me, 0:11-0:15

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved reference for Stella Strawberry exactly. Close-up on Stella's strawberry face and visible gold necklace chain. Her hurt smile tightens into cold disbelief as she repeats the fake greeting back at Marco. Small breath, eye shine, eyelids narrowing, one controlled head tilt. Background softly blurred sunset villa. No text in frame.
```

### Shot 05: Stella Shows Her Half, 0:15-0:20

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Stella Strawberry and Mango Marco exactly. Stella lifts her half of a seed-heart necklace toward camera; the prop catches warm pool light. Rack focus from the necklace to Marco in the background as his smile drops. Stella remains calm and steady. Add exact engraving later in edit, do not generate readable tiny text. No logos, no captions.
```

### Shot 06: Marco Laughs Too Loud, 0:20-0:28

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Mango Marco and Pina Pineapple exactly. Marco laughs too loudly beside Pina and waves off Stella's necklace, but his fingers drift toward the chain hidden under his shirt collar. Pina's confident smile flickers. Reality-TV handheld push-in, villa contestants only as soft background silhouettes, natural mouth movement and nervous hand acting.
```

### Shot 07: Bella Notices The Tell, 0:28-0:34

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Bella Blueberry and Mango Marco exactly. Close-up on Marco's hand touching the hidden necklace under his floral shirt, then snap focus to Bella Blueberry noticing it with a playful detective expression. Bella leans into frame with bright eyes and a tiny smile. Quick reality-show zoom, crisp prop visibility, no extra text.
```

### Shot 08: Bella Flips The Necklace, 0:34-0:40

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Bella Blueberry and Mango Marco exactly. Bella steps behind Marco and flips his matching seed-heart necklace outward toward the camera. Marco's mango face panics, shoulders tightening. Bella looks triumphant but amused. Fast hand close-up, necklace clearly visible, do not attempt readable engraved text in generation.
```

### Shot 09: Pina Realizes, 0:40-0:46

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Pina Pineapple, Stella Strawberry, and Bella Blueberry exactly. Reaction triangle by the villa pool: Bella points at Marco's necklace, Pina's smug expression collapses into embarrassed confusion, Stella watches silently with controlled fury. Add clean overlay in edit reading S + M - 11:47 PM. Camera cuts from necklace insert to Pina to Stella, no baked-in subtitles.
```

### Shot 10: Benny Cuts Cameras, 0:46-0:52

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Benny Banana and Stella Strawberry exactly. Benny Banana's polished host smile breaks as he turns toward offscreen camera crew and makes a sharp cut gesture with his cue cards. Stella turns toward him, suddenly realizing the host knows more. Whip pan to Benny, earpiece visible, tropical production chaos, no logos.
```

### Shot 11: Benny Knew, 0:52-0:55

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Bella Blueberry, Benny Banana, and Stella Strawberry exactly. Bella points at Benny with forensic confidence, Stella's eyes shift from Marco to Benny, Benny freezes with his host smile stuck halfway. Three-character triangle composition, sunset pool ceremony lighting, sharp reaction cuts, no captions in the generated clip.
```

### Shot 12: Roll The Tape, 0:55-1:00

```text
Vertical 9:16 premium 3D animated reality-show microdrama. Use approved references for Stella Strawberry, Benny Banana, and Mango Marco exactly. Stella points toward the reality-show camera and demands the audition tape. Benny reaches one hand forward, panicked, trying to stop her. Marco stands behind them looking more scared than guilty. Slow push on Stella, smash cut mid-motion, designed to loop back to Marco's denial. No embedded subtitles or logos.
```

## 18-Second FYP Test Cut

Use this shorter version to test the non-human character hook before paying for the full 60-second episode.

1. **0:00-0:03:** Marco enters with Pina and says he has never met Stella.
2. **0:03-0:07:** Stella shows her matching necklace.
3. **0:07-0:11:** Bella catches Marco touching his hidden chain.
4. **0:11-0:15:** Bella flips Marco's necklace. Overlay: `S + M - 11:47 PM`.
5. **0:15-0:18:** Benny says, "Not the audition tape." Smash cut.

### 18-Second Caption

```text
Fruit villa drama where Mango Marco denies knowing Stella, but the necklace from last night's audition exposes him. Did Marco betray Stella, or did Benny set them both up?
```

### 18-Second Prompt

```text
Vertical 9:16 premium 3D animated fruit reality microdrama trailer. Use approved character references for Stella Strawberry, Mango Marco, Pina Pineapple, Bella Blueberry, and Benny Banana exactly. Five hard cuts: Marco enters holding Pina's hand and denies knowing Stella; Stella lifts her matching seed-heart necklace; Bella notices Marco touching his hidden chain; Bella flips Marco's necklace toward camera; Benny Banana panics and tries to cut the cameras. Sunset tropical villa pool, glossy humanoid fruit characters, expressive faces and hands, dramatic reality-TV push-ins, clean edited overlay for S + M - 11:47 PM, no baked-in captions, no logos, no watermarks.
```

## Audio, Caption, And Lore Package

- **Original audio cue:** A bright villa sting, a quick silence on Stella's "Nice to meet me?", then a low bass hit when Bella says "11:47 p.m."
- **Repeatable sound title:** Stella's Theme - Nice To Meet Me
- **Search caption:** Fruit villa drama where Mango Marco denies knowing Stella, but the necklace from last night's audition exposes him.
- **Comment bait:** Did Marco betray Stella, or did Benny set them both up?
- **Lore drop comment:** Look at Marco's hand before Bella says anything. He touches the necklace like he already knows it will ruin him.
- **Loop note:** Cut Benny's "Stella, don't" directly back to Marco saying, "I have never met that strawberry in my life."

## Episode 2 Continuity Promise

Part 2 must open on the audition tape. Do not skip to a new villa problem.

Episode 2 opening answer:

```text
Security footage from 11:47 p.m. shows Marco placing the necklace on Stella and saying, "If we enter together, they will know we passed the chemistry test." Benny steps into frame and says, "No. Tomorrow you enter with Pina. If Stella reacts, we keep the tape."
```

Episode 2 new cliffhanger:

```text
Pina watches the tape and whispers, "Then why is my name on the contract too?"
```

## Render Checklist

- Generate character stills first, then use image-to-video. Do not ask the video model to invent character designs shot by shot.
- Keep every shot under 5 seconds unless it contains an active facial reaction.
- Do not let the model generate text overlays. Add captions, timestamps, and necklace engraving in edit.
- Compare every output to the approved reference pack for fruit texture, eyes, hands, jewelry, and villa lighting.
- Reject any shot where Marco's necklace disappears, Stella's necklace changes shape, or Pina looks like she already knows the truth.
- The full episode is ready only when the final second creates a specific question: what is on the audition tape?
