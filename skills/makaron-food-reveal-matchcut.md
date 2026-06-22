---
name: makaron-food-reveal-matchcut
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "🍔"
    color: "#F97316"
    tags: [food, reveal, matchcut, transition, vlog]
    faceProtection: default
    defaultAspectRatio: "9:16"
---

# Food Reveal Matchcut — 空手变食物卡点

Turn food photos into a rhythmic food review reel through empty-hand → food-in-hand match cuts. Same person, same outfit, same background, same hand pose — only the food appears on the beat.

Status: approved as supervised food-reveal matchcut draft.

## Core Concept

Each stop is a **reveal pair**:
1. **Prep frame** — same person, same everything, hand reaching toward camera, **empty hand**
2. **Reveal frame** — same person, same everything, same hand pose, **food appears in hand**

Cut between them exactly on the beat → instant "magical reveal" feel.

## Input

Per stop:
- `food_in_hand_image` — required if user already has a food-in-hand photo
- `food_item` — description (e.g. "matcha latte", "taco")
- `person_reference` — reference photo of the person for face/outfit/bg matching
- `place_name` — optional, for map pin
- `city` — optional
- `map_transition` — optional, true to add map pin chapter

Rules:
- If `food_in_hand_image` exists → generate **only prep frame** to match it
- If no food image → generate **prep + reveal pair** from `food_item` description
- 2–5 stops recommended, 3–4 ideal for 12–15s

## Safety

- Food items only — no weapons, no dangerous objects, no body parts as food
- Face preserved across all frames
- If reference appears underage: no suggestive hand gestures → BLOCKED
- No real brand logos — obscured or generic

## Budget

- Per stop: max 2 images (1 prep + 1 retry)
- If generating reveal pair: max 2 images per stop (1 prep + 1 reveal, no retry each)
- Max video attempts: 1
- Still failing → BLOCKED, ask human

## Pipeline

### Step 1 — Analyze Input
For each stop, if `food_in_hand_image` exists, call analyze_image. Extract: face, outfit, background, lighting, camera angle, arm position, hand pose, finger position. This is the blueprint for the prep shot.

### Step 2 — Generate Prep Frame
Generate identical scene but hand is EMPTY. Same face, same outfit, same background, same lighting, same camera angle, same arm position, same hand reaching toward camera. Fingers slightly open, palm up or reaching forward. No food, no object. Just empty hand. 9:16 vertical.

### Step 3 — Verify Pair Alignment
Check prep frame against reveal frame (or original food image). Must match on all:
- Same face ✓
- Same outfit ✓
- Same background ✓
- Same camera angle ✓
- Same hand pose ✓
- Only food differs ✓
- Hands natural, no extra fingers ✓
- Food not floating, contact with hand plausible ✓

Mismatch → REROLL (max 1 retry per pair).

### Step 4 — Chain into Video
Sequence per stop:
```
0.0–1.0s:   Map pin + place name (optional, generic map style only)
1.0–1.8s:   Prep frame — person empty hand reaching toward camera
1.8s:       BEAT CUT / snap / flash
1.8–2.8s:   Reveal frame — food appears in hand
2.8–3.5s:   Reaction — smile, hand heart, cheers, or bite (optional)
3.5s:       Map swipe to next stop
```

3–4 stops = 12–15s total. Music-driven rhythm. Clean cuts or snap zooms exactly on beat.

### Step 5 — QC

| Outcome | Condition | Action |
|---------|-----------|--------|
| PASS | All pairs aligned, face preserved, hand pose consistent, food clear, cuts on beat, each stop distinguishable | Deliver |
| REROLL | Face drift, outfit mismatch, background shift, hand pose wrong, food floating/blurry, style inconsistent (max 1 retry per pair) | Regenerate |
| BLOCKED | Cannot match prep, over budget, face lost, brand/IP, hand deformation, map uses real Google logo/fake ratings | Halt |

### Pair Alignment Checklist (per stop)
- [ ] Same face
- [ ] Same outfit
- [ ] Same background
- [ ] Same camera angle
- [ ] Same hand pose
- [ ] Only food differs
- [ ] Hands natural, no extra fingers
- [ ] Food not floating, contact with hand plausible

#### Map Rules
Generic map app style only. No Google Maps logo/UI. No fake ratings, reviews, route lines, or business hours. Chapter transition only: pin + city label + next stop name.

## Negative

- No different face between prep and reveal
- No different outfit, no different background
- No weapon or dangerous object in hand
- No body parts as food
- No suggestive hand gestures
- No real brand logos
- No extra fingers, no deformed hands
- No floating food — must have plausible contact with hand
- No real Google Maps / map app branding
- No fake ratings or reviews
- No face swap

## Delivery

- `food_reveal_matchcut.mp4` (12–18s, 9:16)
- `cover_frame.jpg` (from best reveal frame)
- `prep_frames/stop_01_prep.png`, `stop_02_prep.png`, ...
- `reveal_frames/stop_01_reveal.png` or use user's original food images
- `edit_timeline.json`
- `prompt_used.md`
- `qc_report.md`

## Design Principles

1. Match cut is everything — same person, same everything, only food changes
2. Beat-synced cuts — snap or flash exactly on the beat
3. Hand is the hero — consistent hand pose anchors the reveal
4. Each stop visually distinct — different background, different food, different vibe
5. Fast rhythm — 0.8–1.2s prep, beat, 0.8–1.5s reveal, no lingering
