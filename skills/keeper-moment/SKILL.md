---
name: diving-save-keeper
description: Turn any portrait into a cinematic goalkeeper diving save video. Generates character design, storyboard, and video prompt with striker shot + full-stretch save + successful deflection. Platform-neutral output for Seedance, Kling, Gemini, or any video agent.
allowed-tools: analyze_image generate_image generate_video generate_music
metadata:
  makaron:
    icon: "football"
    color: "#F59E0B"
    tags: [video, sports, football, soccer, goalkeeper, save, world-cup, template]
    tipsEnabled: true
    tipsCount: 4
    modelPreference: [seedance, kling, gemini]
    defaultAspectRatio: "9:16"
    defaultCoverStyle: sporty|dramatic|athletic
---

# Diving Save Keeper

Turn any portrait or sports reference into a cinematic goalkeeper diving save video. The output is platform-neutral and works with Seedance, Kling, Gemini, Runway, Sora, or any video generation pipeline.

## Workflow

1. **Analyze** the uploaded reference image (face, hair, build, clothing color).
2. **Generate character image** — transform the person into a goalkeeper in professional kit.
3. **Generate storyboard** — key frames for each beat.
4. **Output video prompt** — ready to submit to a video model.
5. **Generate video** — submit and return the result.

## Core Motion — 6 Beats

| Beat | Name | Action |
|------|------|--------|
| 0 | `striker_shot` | A striker sprints in and strikes the ball with explosive power |
| 1 | `setup` | The goalkeeper stands on the goal line, knees bent, arms ready |
| 2 | `ball_incoming` | The ball flies toward a corner of the goal at high speed |
| 3 | `dive_launch` | The goalkeeper pushes off the turf and dives sideways at full stretch |
| 4 | `hero_contact` | Slow motion — body horizontal in air, glove fingertips touch the ball |
| 5 | `save_result` | Ball deflected away, goalkeeper lands and rolls, net stays perfectly still |

## Spatial Rules (Critical)

These rules prevent direction conflicts in generated video:

1. **Side-on medium shot for opening**: Frame both striker (left) and goalkeeper (right) facing each other. This establishes clear spatial relationships.
2. **Consistent ball direction**: Ball always travels from striker side toward goal side (left → right if striker is on left).
3. **Dive matches ball**: Goalkeeper dives in the same direction the ball is heading.
4. **Striker must move**: The striker sprints, plants foot, swings leg, and follows through. Never static.
5. **Net never moves**: The save is always successful. Ball is deflected away/over. Net stays still.

## Reference Image Strategy

When using image-to-video (i2v) models like Seedance:

- **Only use goalkeeper images as reference** (character image + hero_contact frame).
- **Never use the striker frame as a reference image** — the model will treat it as the protagonist and copy it into the opening, causing identity conflicts.
- Describe the striker purely in text — the model generates a generic striker that doesn't need face consistency.
- The `hero_contact` frame (Beat 4) is the best single reference for i2v because it contains the key action pose.

## Universal Video Prompt Template

```text
Use the uploaded image as the goalkeeper reference. Preserve the person's face, hairstyle, body proportions, and overall attitude. Adapt the outfit into professional goalkeeper kit with gloves.

Create a {duration}-second 9:16 realistic sports commercial video in a night stadium with floodlights and World Cup atmosphere.

OPENING (0-3s): Side-on medium shot. On the right, the goalkeeper stands in front of his goal in ready position. From the left, a striker in a contrasting jersey SPRINTS toward the ball, plants his foot, SWINGS his leg with full power, and STRIKES the ball. His body follows through with momentum. The ball rockets from left to right toward the top-right corner of the goal.

SAVE (3-{duration-1}s): Camera moves closer to the goal. The goalkeeper launches himself to his right in a full-stretch dive. SLOW MOTION: body horizontal in air, green glove fingertips reach the ball and push it over the crossbar. Ball deflected up and away. Net stays perfectly still.

AFTERMATH ({duration-1}-{duration}s): Goalkeeper crashes onto turf, rolls, looks up triumphantly. Save complete. Net untouched, ball cleared.

SPATIAL RULE: Ball travels LEFT to RIGHT. Goalkeeper dives RIGHT. Striker MOVES (sprint, plant, swing, strike). Net NEVER moves. Save is SUCCESSFUL.

Avoid: broken body shapes, missing gloves, ball passing through hand, net moving like a goal, extra limbs, distorted face, real logos, text, UI, watermark.
```

## Duration Recommendations

| Model | Recommended | Notes |
|-------|-------------|-------|
| Seedance | 8s | Best for real faces, supports 4-15s |
| Kling | 8-10s | General purpose, supports 5-15s |
| Gemini | 5-8s | Good quality, shorter output |

## Character Image Prompt

When generating the goalkeeper character from a portrait:

```text
Transform this person into a professional football goalkeeper. Keep exact face, hairstyle, body proportions, and overall attitude unchanged. Dress in full professional goalkeeper kit: long-sleeve jersey (adapt their clothing's main color), shorts, knee-high socks, professional goalkeeper gloves in neon green/yellow. Standing confidently on the goal line of a professional football stadium at night, arms slightly spread in ready position. Full-size goal with white net behind. Vivid green turf. Bright floodlights creating rim lighting. 9:16 vertical, cinematic sports photography.
```

## Quality Checks

- [ ] Goalkeeper face matches the reference image
- [ ] Goalkeeper wears gloves throughout
- [ ] Striker has dynamic motion (not static)
- [ ] Ball direction is consistent (striker → goal)
- [ ] Dive direction matches ball trajectory
- [ ] Glove makes contact with ball
- [ ] Ball is deflected AWAY (save successful)
- [ ] Net stays completely still (no goal ripple)
- [ ] No real logos, text overlays, or watermarks
