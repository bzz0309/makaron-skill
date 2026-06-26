---
name: curved-free-kick
description: Turn a portrait or sports reference into an 8-second cinematic curved free kick goal video. Platform-neutral — works with any AI video agent (Seedance, Kling, Runway, Gemini, Sora, etc.).
allowed-tools: analyze_image generate_image generate_video generate_music
metadata:
  makaron:
    icon: "football"
    color: "#2563EB"
    tags: [video, sports, football, soccer, free-kick, world-cup, template]
    tipsEnabled: true
    tipsCount: 4
    modelPreference: [seedance, kling, gemini]
    defaultAspectRatio: "9:16"
---

# Curved Free Kick

Create a cinematic AI video of a bending free kick goal from a single portrait or sports reference image. The output is a vertical (9:16) sports-commercial-style clip showing the full sequence: setup, run-up, curving strike, and goal.

This skill is platform-neutral — it outputs prompts usable by Seedance, Kling, Runway, Gemini, Sora, or any AI video generation pipeline.

## Core Motion

The action must be readable in five beats:

1. `setup_beat` — the protagonist stands behind a stationary ball, calm breath, eyes on goal.
2. `ball_cue` — the ball sits still on the turf; a defensive wall and goalkeeper are clearly visible.
3. `action_ramp` — three-to-five-step run-up; support foot plants firmly beside the ball.
4. `hero_contact` — slow-motion moment: inside of the foot wraps around the ball; grass debris flies; the ball launches with visible spin on a curved trajectory.
5. `result_beat` — the ball bends around the wall into the top corner; goalkeeper dives too late; crowd erupts.

## Universal Prompt Template

```text
Use the uploaded image as the protagonist reference. Preserve the person's face, hairstyle, body proportions, and overall attitude throughout. Do not swap or morph the protagonist.

Create an 8-second 9:16 vertical realistic sports commercial video set in a large professional football stadium at night. Strong white floodlights illuminate real grass turf. The atmosphere is tense — a World Cup final moment.

IMPORTANT — Jersey color contrast: The protagonist wears a solid dark blue jersey and dark shorts. The defensive wall (4-5 players) and the goalkeeper ALL wear solid white jerseys and white shorts. All jerseys are plain solid colors with NO text, numbers, logos, or badges of any kind.

Action: curved free kick (bending free kick goal).

Shot 1 (1.5s): Wide broadcast angle. The protagonist in dark blue stands 5 meters behind a stationary football, breathing calmly, eyes locked on goal. Ahead at 20 meters, 4 white-jersey players form the wall. A white-jersey goalkeeper stands slightly right of center in the goal. Crowd lights shimmer in the background.

Shot 2 (1s): Low ground-level close-up. The football sits still on the grass, blades of grass in sharp focus. The white wall is visible as a blurred backdrop.

Shot 3 (1.5s): Side-tracking medium shot. The protagonist begins a three-step run-up, strides powerful and controlled. The support foot plants firmly to the left of the ball, body leaning right to load power.

Shot 4 (2.5s): SLOW MOTION — this is the hero shot. The inside of the foot wraps around the outside of the ball. Grass debris scatters. The ball lifts off and curves RIGHT first, visibly arcing AROUND the right end of the white wall, then bends sharply LEFT toward the top-left corner of the goal. The camera tracks the ball along its curved flight path. The arc must be clearly visible — NOT a straight line.

Shot 5 (1.5s): Goal close-up. The ball curls into the top-left corner. The goalkeeper in white dives right but is beaten completely. The net bulges violently. Cut to wide: crowd erupts, floodlights flare.

Camera: broadcast angle → ground close-up → side tracking → ball-follow arc → goal close-up. One protagonist, one ball, one wall, one clear goal direction throughout.

Style: High-definition realistic sports commercial. Night stadium with cool white floodlights. Cinematic motion camera. Vertical 9:16.

AVOID: straight ball path (MUST curve), same-color jerseys on wall and protagonist, any text or numbers or logos on jerseys, wrong goal scale, ball teleporting, extra limbs, face morphing or drifting, real brand logos, subtitles, UI overlays, watermarks.
```

## Stabilization Notes

These lessons come from multi-round testing and improve first-attempt success rate:

- **Use 8 seconds minimum.** At 5 seconds the curve has no time to develop — the ball appears to fly straight. 8 seconds gives Shot 4 enough room for the slow-motion arc.
- **Explicitly contrast jersey colors.** If not specified, models default to similar dark colors for everyone, making it impossible to distinguish attacker from defenders. Always state: protagonist = dark color, wall + goalkeeper = different light color.
- **State the curve direction explicitly.** "Bends around the wall" is too vague. Specify: "curves RIGHT first, then bends LEFT into the top-left corner" (or vice versa). Without a clear direction, models produce straight shots.
- **No text on jerseys.** AI video models produce garbled characters on clothing. Pre-empt this by requiring "plain solid color jerseys with no text, numbers, or logos."
- **Keep the wall small.** 4 players maximum. More players create visual chaos and confuse the model about where the ball should go.
- **Slow-motion in Shot 4 sells the curve.** Without the slo-mo cue, the ball-flight happens too fast to read as a curve.

## Quality Checks

- [ ] The ball starts completely stationary in Shot 1-2.
- [ ] The wall and goalkeeper are clearly a DIFFERENT color from the protagonist.
- [ ] The support foot visibly lands beside the ball before contact.
- [ ] The ball path is a visible ARC, not a straight line.
- [ ] No readable text or garbled characters appear on any jersey.
- [ ] The goalkeeper dives in the wrong direction (confirming the bend).
- [ ] One consistent protagonist face throughout — no morphing.
