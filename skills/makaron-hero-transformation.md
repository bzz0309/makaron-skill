---
name: hero-transformation
description: Turn an ordinary selfie into a cinematic 5-stage hero transformation reel. Original archetype-based hero persona — never IP-derived.
allowed-tools: [generate_image, generate_video]
metadata:
  makaron:
    icon: "🦸"
    color: "#F59E0B"
    tags: [hero, transform, cinematic, 5-frame, portrait, reel]
    faceProtection: strict
    defaultAspectRatio: "9:16"
    imageModels: [openai, gemini]
    videoModels: [seedance, kling, seedance-fast]
---

# Hero Transformation — v2

## Core Concept

User uploads 1 selfie photo → agent generates 5 cinematic hero-transformation frames (ordinary → awakening → outfit forming → power surge → heroic stance) → assembles into a 9:16 vertical reveal reel. Each frame uses the same person's face with an original hero persona built from archetype + material palette + signature element — never a known IP character.

## Input Schema

| Field | Required | Type | Default | Description | Example |
|-------|:--------:|------|---------|-------------|---------|
| `selfie_image` | ✅ | image | — | Clear front-facing or 3/4 portrait with visible face. Plain background preferred. | `user-selfie.jpg` |
| `archetype` | ❌ | string | agent picks from allowlist | Hero archetype from allowlist. | `"Storm sentinel"` |
| `material_palette` | ❌ | string | agent picks from allowlist | Primary and accent material from allowlist. | `"liquid silver + sapphire light"` |
| `signature_element` | ❌ | string | agent picks from allowlist | One abstract signature element from allowlist. | `"geometric shoulder guard"` |
| `environment` | ❌ | string | agent picks from allowlist | Final-frame background category. | `"dusk skyline"` or `"mountain peak"` or `"abstract stage"` |
| `duration_seconds` | ❌ | integer | 12 | Total video duration. Range: 10–16. | `12` |

## Safety

### Allowlist — permitted content
- Original hero archetypes: Solar warrior, Storm sentinel, Void walker, Crystal knight, Flame warden, Shadow ranger, Frost guardian, Lightweaver
- Original material palettes: burnished bronze + obsidian crystal, liquid silver + sapphire light, driftwood + amber flame, ember + charcoal, violet + silver
- Original signature elements: geometric shoulder guard, asymmetric circlet, floating orbit ring, cracked-stone gauntlet, abstract energy pattern
- Cinematic environments: dusk skyline, mountain peak, abstract stage, storm clouds, crystal cavern, void backdrop

### Blocklist — FORBIDDEN
- Marvel, DC, anime, game, or franchise characters (Iron Man, Superman, Goku, Thor, Spiderman, Batman, Wonder Woman, Captain America, and all other named IP)
- Real logos, brand marks, emblems, chest symbols, agency marks, heraldry
- Military insignia, real combat gear, national flag motifs, fandom symbols
- Sexualized armor, skin-baring costume, minors in combat styling
- Horror, body horror, warped anatomy, extra limbs, grotesque distortion
- Face swap, face morph, face unrecognizable, beautified beyond recognition
- Recognizable superhero suit or IP-derived armor design

### Identity / Face Rules
- Face must remain recognizable in all 5 frames
- No face swap between frames
- Same person across F1→F5; only outfit and environment change

### Minors / Sexual / Violence Rules
- No minors in intense combat styling
- No sexualized content or skin-baring costume
- No gore, body horror, or explicit violence

### BLOCKED Conditions
Agent returns BLOCKED immediately when:
- selfie_image missing or face not detectable
- Any generated frame contains detectable IP (Marvel/DC/anime/game character)
- Face identity lost after retry
- Safety violation detected (minors, sexualized, horror, military insignia)
- Budget exhausted
Report blocked frame, reason, and ask human.

## Budget

Per-frame generation: openai → retry openai → gemini → BLOCKED. This is 3 attempts per frame max.

