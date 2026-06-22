---
name: makaron-location-food-popin
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "📍"
    color: "#F97316"
    tags: [food, location, reveal, popin, checkin, transition]
    faceProtection: default
    defaultAspectRatio: "9:16"
---

# Location Food Pop-in — 地点打卡 + 伸手 + 食物弹出

Different locations, same empty-hand reach, different food pops in on the beat. Each stop is a tight 2-second reveal: location check-in → empty hand → beat cut → food appears in hand. No map, no full vlog — just the pop-in trick.

Status: approved as supervised location-food-popin draft.

## Core Concept

```
Location A: check-in → empty hand reach → CUT → food A in hand
Location B: check-in → empty hand reach → CUT → food B in hand
Location C: check-in → empty hand reach → CUT → food C in hand
```

Each stop is ~2s:
```
0.0–0.8s:   Location check-in + person reaches hand toward camera, hand empty
0.8s:       BEAT CUT / snap / flash
0.8–1.8s:   Same composition, same hand, food appears in hand
1.8–2.0s:   Light reaction — smile, bite, or hold
```

3–5 locations = 6–10s total. No map pins, no swipe transitions — just location → reach → pop-in → next location.

## Input

Per location:
- `location_name` — e.g. "Shinjuku ramen alley", "Shibuya crepe stand"
- `food_item` — description (e.g. "tonkotsu ramen", "strawberry crepe")
- `food_image` — optional real food photo. If provided, paste it onto the hand instead of generating food
- `location_background` — optional background photo for the location
- `person_reference` — reference photo of the person for face/outfit matching

2–5 locations recommended, 3–4 ideal.

## Safety

- Food items only — no weapons, no dangerous objects, no body parts as food
- Face preserved across all frames
- If reference appears underage: no suggestive hand gestures → BLOCKED
- No real brand logos on food packaging — obscured or generic
- Real location names allowed, but do not generate real logos, storefront signage, ratings, official recommendations, or advertising endorsements. Default to generic storefront / location vibe

## Budget

- With `food_image` provided: max 1 prep generation + 1 retry per location
- Without `food_image`: max 2 frame generations (prep + reveal) + 1 retry per location
- Max video attempts: 1
- Still failing → BLOCKED, ask human

## Pipeline

### Step 1 — Analyze Person Reference
Call analyze_image. Extract: face, outfit, build. This is the constant across all locations.

### Step 2 — For Each Location: Generate Check-in Prep Frame
Generate person standing at the location, hand reaching toward camera, hand EMPTY. Same person, same outfit. Background matches location vibe. Hand is natural, palm facing camera or slightly angled, fingers open, ready to hold food. 9:16 vertical.

### Step 3 — For Each Location: Prepare Food-in-Hand Frame
- If `food_image` provided → same composition as prep frame, integrate the provided food image into the reveal frame using available image generation/editing runtime, with plausible grip/contact
- If no food image → generate same composition, same hand, food item appears in hand

### Step 4 — Verify Per-Location Alignment
Check prep frame against food-in-hand frame for each location. Must match:
- Same face ✓
- Same outfit ✓
- Same location background ✓
- Same camera angle ✓
- Same hand pose ✓
- Only food differs ✓
- Hands natural, no extra fingers ✓
- Food not floating, contact with hand plausible ✓
- Locations visually distinct from each other ✓
- Same location: prep and reveal must match on everything except food ✓
- Different locations: background may differ, but face and outfit must remain stable ✓

Mismatch → REROLL (max 1 retry per location).

### Step 5 — Compile Video
Chain locations sequentially:
```
Location A: check-in (0.8s) → CUT → food A reveal (1.0s) → reaction (0.2s)
Location B: check-in (0.8s) → CUT → food B reveal (1.0s) → reaction (0.2s)
Location C: check-in (0.8s) → CUT → food C reveal (1.0s) → reaction (0.2s)
```

3 locations = ~6s, 5 locations = ~10s. Beat-synced cuts. Clean snap transition between locations.

### Step 6 — QC

| Outcome | Condition | Action |
|---------|-----------|--------|
| PASS | All pairs aligned, face consistent, hand pose natural, food makes contact, locations distinguishable, cuts on beat | Deliver |
| REROLL | Face drift, hand deformation, food floating, location backgrounds too similar, style inconsistent (max 1 retry per location) | Regenerate |
| BLOCKED | Cannot match prep, over budget, face lost, brand/IP, food looks disgusting | Halt |

### Per-Location Pair Checklist
- [ ] Same face
- [ ] Same outfit
- [ ] Same location background
- [ ] Same camera angle
- [ ] Same hand pose (natural, reaching toward camera)
- [ ] Only food differs between prep and reveal
- [ ] Hands natural, no extra fingers
- [ ] Food not floating — plausible contact with hand
- [ ] Location visually distinct from other locations

## Negative

- No different face between prep and reveal
- No different outfit, no different background within same location
- No weapon or dangerous object in hand
- No body parts as food
- No suggestive hand gestures
- No real brand logos or branded packaging
- No extra fingers, no deformed hands
- No floating food — must have plausible contact with hand
- No face swap
- No map UI, no fake ratings, no Google/Apple Maps branding
- No real store logos, no real signage, no real ratings or official endorsements

## Delivery

- `location_food_popin.mp4` (6–12s, 9:16)
- `cover_frame.jpg` (from best reveal)
- `checkin_frames/loc_01_checkin.png`, `loc_02_checkin.png`, ...
- `reveal_frames/loc_01_reveal.png`, `loc_02_reveal.png`, ... (or original food images composited)
- `edit_timeline.json`
- `prompt_used.md`
- `qc_report.md`

## Design Principles

1. Tight 2s per stop — no filler, pure pop-in trick
2. Same person across all locations — outfit constant, only location and food change
3. Hand is the star — consistent reach, natural pose, anchors the reveal
4. Real food photos prioritized — composite when available, generate only when not
5. Locations visually distinct — each one reads as a different place instantly
