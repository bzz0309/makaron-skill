---
name: ending-fairy
allowed-tools: [analyze_image, generate_image, generate_video]
modelPreference: [seedance]
defaultAspectRatio: "9:16"
---

# Ending Fairy

Upload a portrait, become a K-pop music show ending fairy — finishing a stage performance under purple-blue bokeh, catching breath, soft smile, small heart gesture, hold the gaze. 8 seconds.

## Pipeline

Input Photo → Cover Image (image model first) + Broadcast UI → Video Rendering (Seedance 8s) → QC → Delivery

**Core rule: UI gets done in the cover first. Video only handles motion.** Do not rely on Seedance to generate stable text/UI.

## Step 1: Cover Image with Broadcast UI (image model first)

makaron-cli chat --project auto --image <user_photo> --json -b "<prompt>"

### Prompt Template

Transform this person into a K-pop idol on a music show ending fairy stage. Keep their face and natural look 100% recognizable — do NOT add hats, caps, sunglasses, or glasses unless the original photo already has them. Retain their hair color, hairstyle, facial features, and personal style. Dark stage with purple-blue bokeh background. The subject is centered upper-middle / slightly right, wearing sparkly stage outfit with chain accessories, IEM + headset mic. Leave clean lower-left safe space for large broadcast title overlay.

Add high-quality Korean music show broadcast UI:
- Top-right: large hot-pink rounded M badge with bold white M.
- Lower-left: rounded capsule label FOCUS CAM, huge bold white Korean stage name {member_name}, short hot-pink underline, bold white Korean song title {song_title}.
- Bottom-right: black semi-transparent rounded rectangle with white {timecode}.
- Clean safe margins, UI not cropped, crisp typography, professional K-pop TV thumbnail style.

### Variables

| Variable | Description | Default |
|---|---|---|
| `{member_name}` | Korean idol stage name | Auto-generate Korean stage name matching the subject (e.g. `이수아`) |
| `{song_title}` | Korean song title | Auto-generate Korean song title (e.g. `첫사랑`) |
| `{timecode}` | Video timecode | Random 3:00–5:00 (e.g. `4:15`) |

If user specifies values, use user-specified values. Otherwise auto-generate.

### Forbidden

- Do NOT add hats, caps, sunglasses, or glasses not in original
- Do NOT change hair color or style
- Do NOT block or obscure the face
- Do NOT force a uniform look
- Do NOT render readable text signs other than the specified UI
- Do NOT let the subject overlap with the broadcast UI area

## Step 2: Video Rendering

makaron-cli video create --model seedance --image <cover_cdn_url> --script "<script>" --duration 8 --json

### Script Template

8-second ENDING FAIRY fancam video (default 9:16 vertical; 16:9 optional for thumbnail/cover). Dark stage with purple-blue bokeh. Use the approved cover image as the source frame. Preserve the broadcast UI as much as possible. Do NOT redesign or replace any UI text/logo. Only animate the idol's ending-fairy motion:

The idol has just finished performing: subtle shoulder rise and fall, continuous breathing visible in chest and shoulders, direct eye contact with camera — never look down (2s). Breathing continues as she slowly smiles, finding the camera (2s). Makes a small gentle finger heart or cheek heart (2s). Holds the gaze with warm smile as breathing slows (2s).

Slight handheld micro push-in. Real K-pop music show ending fairy moment — post-performance exhaustion, not confident stage pose. No text changes, no new UI, no slow motion.

## Step 3: QC Checklist

| QC Item | Pass Criteria |
|---|---|
| Face Identity | Matches input photo, no deformation |
| Hair | Matches original — color and style unchanged |
| No Forced Accessories | No added hats, caps, sunglasses, glasses |
| Scene Completeness | Dark stage + purple-blue bokeh + stage outfit |
| Motion Flow | Breathing → smile → small heart → hold gaze |
| Ending Fairy Feel | Post-performance exhaustion, not "confident pose" |
| Cover UI Preserved | M badge, FOCUS CAM, name, song, timecode intact |
| Quality | No tears, no limb distortion |
| Eye Contact | Maintains camera eye contact throughout, no looking down |
| Foreground Focus | Subject is clear main focus, face sharp |
| Brand Safety | No real brand logos |

## Failure Modes

| Symptom | Root Cause | Fix |
|---|---|---|
| UI eaten by Seedance | Video model strips text | Generate transparent PNG UI overlay, ffmpeg direct overlay (no chroma-key) |
| Looks like "award acceptance" not ending fairy | Script describes confident pose | Use "post-performance exhaustion, breathing, small heart" language |
| Added hats/sunglasses not in original | Prompt hardcodes accessories | Emphasize "do NOT add" |
| Face deformed | Seedance anatomy drift | Regenerate cover image, increase face preservation |
| Stiff motion | Poor time distribution | Adjust segment timing |
| Looking down | Script says "catch breath looking down" | Remove "look down", keep "direct eye contact throughout" |

## UI Overlay Fallback

When Seedance strips the broadcast UI, create a transparent PNG overlay and composite:

1. Generate UI overlay as transparent PNG using HTML/CSS, SVG, Remotion, or Python PIL
2. Composite directly (no green screen needed):
```bash
ffmpeg -i video.mp4 -i ui-overlay.png \
  -filter_complex "[0:v][1:v]overlay=0:0" \
  -c:v libx264 -crf 18 -c:a copy output.mp4
```

Reusable UI prompt fragment:
```
Add high-quality Korean music show broadcast UI. Top-right: large hot-pink rounded/slanted M badge with bold white M. Lower-left: rounded capsule label FOCUS CAM, huge bold white Korean stage name, short hot-pink underline, bold white Korean song title. Bottom-right: black semi-transparent rounded rectangle with white timecode. Clean safe margins, UI not cropped, crisp typography, professional K-pop TV thumbnail style.
```
