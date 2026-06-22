---
name: hero-transformation
allowed-tools: [generate_image, generate_video]
metadata:
  makaron:
    icon: "🦸"
    color: "#F59E0B"
    tags: [hero, transform, cinematic, 5-frame, portrait, reel]
    faceProtection: strict
    defaultAspectRatio: "9:16"
    modelPreference: [openai, gemini]
---

# Hero Transformation

## Core Concept

ordinary selfie → 5-frame original cinematic hero transformation → vertical reveal reel.

The result should feel like an original cinematic hero persona, not any existing superhero / anime / game / franchise character.

## Pipeline

Generate 5 designed frames, then assemble into a 9:16 transformation reel.

### F1 — Ordinary Selfie
Baseline frame. Keep the original person as-is.
- neutral / natural expression
- no hero elements
- no glow
- no dramatic lighting
- no costume changes

### F2 — Awakening
Same face and identity cues.
- subtle amber / gold eye glow
- faint energy lines near cheekbones or jaw
- background darkens slightly
- warm cinematic rim light
- transformation just beginning
Avoid: full suit, heavy effects, face change.

### F3 — Hero Outfit Forming
Same face.
- original energy-forged hero outfit begins forming around shoulders / torso
- symbolic cinematic costume, not armor from any IP
- material can feel like bronze, obsidian, crystal, light-weave, fabric, or energy
- hair / clothing may show slight wind movement
- no logo, emblem, chest symbol, flag, agency mark
Avoid: recognizable superhero suit, military gear, copied armor, face drift.

### F4 — Power Surge
Same face.
- full cinematic energy release
- outfit now complete
- particles / lens flare allowed but controlled
- expression focused, calm, determined
- keep face visible and recognizable
Avoid: overexposure, screaming face, horror, IP-like costume.

### F5 — Heroic Stance
Final composed hero portrait.
- calm confident hero pose
- cinematic environment, e.g. dusk skyline / mountain / abstract stage
- subtle afterglow
- original outfit visible
- no emblem / logo / copyrighted motif
This is the final hold frame.

## Video Assembly

- 9:16 vertical
- 0–2s: F1 → F2 hook, ordinary person begins awakening
- 2–5s: F3 outfit forming
- 5–8s: F4 power surge
- 8–12s: F5 heroic stance
- 12–16s: hold F5 with subtle motion / final reveal

Use clean cuts or light dissolve. Do not let the video model redraw the identity if simple frame assembly is enough.

## Identity Construction Rules

Use original archetypes only. Do not use existing character names.

Allowed archetype examples:
- Solar warrior
- Storm sentinel
- Void walker
- Crystal knight
- Flame warden
- Shadow ranger
- Frost guardian
- Lightweaver

Original material palette examples:
- burnished bronze + obsidian crystal
- liquid silver + sapphire light
- driftwood + amber flame
- ember + charcoal
- violet + silver

Allowed signature elements:
- geometric shoulder guard
- asymmetrical circlet
- floating orbit ring
- cracked-stone gauntlet
- abstract energy pattern

Forbidden:
- Marvel, DC, anime/game/franchise characters
- superhero names
- real logos
- chest emblems
- agency marks
- fandom symbols
- national flag motifs

## Safety

Red lines:
- Face identity must remain recognizable.
- No real brand logos.
- No trademarked hero costumes.
- No copyrighted fandom art.
- No military insignia or real combat gear.
- No sexualized armor / skin-baring costume.
- No horror or body horror.
- No minors in intense combat styling.
- No face swap.

## Budget

- Max 10 image generations total.
- Each frame gets 1 main attempt + 1 retry.
- Max video assembly attempts: 1.
- If still failing after budget: BLOCKED and ask human.

## QC

### PASS
Pass only if:
- all 5 frames preserve identity cues
- transformation is clear by F2 within first 2 seconds
- outfit is original and non-IP
- face is visible in every frame

### REROLL
- face drift / identity cues lost
- transformation unclear by F2
- outfit resembles known IP
- over-stylization or distortion
Max 1 retry per frame within budget.

### BLOCKED
- cannot preserve face after retry
- IP detected
- safety violation (minors, horror, sexualized)
- over budget
Report which frame and why, then ask human.

## Negative (Global)

different face, unrecognizable, face swap, face morph, beautified beyond recognition,
Iron Man, Superman, Goku, Thor, Spiderman, Batman, Wonder Woman, Captain America,
Marvel, DC, anime character, game character, IP character,
logo, emblem, heraldry, brand, trademark, chest symbol, agency mark,
military insignia, real combat gear,
warped anatomy, extra limbs, grotesque, body horror,
sexualized, skin-baring armor, minors in combat styling,
fandom symbols, national flag motifs

## Delivery

- `hero_f1_ordinary.png`
- `hero_f2_awakening.png`
- `hero_f3_outfit_forming.png`
- `hero_f4_power_surge.png`
- `hero_f5_heroic_stance.png`
- `hero_transformation.mp4` — 9:16 vertical reveal reel (12–16s total)
- `prompt_log.md`
- `qc_report.md`
