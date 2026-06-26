# Fan Meeting — K-Pop Idol Fan Signing Video

## Metadata
```yaml
name: Fan Meeting
id: makaron-fan-meeting
description: One selfie → you are the K-pop idol at your own fan signing event. Cute accessories, signing table, real fan interaction, camera flash effects — 8s video. Male & female universal.
category: video
tags: [fan-meeting, kpop, idol, signing, fansign, event, meet-and-greet, interact, boy-group, girl-group, flash, photocard, aegyo]
allowed-tools: [generate_image, generate_animation]
ratio: "9:16"
duration: 8
version: "1.0.0"
author: makaron

# Makaron marketplace metadata
makaron:
  internalName: makaron-fan-meeting
  displayName: Fan Meeting
  category: video
  engine: seedance
  previewVideo: ""
  pricing: free
```

## Overview
Upload **one selfie** → become a K-pop idol at your own fan signing event. Sit at the signing table in a cute accessory + outfit combo, interact warmly with fans, sign albums, make heart gestures — all captured with **camera flash effects** like a real fansign photoshoot. 1080p, 9:16 vertical, 8 seconds. **Works for both male and female idols.**

## What Users Provide
- **1 selfie/portrait photo** (face clearly visible, well-lit, front-facing)
- **Optional preferences:**
  - Hair color (default: ash blonde for female, natural dark for male)
  - Accessory + outfit combo from the styling table below
  - Gender preference (auto-detected from photo if not specified)

## Generated Assets (Internal)
The skill generates **4 style reference images** before rendering the video. Each image uses the user's face identity with K-pop idol styling.

| # | Image | Description |
|---|-------|-------------|
| 1 | **idol_portrait.jpg** | Close-up portrait: idol in the chosen accessory + outfit combo. K-pop glass dewy skin, soft brown gradient eye makeup, defined lash line, pink glossy lips, aegyo sal highlight. Hair styled with soft voluminous waves, glossy healthy shine. Warm smile, eye contact with camera. Clean neutral background. |
| 2 | **signing_table.jpg** | Medium shot: idol seated at a dark blue signing table, hands resting on the table. Wooden chair behind, clean gray wall. Warm approachable smile. Soft diffused studio/event lighting. |
| 3 | **interaction_moment.jpg** | Over-the-shoulder shot: idol leans forward toward a fan standing in front (fan seen from behind, casual dark sweater). Reaching one hand out warmly, bright eyes making eye contact. Intimate connection moment. Dark blue tablecloth. |
| 4 | **ending_pose.jpg** | Close-up: idol makes a cute finger heart gesture with both hands at chest. Big warm smile, sparkling eyes, slight head tilt. Happy fansign ending energy. Clean gray background. |

## Video Structure (8s, with Camera Flash Effects)

### 0-2s: Sit Down & Adjust Accessory
```
<<<media_2>>> establishing shot.
The idol walks in, sits down at the signing table, reaches up to adjust the cute headband.
Brief camera flash strobe (white flash blinks once).
Hands rest on the dark blue tablecloth. Warm smile at the camera. Background has subtle sparkle bokeh from camera flashes.
```

### 2-4s: Lean In & Greet Fan (Interaction)
```
<<<media_3>>> over-the-shoulder interaction shot.
A fan stands in front of the table (seen from behind).
Multiple rapid camera flashes pop from the sides — paparazzi-style white strobe flickers.
The idol leans forward toward the fan, eyes bright, reaching out one hand slightly.
Real conversation energy. Flash reflections catch in glossy hair.
```

### 4-6s: Sign Album + Talk (Action)
```
<<<media_1>>> close-up of idol.
Idol picks up a marker, signs an album. Intermittent soft camera flashes illuminate the face.
Looks up at the fan while signing. Mouth moves slightly (talking). Nods, smiles naturally.
The flash catches the shine in her/his eyes. Dewy skin glows under the flash light.
```

### 6-8s: Heart Gesture + Flash Burst + Wave
```
<<<media_4>>> final pose.
Idol makes a finger heart gesture with both hands at chest.
A burst of rapid camera flashes (3-4 quick white strobes) lights up the scene.
Big warm smile, slight head tilt. Accessory bounces slightly. Quick wave goodbye. Fade to white.
```

## Idol Styling — K-Pop Makeup Standard

All generated images must apply this K-pop idol beauty standard (regardless of user photo):

### Skin
- **Glass dewy finish** — luminous, hydrated, poreless-looking but not artificial
- No heavy matte foundation
- Subtle highlight on cheekbones, nose bridge, brow bone

### Eyes
- **Soft brown gradient eyeshadow** on upper lids, slightly deeper at outer corners
- **Defined lash line** — thin eyeliner close to lash line, subtle wing
- **Natural lash enhancement** — mascara or natural-looking false lashes for volume
- **Aegyo sal highlight** — subtle shimmer under the eye bags for bigger, brighter eyes
- **Circle lens effect** — eyes appear slightly larger and brighter (like colored contact lenses)
- Eyebrows: softly defined, following natural shape

### Lips
- **Soft pink gradient lip** — darker inner, lighter outer (Korean gradient lip style)
- Glossy or semi-matte finish
- Natural "my lips but better" tone

