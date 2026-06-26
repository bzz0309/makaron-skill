---
name: makaron-hero-transformation
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "⚡"
    color: "#7C3AED"
    tags: [hero, transformation, cyberpunk, energy, reveal]
    faceProtection: default
    defaultAspectRatio: "9:16"
---

# Hero Transformation — 英雄觉醒变身

Turn a selfie into a cinematic hero transformation sequence. 12s 9:16 vertical video through 5 frames: street scene → energy burst → transformation → hero reveal → final pose.

Status: draft for supervised generation.

## Core Concept

Selfie → Street Scene → Energy Burst → Transformation → Hero Reveal → Final Pose. 12s 9:16 vertical. Face preserved throughout.

## Safety

Fictional character transformation only. Person empowered, not harmed. No gore, no body horror. No real brand logos. Face recognizable throughout.

## Budget

Max image 5 (5 frames). Max video 1. BLOCKED on failure.

## Pipeline

Frame 1 (0-2s): Person in neon cyberpunk street, casual outfit, face clear.
Frame 2 (2-5s): Energy burst, blue-purple particles erupting, eyes glowing.
Frame 3 (5-8s): Peak morphing, energy cocoon, armor phasing on.
Frame 4 (8-11s): Hero reveal, cyberpunk armor with glow accents, confident stance.
Frame 5 (11-12s): Final power pose against neon skyline.

## QC

PASS: face preserved, transformation arc complete, cohesive aesthetic.
REROLL: face drift, energy artifacts, armor looks like cosplay (max 1 retry).
BLOCKED: body horror, gore, brand/IP, over budget.

## Negative

no gore, no body horror, no real brands, no face swap, no violence.

## Delivery

hero_transformation.mp4 (12s, 9:16), cover_frame.jpg, frame_1-5.png, prompt_used.md, qc_report.md.
