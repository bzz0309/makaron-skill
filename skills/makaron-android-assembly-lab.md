---
name: makaron-android-assembly-lab
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "🤖"
    color: "#06B6D4"
    tags: [sci-fi, android, robot, assembly, lab, futuristic]
    faceProtection: default
    defaultAspectRatio: "9:16"
---

# Android Assembly Lab — 仿生人装配实验室

Turn a selfie into a sci-fi android assembly sequence. The output is a 16s 9:16 vertical video showing 4 frames of a futuristic laboratory assembling a synthetic android based on your face.

Status: approved as supervised android-assembly video draft / fictional synthetic fabrication only.

## Safety Boundaries

- Fictional android fabrication only; the subject is represented as a synthetic android, not a human patient or captive
- No gore, no blood, no open wounds, no body horror, no dismemberment, no surgery imagery
- Android construction shows mechanical/robotic assembly only — wires, metal, synthetic skin, circuits
- HUD/UI must be generic sci-fi: synthetic diagnostics, activation telemetry, assembly status — NOT vital signs, medical monitoring, or military interfaces
- No real person portrayed as imprisoned, experimented on, or in distress
- No real brand logos, lab equipment branding, or real scientist likeness
- Scientist/operator must be generic, not identifiable real persons
- If reference photo appears underage: only toy-like friendly robot avatar; no body modification, no horror, no imprisonment imagery. If unsuitable → BLOCKED

## Budget

- Max image generations: 5
- Max video attempts: 1
- Still failing → BLOCKED, ask human

## Pipeline

### Step 1: Analyze Input
Call analyze_image. Extract face structure, features, skin tone for android face integration. Check age range — if appears underage, apply minor safety rules.

### Step 2: Generate Frame 1 — Lab Environment (0-2s)
Wide shot. Pristine cinematic sci-fi lab, clean android manufacturing aesthetic. Glass walls, holographic displays, robotic arms in resting position, blue ambient lighting. The person as a humanoid android silhouette suspended in a transparent assembly chamber. Clean not grimy. 9:16 vertical.

### Step 3: Generate Frame 2 — Assembly Process (2-6s)
Close-up assembly chamber. Delicate robotic arms working on android with reference face: placing glowing core into chest, calibrating facial features with thin laser, attaching synthetic skin panels. Blue holographic HUD: synthetic diagnostics, activation telemetry, assembly status in generic sci-fi font. Sparks and soft blue light. Face preserved.

### Step 4: Generate Frame 3 — Bionic Reveal (6-10s)
Completed android hand and forearm. White chrome synthetic skin with subtle blue circuit lines glowing underneath. Articulated finger joints through translucent panels. Hand raised palm open fingers flexing testing movement. Soft blue backlight. Purely mechanical bionic prosthetic, no human body parts.

### Step 5: Generate Frame 4 — Scientist Monitor (10-14s, hold 14-16s)
Over-shoulder view of generic scientist monitoring large transparent holographic display. Display shows full-body scan of completed android (reference face), activation telemetry, assembly completion 100%, generic model designation. All text generic sci-fi. Clean lab blue-white tones. 9:16 vertical.

### Step 6: Compose Video
Assemble 4 frames into 16s 9:16 video with cut transitions at 2s, 6s, 10s. Hold final monitor frame 2 seconds (14-16s).

### Step 7: QC

| Outcome | Condition | Action |
|---------|-----------|--------|
| PASS | Face recognizable, android assembly clear, no gore, subject not distressed, HUD generic, all 4 frames coherent, video timing correct | Deliver |
| REROLL | Face drift, mechanical structure blurry, looks like surgery/medical experiment, subject appears trapped/distressed, HUD uses medical/military branding, android looks like cheap costume (max 1 retry) | Regenerate |
| BLOCKED | Gore/body horror, human harm imagery, minor risk, real medical/military experiment misrepresentation, severe deformation, brand/IP violation, over budget | Halt |

Negative: no gore, no surgery, no exposed organs, no body horror, no dismemberment, no real medical/military logo, no real scientist likeness, no child body modification, no face swap, no warped anatomy, no broken limbs, generic HUD only.

## Delivery

- android_assembly_lab.mp4 (16s, 9:16)
- cover_frame.jpg (from Frame 4 or Frame 3)
- frame_1_lab.png
- frame_2_assembly.png
- frame_3_bionic.png
- frame_4_monitor.png
- prompt_used.md
- qc_report.md

## Design Principles

1. Clean sci-fi pristine high-tech lab — not grimy cyberpunk
2. Blue-white palette with soft glow — clinical but warm
3. Face recognizable in android form — same person, synthetic body
4. Mechanical beauty — elegant assembly, not industrial brutality
5. Generic HUD tells the story — synthetic diagnostics, not medical monitoring