### Hair
- **Polished, glossy shine** — healthy, luminous finish
- **Soft voluminous waves** or sleek straight — never flat or messy
- **Center part** preferred
- Hair color options:
  - _Ash blonde_ (default female) — light platinum/ash blonde
  - _Honey brown_ — warm medium brown with golden tones
  - _Natural black_ (default male) — rich glossy black
  - _Rose gold_ — pinkish warm blonde (female)
  - _Silver lavender_ — pale purple-grey (female/unisex)
  - _Navy blue tips_ — dark base with colored ends (unisex)

## Outfit + Accessory Combos

Each combo = accessory + top + vibe. User picks or system selects based on gender.

### Female Default Combos
| # | Combo | Accessory | Top | Vibe |
|---|-------|-----------|-----|------|
| 1 | 🐰 **Bunny Sweet** | White plush bunny ears, pink inner ears | White lace-trim camisole | Soft, innocent, classic fansign |
| 2 | 🎀 **Red Bow** | Large red satin bow headpiece | White lace camisole | Bold, eye-catching, aegyo queen |
| 3 | 👑 **Tiara** | Crystal tiara / small crown | Pastel pink knit sweater | Elegant princess, soft dreamy |
| 4 | 🐱 **Cat Playful** | Black cat ears + silver bell | Off-shoulder white blouse | Mischievous, flirty, energetic |
| 5 | 🌸 **Flower Fairy** | Flower crown (cherry blossom) | Light blue lace camisole | Fresh, spring, romantic |
| 6 | ⭐ **Stage Star** | Rhinestone headband + star pins | Black sequin crop top | Glam, comeback stage energy |

### Male Default Combos
| # | Combo | Accessory | Top | Vibe |
|---|-------|-----------|-----|------|
| 1 | 🐰 **Bunny Boy** | White plush bunny ears, pink inner ears | White slim-fit tee | Playful fan-service, cute but masculine |
| 2 | 🧢 **Street Idol** | Black baseball cap | Oversized pastel hoodie | Boyfriend vibe, approachable |
| 3 | 🐻 **Bear Hug** | Brown bear ear headband | Cream knit sweater | Cozy, soft, cuddly |
| 4 | 👔 **Suave** | No head accessory, styled hair | White button-up, top buttons open | Mature, charismatic, fan-meet elegant |
| 5 | 🐱 **Kitty Boy** | Black cat ear headband | Black slim-fit turtleneck | Edgy but cute, NCT/WayV energy |
| 6 | ⭐ **Stage King** | Rhinestone headband | Black sequin jacket | Glam comeback, performer |

**Mix & match:** Any accessory can pair with any outfit regardless of gender. "Bunny ears + hoodie" or "cap + lace cami" all valid.

### Makeup for Male Idols
- Same glass skin base, but slightly less glossy (semi-matte)
- Subtle brown eyeshadow at lash line, no visible wing
- Natural brow grooming, slightly straighter shape
- MLBB lip tint (sheer peach/pink)
- No heavy aegyo sal — subtle brightening only
- Hair: glossy healthy texture, soft volume

## Camera & Lighting Style

### Lighting
- Soft diffused studio/event lighting (no harsh shadows)
- Mixed with intermittent white camera flash strobes throughout video
- Flash reflections in glossy hair and on dewy skin
- Warm 3200-4000K color temperature

### Camera
- Medium close-up shots (face + upper body)
- Over-the-shoulder angles for fan interaction scenes
- 1080p final output
- Shallow depth of field (background slightly blurred)
- Steady, smooth camera movement
- Behind-the-scenes / fansign photoshoot aesthetic — not sterile studio

### Background
- Clean gray wall (minimal, distraction-free)
- Dark blue tablecloth on signing table
- Wooden-backed chair
- Subtle sparkle bokeh from off-screen camera flashes

## Test Cases (Verified)

| # | Input | Hair | Combo | Expected |
|---|-------|------|-------|----------|
| 1 | Female, Asian | Ash blonde | Bunny Sweet | White lace cami, bunny ears, glass skin, flash effects ✅ |
| 2 | Male, Asian | Natural black | Bunny Boy | White tee, bunny ears, semi-matte skin, same interaction ✅ |
| 3 | Female, Caucasian | Rose gold | Red Bow | Red bow + lace cami, face identity preserved ✅ |
| 4 | Male, Caucasian | Natural black | Street Idol | Cap + hoodie, warm smile, identity preserved ✅ |
| 5 | Any gender | Any | Cat Playful | Cat ears rendering correctly, gender-neutral ✅ |

## Edge Cases
- **Glasses** → keep them on the idol
- **Bangs/fringe** → preserve style, place headband on top of hair
- **Beard/facial hair** (male) → keep it, styled neatly
- **Low quality / blurry photo** → request clearer photo before proceeding
- **Group photo** → ask user to crop to single person
- **Side profile / not facing camera** → request front-facing photo

## Output Specification
- **Format:** MP4 video
- **Resolution:** 1080 x 1920 (9:16 vertical)
- **Duration:** 8 seconds
- **Frame rate:** 24fps
- **Engine:** Seedance (Makaron) / video generation API (other platforms)
- **Face identity:** Consistent with user photo throughout all frames and video
- **Delivery:** Single video file
