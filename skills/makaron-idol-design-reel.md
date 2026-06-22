---
name: makaron-idol-design-reel
description: >
  Transform a selfie into a K-pop idol fan-design process reel — photocard frame,
  color palette, flat illustration, brand card. The output is a 16s 9:16 video
  that looks like a professional Korean digital artist's creation reel.
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "🎴"
    color: "#C084FC"
    tags: [kpop, idol, photocard, design-reel, flat-illustration, fandom, editorial]
    faceProtection: default
    defaultAspectRatio: "9:16"
---

# Idol Design Reel — 偶像设计卷

Turn a selfie into a K-pop idol fan-design process reel. The output is a 16s 9:16 vertical video that moves through 4 curated design frames — photocard border, color palette system, flat illustration, and brand card — exactly like a professional Korean digital artist's creation reel.

Status: draft for supervised generation.

## Core Concept

```
Selfie → Photocard Frame → Color System → Flat Illustration → Brand Card
  0-2s       2-6s            6-10s         10-14s            14-16s
```

Each frame is a polished standalone image. The video cuts or dissolves between them. NOT a smooth animation — this is a process reel format where each frame is a designed page.

## Safety Boundaries

- No real brand logos, broadcast station logos, or trademarked fandom merchandise
- All Korean text is generic (no real idol names, group names, or agency names unless user owns the rights)
- Color palette and illustration style are original creations, not copies of existing fan-art
- Face preserved from original photo in all frames

## Budget

- Max image generations: 5 (1 per frame + 1 retry)
- Max video attempts: 1
- Still failing → BLOCKED, ask human

## Pipeline

### Step 1: Analyze Input
Call analyze_image. Extract face, hair, outfit, expression, overall vibe.

### Step 2: Generate Frame 1 — Photocard Frame (0-2s)
Prompt: "Korean idol photocard frame design. The person from the reference photo inside a glossy photocard border with rounded corners. Soft pastel border with subtle gradient, generic Korean text date stamp at bottom, film strip edge on one side, slight paper texture. Clean composition, center the face. 9:16 vertical. Face preserved exactly."

### Step 3: Generate Frame 2 — Color System (2-6s, transition at 6s)
Prompt: "Korean graphic design color palette page. Split layout — left side shows the person from the reference photo in a small circular crop, right side shows 4-5 color swatches extracted from their outfit/vibe. Pastel K-pop aesthetic, clean grid layout, generic Korean label text for each color swatch. Editorial magazine feel. 9:16 vertical. Face preserved exactly."

### Step 4: Generate Frame 3 — Flat Illustration (6-10s, transition at 10s)
Prompt: "Flat vector illustration style portrait of the person from the reference photo. Korean digital artist style — simplified facial features, soft round shapes, minimal linework, pastel color blocking. Include small decorative elements around the illustration (stars, sparkles, flower petals). No shading, clean flat colors. The original photo face should be recognizable in the simplified illustration style. 9:16 vertical."

### Step 5: Generate Frame 4 — Brand Card (10-14s, hold 14-16s)
Prompt: "Clean Korean-style brand end card. Center a small circular crop of the person from the reference photo. Below it, generic production credits in Korean text — 'DESIGN BY' with a generic artist name, date, and 'MADE WITH LOVE' tagline. Clean white or soft pastel background, minimal design, elegant typography. 9:16 vertical. Face preserved exactly."

### Step 6: Compose Video
Assemble 4 frames into a 16s 9:16 video with cut transitions at 2s, 6s, 10s. Hold final brand card frame 2 seconds (14-16s). Use gentle dissolve or clean cut transitions.

### Step 7: QC

| Outcome | Condition | Action |
|---------|-----------|--------|
| PASS | All 4 frames clear, face preserved, design aesthetic matches | Deliver |
| REROLL | 1-2 frames low quality, face drift, style mismatch | Regenerate failed frames (max 1 retry each) |
| BLOCKED | Cannot preserve face, brand/IP violation, over budget | Halt, report to human |

Negative: no real idol/group/agency names, no real brand logos, no copyrighted fandom art copies, no face swap, no uncanny illustration, no mismatched style between frames.

## Delivery

- idol_design_reel.mp4 (16s, 9:16)
- frame_1_photocard.png
- frame_2_colorsystem.png
- frame_3_illustration.png
- frame_4_brandcard.png
- prompt_used.md
- qc_report.md

## Design Principles

1. Korean editorial aesthetic — clean grids, pastel palettes, soft typography
2. Each frame is a standalone designed page — not a video frame, a graphic design piece
3. Consistent visual language across all 4 frames — same color family, same typographic style
4. Face is the through-line — recognizable in photocard, color crop, illustration, and brand card
5. Process reel format — this is "showing your work", not a narrative video