| Stage | Max attempts | Fallback chain |
|-------|:-----------:|----------------|
| F1 (Ordinary) | 3 | openai → openai(retry) → gemini → BLOCKED |
| F2 (Awakening) | 3 | openai → openai(retry) → gemini → BLOCKED |
| F3 (Outfit Forming) | 3 | openai → openai(retry) → gemini → BLOCKED |
| F4 (Power Surge) | 3 | openai → openai(retry) → gemini → BLOCKED |
| F5 (Heroic Stance) | 3 | openai → openai(retry) → gemini → BLOCKED |
| Video assembly | 1 | → BLOCKED |
| **Total max** | **15 image + 1 video** | |

Image model chain: openai (default), gemini (fallback).
Video/assembly model chain: seedance (default), kling (fallback).

## Workflow

### Step 1: Validate
- Confirm `selfie_image` received and readable
- Detect face present in input image (analyze_image)
- If `archetype` / `material_palette` / `signature_element` / `environment` not provided by user → agent randomly selects one from allowlist
- If `duration_seconds` not provided → default 12
- If selfie_image missing or no face detected → BLOCKED immediately

### Step 2: Analyze
- Extract face identity cues: gender expression, skin tone, hair color, hair style, face shape, glasses, facial hair
- Extract clothing cues: current outfit color, collar/neckline area
- Note lighting direction and background color for continuity into F2
- Write analysis to plan.json as `identity_cues`

### Step 3: Build plan
Write `plan.json` with:
```json
{
  "archetype": "...",
  "material_palette": "...",
  "signature_element": "...",
  "environment": "...",
  "duration_seconds": 12,
  "identity_cues": { "gender": "...", "skin_tone": "...", "hair": "...", "glasses": "...", "facial_hair": "...", "clothing": "..." },
  "frames": { "f1": { "prompt": "...", "model": "openai" }, "f2": {...}, "f3": {...}, "f4": {...}, "f5": {...} },
  "video_timeline": "0-2s F1→F2 / 2-5s F3 / 5-8s F4 / 8-12s F5"
}
```

### Step 4: Fill prompt templates
Use the templates below. Fill each `{placeholder}` from plan.json and identity_cues. Write final filled prompts into `prompt_used.md`. Do NOT translate, rewrite, add, or remove sentences from the template.

### Step 5: Generate frames
Generate F1→F5 in sequence. For each frame:
- Default model: openai
- QC pass → proceed to next frame
- QC fail → retry once with openai
- Retry also fails → fallback to gemini
- Gemini fails → BLOCKED (report frame number + reason)

### Step 6: QC
Apply per-frame QC checklist (see QC section). If all 5 frames pass → proceed. If any frame fails after budget → BLOCKED.

### Step 7: Assemble video
- All 5 frames must be 9:16 and pass QC
- Assemble using light motion / sequence transition from the 5 approved PNG frames — do NOT let the video model redraw faces
- Use `generate_video` with the 5 frames as reference images, prompt: "Assemble these 5 frames into a 9:16 vertical reel with dissolve transitions. F1→F2 with crossfade, then cut to F3, F4, F5 with light camera motion. Do NOT redraw or change any faces."
- Structure: 0-2s F1→F2 dissolve / 2-5s F3 / 5-8s F4 / 8-12s F5
- If video model redraws identity → BLOCKED

### Step 8: Deliver
Output files (see Output section). Present to user with:
- Final video
- Frame montage (5 frames side by side or sequential)
- Adjust options: "换一个 archetype" / "换 material palette" / "换环境"

---

## Prompt Templates

### F1 — Ordinary Selfie
```
{identity_gender} portrait, {hair_color} {hair_style}, {skin_tone} skin, neutral natural expression. Plain {background_color} background, soft even lighting, no dramatic shadows. Wearing {clothing}. No hero elements, no glow, no dramatic lighting, no costume changes. Keep the original person exactly as-is. Photorealistic, sharp focus on face, 9:16.
```

### F2 — Awakening
```
Same person as reference, {identity_gender}, {hair_color} {hair_style}, {skin_tone} skin. Subtle amber gold light glowing in eyes. Faint energy lines near cheekbones and jaw. Background darkens slightly from {background_color}. Warm cinematic rim light on hair and shoulders. Transformation just beginning — no full suit, no heavy effects, face unchanged. Cinematic portrait, 9:16, photorealistic.
```

