---
name: time-freeze-snap-video
description: Create reusable cinematic video prompts and generation workflows for finger-snap time-freeze effects where a subject stops the surrounding world, holds a visible paused tableau, then optionally snaps again to restore motion. Use when the user asks for time stop, time freeze, paused world, frozen crowd, snap to freeze, double-snap restore, still-world illusion, or a reusable AI video template for tools such as Seedance, Kling, Runway, Pika, Luma, Sora-style models, or image/video-to-video systems.
---

# Time Freeze Snap Video

## Core Principle

Favor a simple, readable timeline over heavy VFX language. The most reliable result is:

1. Normal visible motion before the first snap.
2. One clear first snap.
3. A paused-video-frame freeze.
4. One clear second snap if restoring time.
5. Motion resumes only after the second snap.

Do not over-constrain the prompt after a good result. If a version works, modify only the failing detail. Excessive negative prompts can make models invent outlines, statue effects, early freezing, fog, or other artifacts.

## Default Timing

For a readable social-video template, use 10-12 seconds in 9:16:

- **0.0-4.0s Moving world**: background pedestrians walk visibly for multiple steps, vehicle or scooter headlights move, signs flicker, paper scraps or dust move, hair/fabric moves subtly.
- **4.0-5.0s First snap**: subject raises one hand near chest height; thumb and middle finger press together; one readable snap.
- **5.0-8.5s Frozen tableau**: all non-subject motion stops like a paused video frame. People stay normal and human, only motionless.
- **8.5-9.8s Second snap**: while the world is still frozen, subject performs a second readable snap.
- **9.8-12.0s Restore**: background motion resumes from frozen poses.

For shorter clips, compress proportionally but keep at least 2 seconds of visible motion before the first snap and at least 2 seconds of frozen tableau.

## Production Prompt

Use this as the default image-to-video or text-to-video prompt, adapting subject and setting:

```text
Use the reference image as the exact subject identity, face, outfit, hairstyle, expression, lighting direction, and environment layout. Create a 12-second 9:16 premium cinematic live-action VFX video about pure time-stop power. Keep everyone photorealistic and human. No character outline, no black outline, no white outline, no glowing edge, no halo, no cel shading, no anime, no illustration.

0.0-4.0 seconds, normal moving world: use a readable medium shot so the subject and background are both visible. Two or three background pedestrians walk for multiple steps with clear legs and arm swings. A vehicle or scooter headlight moves through the background. Paper scraps or dust drift. Sign light flickers. Hair and clothing move subtly. The subject remains calm and looks into camera. Nothing is frozen before the first snap.

4.0-5.0 seconds, first visible snap freezes time: the subject raises one hand near chest height. Show thumb and middle finger press together, then one clean readable finger snap. At the snap, use only a subtle transparent light-bend ripple, not a glowing ring.

5.0-8.5 seconds, paused-world tableau: all surrounding motion stops completely like a paused video frame. Pedestrians remain normal real humans frozen mid-step, with normal skin, hair, clothing color, and fabric texture. No walking, drifting, blinking, morphing, or body shifting. Vehicle/headlight motion, paper scraps, dust, sign flicker, hair, and clothing all stop. The subject alone may breathe subtly. The camera may slowly push or orbit to prove the world is paused.

8.5-9.8 seconds, second visible snap restores time: while the world is still frozen, the subject clearly performs a second finger snap near chest height. Do not resume any background motion until this second snap is finished.

9.8-12.0 seconds, time resumes: pedestrians continue walking from their exact frozen poses, headlight motion continues, paper scraps and dust move again, sign flicker resumes, hair and clothing move naturally. End on a calm hero frame.

No rain, airborne water droplets, steam, fog, mist, vapor, smoke, text, watermark, UI, subtitles, extra fingers, missing fingers, deformed hands, melted face, identity change, duplicate person, explosion, disintegration, random magic symbols, or money bills.
```

## Reliability Rules

- Use "paused video frame" instead of "statue", "sculpture", "stone", or "mannequin". Those words can cause material transformation.
- Use "subtle transparent light-bend ripple" instead of "glowing shockwave", "cyan energy", "ring", or "aura". Those words can create outlines or halos.
- Use dry city motion, pedestrians, headlights, paper, dust, signs, hair, fabric, or foreground objects as freeze proof when the user wants this distinct from rain-control effects.
- Avoid rain, droplets, steam, mist, fog, vapor, and wet-weather language unless the user explicitly wants a rain-control or water-control variant.
- Preserve a working composition. If a result is close, keep its timing and shot language and only patch the failed detail.
- For the second snap, avoid "subtle finger flick" unless the user wants understated motion; models may skip it. Prefer "second clearly visible finger snap".

## Troubleshooting

- **World freezes too early**: emphasize "nothing is frozen before the first snap" and add several concrete pre-snap motions: pedestrians walk for multiple steps, headlight moves, paper tumbles.
- **No second snap**: make the restore segment explicit: "time resumes only after the second visible snap; no background motion before the second snap finishes."
- **Pedestrians drift during freeze**: say "paused video frame, no walking, no drifting, no blinking, no morphing, no body shifting."
- **People become statues**: remove statue/sculpture/mannequin language and add "normal real humans; normal skin, hair, clothing, color, and fabric texture."
- **Outlines or halos appear**: remove energy/ring/aura words and add "no black outline, no white outline, no glowing edge, no halo, no cyan glow."
- **The shot is hard to read**: use a wider medium shot, 10-12 seconds, and large readable pedestrians rather than tiny distant figures.
