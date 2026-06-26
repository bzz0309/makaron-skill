---
name: game-character-demo-video
description: >
  Generate a 9:16 game character demo video from a single uploaded line-art
  sketch, concept image, character artwork, selfie/photo, or text prompt. The
  template shows each character one at a time: sketch/concept form transforms
  into a polished AAA/anime game character with red-black graphic transitions,
  glass shards, hero cards, and dynamic action close-ups. If the input is a
  normal selfie or photo, first create a matching line-art game concept sketch,
  then animate the sketch-to-final game-character transformation. Use for
  Makaron image-to-video or text-to-video game promo effects.
allowed-tools: analyze_image generate_image generate_video generate_animation
metadata:
  makaron:
    icon: "gamepad-2"
    color: "#E5322D"
    tags: [video, game, character, anime, sketch-to-game, template]
    tipsEnabled: true
    tipsCount: 4
    modelPreference: [seedance, kling, gemini]
    faceProtection: default
    defaultAspectRatio: "9:16"
---

# Game Character Demo Video

Create a vertical game character promo where a sketch, concept image, selfie, or ordinary photo becomes a polished in-game hero. The default flow is one character at a time, like the reference video: sketch/concept frame first, then a red-black transformation into the final game character, then an action close-up.

Do not require users to upload one vertical sheet containing 2-3 character sketches. A single uploaded sketch or selfie is enough. If the user provides multiple references, switch between 2-3 characters. If the user provides one selfie/photo, first create a line-art game concept sketch from that photo, then transform it into a final AAA/anime game character.

## Default Output

- 9:16 vertical video.
- Default duration: 6 seconds for one uploaded sketch/photo; 8-10 seconds for multiple characters.
- Visual style: red-and-black high contrast, anime/AAA game promo, bold uppercase typography, floating glass shards, white flash transitions, snap zooms, and parallax.
- Single-character structure: sketch/concept reveal -> red-black transition -> final polished game character -> action close-up -> hero card.
- Multi-character structure: repeat the same sketch-to-final transformation for 2-3 separate characters, one after another.
- If the user uploads a line-art sketch, preserve that sketch as the identity source.
- If the user uploads a normal selfie/photo, preserve the person's general face vibe, hairstyle, clothing color cues, and attitude while turning them into an original game character.
- Do not generate watermarks, tutorial captions, phone UI, play buttons, prompt cards, creator labels, or platform interface.

## Core Effect

The video must clearly show these beats:

1. A rough sketch, line drawing, clean concept frame, or white-background design of a character.
2. A fast red-black graphic transition with glass shards, scan lines, flash, cursor/selection spark, or panel wipe.
3. The same character becomes a polished final game hero: realistic/anime game render, full color, cinematic lighting, detailed armor/outfit, weapon, and effects.
4. A dynamic close-up or action pose: drawing a weapon, aiming, lunging, power charge, eye glow, punch, kick, blade sweep, or magic shield.
5. Repeat for 2-3 different characters only when the user provides multiple references or asks for a lineup/team.

Use roster UI only as a supporting transition. The main hook is the transformation from sketch/concept/photo-derived sketch into the final in-game character.

## Workflow

### Step 1: Read The Input

If the user uploads one image:
- If it is line art/concept art, use it directly as the sketch/concept phase and preserve its design.
- If it is a finished character image, first create or imply a matching rough sketch/concept version, then transform into the final game render.
- If it is a selfie or ordinary photo, create a matching line-art game character concept sketch first. Preserve the person's general face vibe, hairstyle, outfit color cues, and attitude, but reinterpret them as an original game hero. Then animate from that sketch into the final polished hero.
- Do not ask the user for more characters. A single uploaded sketch/photo should produce a complete single-character transformation video.

If the user uploads multiple images:
- Use up to 3 images as separate characters.
- Keep each character visually distinct.
- Do not merge all references into one character unless the user asks for a single hero.

If the user gives text only:
- If the prompt describes one character, create one sketch/concept frame, then transform it into one polished game hero.
- If the prompt describes a team/lineup, invent 2-3 distinct characters from the prompt.
- Give each character a short uppercase name and a different role, weapon, and silhouette.

### Step 2: Choose Single Or Multi-Character Mode

Use single-character mode by default when the user uploads one image or describes one character.

Single-character mode needs:
- One short uppercase name.
- One sketch/concept form.
- One final polished game render form.
- One signature action close-up.

Use 2-3 character mode only when the user uploads multiple images, asks for several characters, or asks for a lineup/team.

Multi-character mode needs, for each character:
- Short uppercase name.
- Unique silhouette.
- Different color palette.
- Different role or weapon.
- Visible sketch/concept phase.
- Polished final game render phase.
- One signature action.

Example lineup:
- NYXARA: black-and-gold cyber valkyrie assassin, twin plasma daggers, amber eyes.
- ORION VEIL: blue hooded techno mage, floating rings, energy shield.
- KIRA VANTA: red heavy gunner, bulky armor, shoulder cannon.

Avoid protected or famous character names.

### Step 3: Generate Or Prepare The Sketch Anchor

For selfie/photo inputs, generate a matching line-art concept sketch first:

