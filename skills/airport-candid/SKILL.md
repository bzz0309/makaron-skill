---
name: airport-arrival
allowed-tools: [analyze_image, generate_image, generate_video]
modelPreference: [seedance]
defaultAspectRatio: "4:5"
---

# Airport Arrival

Upload a portrait, walk through the airport arrival gate — paparazzi flash, security escort, fans watching. 8 seconds to become an airport arrival star.

## Pipeline

```
Input Photo → Scene Image (Airport Arrival) → Video Rendering (Seedance 8s) → QC → Delivery
```

## Step 1: Scene Image

```bash
makaron-cli chat --project auto --image <user_photo> --json -b "<prompt>"
```

### Prompt Template

```
Transform this person into a celebrity / idol airport arrival candid paparazzi scene. Keep their face and natural look 100% recognizable — do NOT add hats, caps, sunglasses, or glasses unless the original photo already has them. Retain their hair color, hairstyle, facial features, and personal style. Add light airport street-fashion styling only if it does not block the face or hair. Scene: walking through a bright modern airport terminal with large glass windows, queue barriers, metal beams, security guard nearby, paparazzi cameras and fans blurred in the background. The subject must remain the clear foreground focus, face sharp and unobstructed, background people blurred. Natural airport daylight, raw unfiltered colors, handheld fan-cam feeling, slightly tilted candid framing, full-body documentary shot, 4:5 vertical. Hyper-realistic, no text overlays, no real brand logos, no airline logos. Do NOT duplicate the subject's face onto background people.
```

### Forbidden

- ❌ Do NOT add hats, caps, sunglasses, or glasses not in the original photo
- ❌ Do NOT change hair color or hairstyle
- ❌ Do NOT block or obscure the face
- ❌ Do NOT force a uniform look — preserve each person's individual style
- ❌ Do NOT include real airline logos, airport brand logos, or luxury brand trademarks
- ❌ Do NOT render readable text signs or flight info screens
- ❌ Do NOT duplicate the subject's face onto background people or crowd

## Step 2: Video Rendering

```bash
makaron-cli video create --model seedance --image <cdn_url> --script "<script>" --duration 8 --json
```

### Script Template

```
8-second airport arrival candid paparazzi fancam video (4:5 vertical). Handheld shaky documentary style. The subject walks out of the airport arrival gate with a calm confident expression (2s). Camera flash pops — they naturally raise a hand to lightly block the flash or tuck hair behind ear (2s). Continue walking forward as paparazzi flashes continue from all sides (2s). Turn head to look back at camera with a subtle gentle smile (2s). Security guard walking beside them, blurred fans and media in background. The subject must remain the clear foreground focus, face sharp, background people blurred. Natural airport daylight, raw unfiltered colors. No slow motion, real airport walk pace. No text, no UI.
```

## Step 3: QC Checklist

| QC Item | Pass Criteria |
|---|---|
| Face Identity | Matches input photo, no deformation |
| Hair | Matches original — color and style unchanged |
| No Forced Accessories | No added hats, caps, sunglasses, glasses |
| Scene Completeness | Airport + security + paparazzi + fans |
| Motion Flow | Walk → hand block flash / tuck hair → turn → gentle smile |
| Quality | 4:5 vertical, no tears, no limb distortion |
| Foreground Focus | Subject is clear main focus, face sharp, no crowd blocking face |
| Brand Safety | No real airline/airport/luxury brand logos |

## Variable Pool

| Variable | Description | Source |
|---|---|---|
| Portrait | Input photo | User upload |
| Styling | Original outfit + light airport fashion accents | Auto-detected |
| Accessories | Keep only what's in the original | Auto-detected |
| Motion | Walk → hand-up flash block / hair tuck → look back smile | Fixed |

## Failure Modes

| Symptom | Root Cause | Fix |
|---|---|---|
| Added hats/sunglasses not in original | Prompt hardcodes accessories | Remove accessory descriptions, emphasize "do NOT add" |
| Face deformed | Seedance anatomy drift | Regenerate scene image, increase "Keep face 100%" weight |
| Stiff motion | Poor time distribution across segments | Adjust segment timing |
| Incomplete airport scene | Missing prompt elements | Add glass windows / barriers / security / paparazzi details |
| Real brand logos appear | Airport/airline branding in scene | Add "no real brand logos" to prompt, use generic terminal |
| Subject face duplicated on crowd | AI copies face to background people | Add "Do NOT duplicate the subject's face onto background people" |