### F3 — Outfit Forming
```
Same person, same face. Original {archetype} outfit forming around shoulders and torso from translucent energy. Material: {material_palette}. {signature_element} beginning to materialize. Hair and clothing show slight wind movement. Symbolic cinematic costume — not armor from any IP, no logo, no emblem, no chest symbol. Warm amber rim light, particles near body. Cinematic portrait, 9:16, photorealistic, sharp focus on face.
```

### F4 — Power Surge
```
Same person, same face. Full cinematic energy release. {archetype} outfit now complete: {material_palette}, {signature_element}. Controlled particle burst and lens flare around the body. Expression focused, calm, determined. Face clearly visible and recognizable. Background now dark {environment} environment with atmospheric haze. 9:16, cinematic wide shot, photorealistic, dramatic but controlled lighting.
```

### F5 — Heroic Stance
```
Same person, same face. Calm, confident {archetype} hero pose. Full body visible with complete {material_palette} outfit and {signature_element}. {environment} background, cinematic depth of field, subtle afterglow on edges. No emblem, no logo, no copyrighted motif. The final composed hero portrait. 9:16, photorealistic, cinematic lighting, sharp focus on face.
```

---

## QC

### Per-Frame PASS Checklist
- [ ] Face is recognizable — matches identity_cues from F1 reference
- [ ] No IP character resemblance (Marvel/DC/anime/game check)
- [ ] No logo, emblem, chest symbol, agency mark
- [ ] Frame-specific requirements met (as described per frame)
- [ ] No safety violation
- [ ] 9:16 aspect ratio, photorealistic style

### REROLL Strategy
- **First failure** → retry with same model (openai), same template
- **Second failure** → fallback to gemini model, same template
- **Third failure** → BLOCKED, report frame number and reason
- Reroll triggers: face drift, IP resemblance, over-stylization, missing frame requirement

### Video QC
- [ ] All 5 faces are recognizably the same person across frames
- [ ] Transformation progression is clear in first 2 seconds
- [ ] Output is 9:16 vertical, duration matches `duration_seconds`
- [ ] No identity redraw by video model — faces must match approved frames

### BLOCKED — stop and report
- Face unrecognizable after retry chain
- IP character detected in any frame
- Safety violation (minors, sexualized, horror, military, flag)
- Budget exhausted
- Video model redraws identity

---

## Output

Final deliverables:
- `hero_f1_ordinary.png`
- `hero_f2_awakening.png`
- `hero_f3_outfit_forming.png`
- `hero_f4_power_surge.png`
- `hero_f5_heroic_stance.png`
- `hero_transformation.mp4` — 9:16 vertical reveal reel
- `plan.json` — identity_cues + archetype/material/environment selections + timeline
- `prompt_used.md` — all 5 filled prompt templates exactly as sent to model
- `qc_report.md` — per-frame QC report with required fields

### qc_report.md Required Fields

```json
{
  "skill": "hero-transformation",
  "input_selfie": "<filename>",
  "selected_archetype": "...",
  "selected_material_palette": "...",
  "selected_signature_element": "...",
  "selected_environment": "...",
  "duration_seconds": 12,
  "frames": {
    "f1": { "status": "PASS|REROLL|BLOCKED", "model": "openai|gemini", "attempts": 1, "face_match": "PASS|FAIL", "ip_check": "PASS|FAIL", "notes": "" },
    "f2": { "status": "...", "model": "...", "attempts": 1, "face_match": "...", "ip_check": "...", "notes": "" },
    "f3": { "status": "...", "model": "...", "attempts": 1, "face_match": "...", "ip_check": "...", "notes": "" },
    "f4": { "status": "...", "model": "...", "attempts": 1, "face_match": "...", "ip_check": "...", "notes": "" },
    "f5": { "status": "...", "model": "...", "attempts": 1, "face_match": "...", "ip_check": "...", "notes": "" }
  },
  "video": { "status": "PASS|BLOCKED", "model": "seedance|kling", "face_redraw": "none|detected", "notes": "" },
  "overall": "PASS|BLOCKED",
  "blocked_reason": "",
  "budget_remaining_images": 0,
  "budget_used_images": 0
}
```