```text
Convert the uploaded photo into a clean game character line-art concept sketch.
Preserve the person's general face vibe, hairstyle, outfit cues, and attitude,
but reinterpret them as an original AAA/anime game hero. White or light paper
background, pencil/ink sketch lines, full-body or half-body concept pose,
clear silhouette, no color render yet, no watermark, no phone UI.
```

For text-only single-character requests, generate one clean sketch/concept anchor first:

```text
Create a clean white-background line-art concept sketch of one original game
hero based on this description: [USER_TEXT]. Pencil/ink sketch lines, clear
silhouette, outfit and weapon design visible, no full-color render yet, no
watermark, no phone UI.
```

Do not create one vertical sheet with 2-3 stacked characters by default. Show characters one at a time in the video, like separate concept frames.

### Step 4: Generate The Video

Single-character prompt:

```text
Create a 6-second 9:16 vertical cinematic game character demo video.
The core effect is sketch-to-final transformation. Use the provided sketch or
generated line-art concept frame as the starting point.

0.0-1.4s: Show the character as rough line art / white-background concept art /
clean sketch frame. Add subtle paper texture, pencil lines, and faint UI scan
lines.

1.4-3.0s: Red-black graphic transition: white flash, glass shards burst across
the foreground, bold uppercase character name appears, panels slide in. The
sketch transforms into the final polished AAA/anime game character render in
full color, with detailed outfit/armor/weapon and cinematic lighting.

3.0-4.8s: Action close-up: weapon draw, eye glow, lunge, punch, kick, magic
shield, or power charge. Fast push-in, slight shake, motion blur, glass streaks.

4.8-6.0s: Final hero card / impact pose: transformed character in polished game
render form, red-black panels behind them, floating glass shards, bold uppercase
name, cinematic game promo lighting.

Style: polished AAA/anime mobile game promo, red-black graphic design, bold
condensed typography, sketch lines becoming realistic game character, glass
fragments, snap zooms, white flash transitions, parallax, high contrast.

No watermark, no tutorial text, no creator label, no subtitles unless requested,
no phone UI, no app interface, no random logos, no calm portrait slideshow.
Keep the character identity consistent from sketch to final render.
```

Multi-character prompt:

```text
Create an 8-10 second 9:16 vertical cinematic game character demo video.
Show 2-3 different characters one at a time. For each character: start with a
separate sketch/concept frame, transform through red-black panels, white flash,
and glass shards into the final polished AAA/anime game character, then show a
short action close-up. Do not show all sketches stacked in one static sheet.

End with a final transformed lineup / impact montage with red-black panels,
floating glass shards, bold uppercase names, and cinematic game promo lighting.
No watermark, no tutorial text, no phone UI.
```

Recommended parameters:
- `aspectRatio: "9:16"`
- `duration: 6 seconds` for one uploaded sketch/photo.
- `duration: 8-10 seconds` for 2-3 character lineups.
- Prefer `videoModel: "seedance"`. If action is weak, try `kling`.
- If photo-to-sketch-to-final fails in one pass, first generate the line-art concept sketch as an image, then use that sketch as the video reference.

Negative prompt:

```text
watermark, tutorial caption, creator label, app UI, phone screen, play button,
green outline box, random logo, unreadable messy text over face, identity drift,
calm portrait slideshow, static poster only, no sketch phase, no transformation,
soft pastel background, deformed hands, extra limbs, melted weapon
```

### Step 5: Quality Check

Before delivery, verify:
- The video shows sketch/line-art/concept form before the final game render.
- For a single uploaded image, one strong character transformation is enough.
- For multiple references or a lineup prompt, at least 2 different characters appear, preferably 3.
- Each character has a distinct silhouette, role, costume, and action in multi-character mode.
- There is a clear transition from sketch to final render.
- Red-black panels, glass shards, flash, or roster UI elements appear as the visual language.
- The final render looks like a polished game character, not a flat illustration only.
- No watermark, tutorial caption, or phone UI.

If the result fails, regenerate using the correction prompts below.

## Correction Prompts

If it only shows a roster:

```text
The main hook must be sketch-to-final transformation. Add visible rough line art
or white-background concept art before the final game character render. Roster
UI is only a transition element, not the whole video.
```

If there is no transformation:

```text
Show the character starting as rough line art / pencil sketch / concept frame,
then transform through a red-black flash into a polished AAA/anime game render.
Make the before/after transformation visually obvious.
```

If a selfie/photo loses identity:

```text
Preserve the uploaded person's general face vibe, hairstyle, outfit color cues,
and attitude. First show a line-art game concept sketch based on the photo, then
transform that sketch into a polished game hero.
```

If multiple references collapse into one character:

```text
Keep each uploaded reference as a separate character. Show each one at a
different time, with its own sketch phase, transformation, final render, and
signature action.
```

## Reusable Prompt Script

To generate a stable prompt pack:

```bash
python3 scripts/build_prompt.py --character "NYXARA" --mode single --input-mode photo --style "black-and-gold cyber assassin" --duration 6
```

The script only generates prompts. It does not depend on the Makaron API and contains no credentials.
