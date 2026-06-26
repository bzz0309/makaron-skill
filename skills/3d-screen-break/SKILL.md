---
name: naked-eye-3d-billboard-video
description: Create photorealistic naked-eye 3D/anamorphic LED billboard videos from an image or text subject. Use for outdoor 3D advertising screens, L-shaped corner LED billboards, foreign downtown commercial streets, product/animal/character/fashion breakout ads, and Makaron image-to-video prompts.
---

# Naked-Eye 3D Billboard Video

## Goal

Turn a user image or subject into a short photorealistic naked-eye 3D LED billboard video. The output should look like a real outdoor anamorphic advertisement on a large city building, with a clear screen-plane illusion: the subject starts inside the LED screen, then a hand, product, animal paw, vehicle front, splash, prop, or other hero element crosses beyond the physical LED frame into the real street space.

Default style: foreign downtown commercial district, New York/London/Tokyo-style street, English or abstract signage only, cinematic photorealistic outdoor advertising.

## Output Format

When asked to create a prompt or run a generation, produce:

- `Concept`: one sentence describing the hero subject and the breakout action.
- `Makaron prompt`: a direct prompt ready for Makaron. Use English by default for foreign street ads.
- `Negative prompt`: concise constraints.
- `Shot notes`: duration, aspect ratio, camera, timeline, and quality target.

When using Makaron CLI, choose any duration under 15 seconds. Prefer:

- 5 seconds for one simple breakout.
- 7-8 seconds for human gestures such as wave-to-finger-heart.
- 10-12 seconds for product, vehicle, or multi-beat action.

Default aspect ratio: `9:16`.

## Core Workflow

1. Identify the subject type:
   - Human/fashion/portrait
   - Animal/mascot
   - Product/food/drink
   - Vehicle/robot/device
   - Character/fantasy/game/IP-style subject
2. Choose screen architecture:
   - `corner-led`: massive L-shaped LED billboard wrapping a building corner; best default.
   - `wraparound-led`: rounded or curved commercial facade; use for luxury ads.
   - `flat-led`: giant facade LED screen; use only for simpler compositions.
3. Create the anamorphic illusion:
   - Subject begins inside a visible LED screen volume.
   - One active element crosses outside the LED frame.
   - The thick LED frame must partially occlude the crossing element.
   - Use at least three depth layers: real street foreground, out-of-screen element, and the rest of the subject still inside the LED screen.
4. Bind virtual subject to real street:
   - Contact shadows on the LED frame and screen surface.
   - Reflections on glass buildings and wet pavement.
   - Pedestrians, cars, traffic lights, crosswalks, storefronts, and road markings for scale.
5. Prevent common failures:
   - Do not make a flat poster or ordinary screen playback.
   - Do not add Chinese characters or Chinese signage for foreign-street outputs.
   - Do not create UI, captions, subtitles, watermarks, random text, malformed shop signs, or distorted buildings.

## Human Gesture Presets

For portrait, model, influencer, actor, fashion, and beauty images, choose a natural intentional gesture before writing the breakout. Avoid limp arms, dangling hands, random fingers, or awkward reaching.

Use gender-neutral gestures by default:

- `wave`: safest default. The subject raises one hand in a friendly greeting, palm facing the street audience. The hand and part of the forearm cross outside the LED frame while the wrist is partly hidden by the border.
- `finger-heart`: social-media friendly. One hand forms a small finger-heart close to camera outside the LED frame. Keep fingers clean and anatomically correct.
- `wave-to-finger-heart`: best default for 7-8 second human clips. The subject first waves naturally, then smoothly turns the same hand into a small finger-heart outside the LED frame for the peak hold.
- `subtle-wave`: most realistic. The hand crosses only slightly beyond the LED plane, stays near the billboard border, and never becomes a giant foreground close-up.
- `soft-point`: clean unisex gesture. The subject gently points toward the street audience or camera with a relaxed hand; the fingertip crosses slightly outside the screen but remains medium-sized.
- `two-hand-heart`: sweeter and more idol/fan-service. Both hands form a heart just beyond the screen plane, with wrists overlapping the LED border.
- `offer-object`: brand-friendly. The subject reaches out holding a product, flower, ticket, perfume bottle, drink, phone, or gift box; the object becomes the main breakout element.
- `touch-glass`: elegant and stable. The subject places a palm against or just beyond the LED plane; best when face/identity preservation matters.
- `point-to-audience`: energetic and unisex. The subject points toward viewers outside the screen; use for sports, games, concerts, events. Keep the hand medium-sized unless the user explicitly asks for an exaggerated close-up.

Mood- or gender-coded options:

- `blow-kiss`: beauty, celebrity, romance, feminine mood. The hand moves from lips outward with subtle petals or light trails.
- `adjust-sunglasses`: luxury, streetwear, watch, fragrance, car, masculine or androgynous mood. The hand and sunglasses edge cross the LED frame.

For all human gestures, keep the hand tasteful and proportionate: only slightly larger than normal perspective, near the LED border, never covering the face, never dominating the frame, and never pressed close to the camera.

## Human Action Sequences

For clips longer than 6 seconds, use a multi-beat sequence instead of one repeated hand gesture. Keep every hand movement subtle and close to the LED plane.

- `fashion-greeting-sequence`: best default for portrait/fashion. Beat 1: street and billboard reveal. Beat 2: subject turns from a slight side pose to face the street. Beat 3: subject tucks hair or lets hair move in wind. Beat 4: one hand lightly touches or grips the LED frame. Beat 5: subject gives a small wave or relaxed soft-point near the border. Beat 6: hair strands, fabric edge, and light reflections drift slightly outside the screen for the final 3D hold.
- `luxury-pose-sequence`: subject slowly shifts posture, lowers chin, adjusts collar or zipper, places one hand on the LED edge, then leans forward slightly. Use for fashion, beauty, fragrance, watches, and premium brands.
- `fan-greeting-sequence`: subject looks down toward pedestrians, smiles subtly, gives a short wave, then rests the hand naturally on the LED frame. Use for celebrity, idol, influencer, and friendly social ads.
- `cinematic-lookback-sequence`: subject starts turned away or in profile, looks back over shoulder, hair swings gently beyond the LED border, then settles into a direct gaze. Use when hand quality is risky or the user wants a more elegant result.

Avoid loops where the subject only repeats one hand pose. A good sequence changes head direction, shoulder angle, hair/fabric motion, and one small hand interaction with the LED border.

## Prompt Grammar

Use this structure:

```text
Subject identity + foreign city LED billboard architecture + inside-screen setup + intentional breakout action + screen-frame occlusion + real-world shadows/reflections + camera/timeline + quality + negative constraints.
```

## Makaron Prompt Template: Human Wave To Finger-Heart

Use this when the user provides a portrait/fashion image and wants a friendly, natural human action.

```text
Use <<<image_1>>> as the exact identity reference. Create an 8-second 9:16 photorealistic naked-eye 3D LED billboard video in a foreign downtown shopping district, New York/London/Tokyo-style. Preserve the subject's face, hairstyle, outfit, body proportions, and recognizable identity with a stable face.

A massive L-shaped corner LED billboard wraps around a premium glass-and-stone commercial building. Timeline: 0-2s reveal the real street corner, wet pavement, pedestrians, cars, traffic lights, storefronts with English or abstract signage, and the giant LED billboard with the subject inside it. 2-4s the subject leans forward naturally and raises one hand in a friendly wave near the LED border; the waving hand and wrist cross only slightly outside the lower LED frame, with the wrist partially hidden by the thick LED border. 4-7s the same hand gently points toward the street audience or camera, staying medium-sized and close to the billboard plane. Keep fingers clean, anatomically correct, and readable. 7-8s hold the subtle point/wave pose for a polished naked-eye 3D moment. Do not make the hand a giant close-up.

Keep the rest of the body visibly inside the LED screen volume, creating three distinct depth layers: real street foreground, subtly out-of-screen hand/wrist, and body still inside the billboard. Add strong LED-frame occlusion, contact shadows where the hand crosses the border, realistic shadows on the screen surface, glass reflections, wet pavement reflections, pedestrians looking up, cars, traffic lights, and storefronts with English or abstract signage only. Low-angle street-corner camera, subtle push-in, cinematic photorealistic outdoor advertising, high detail, tasteful depth illusion. No Chinese characters, no Chinese signage, no captions, no UI, no watermark, not a flat poster, no awkward dangling arm, no giant hand, no hand close-up, no distorted fingers, no extra hands.
```

## Makaron Prompt Template: General Human Billboard

```text
Use <<<image_1>>> as the exact identity reference. Create a 7-8 second 9:16 naked-eye 3D LED billboard video set in a foreign downtown commercial district, like a New York/London/Tokyo-style shopping block. Preserve the subject's face, hairstyle, outfit, and overall identity.

The subject appears inside a massive L-shaped corner LED billboard, then clearly but subtly breaks the screen plane with a natural intentional gesture: [choose subtle-wave / soft-point / wave / finger-heart / two-hand-heart / offer-object / touch-glass / blow-kiss / adjust-sunglasses / point-to-audience]. The active hand/forearm or object crosses only slightly outside the lower LED frame into the real street foreground, while the wrist, shoulder, or upper arm is partially hidden behind the thick LED border. Keep the hand medium-sized and close to the LED plane, not close to the camera. Keep the rest of the body visibly inside the screen volume to create a strong inside/outside depth split.

Add realistic LED-frame occlusion, contact shadows, glass reflections, pavement reflections, pedestrians, cars, storefronts, and traffic lights for scale. Low-angle street-corner camera, subtle push-in, cinematic photorealistic outdoor advertising. No Chinese characters, no Chinese signage, no captions, no UI, no watermark, not a flat poster, no awkward dangling arm, no giant hand, no hand close-up, no distorted fingers.
```

## Makaron Prompt Template: Varied Fashion Action

```text
Use <<<image_1>>> as the exact identity reference. Create a 10-second 9:16 photorealistic naked-eye 3D LED billboard video in a foreign downtown commercial district, New York/London/Tokyo-style. Preserve the subject's face, hairstyle, outfit, body proportions, and recognizable identity with a stable face. The subject appears inside a massive L-shaped corner LED billboard on a premium glass-and-stone building.

Use a varied fashion-greeting sequence: 0-2s reveal the street, wet pavement, pedestrians, cars, traffic lights, and the LED billboard. 2-4s the subject turns from a slight side pose toward the street audience, hair moving naturally. 4-6s the subject lightly tucks hair or adjusts the collar/zipper while staying inside the screen. 6-8s one hand lightly rests on the lower LED border and crosses only slightly outside the screen plane; wrist is partially hidden by the thick border. 8-10s the subject gives a small tasteful wave or relaxed soft-point near the border while hair strands and fabric edge drift subtly outside the LED frame.

Keep hands medium-sized and close to the screen, never close to camera. Keep three depth layers: real street foreground, subtle out-of-screen hair/fabric/hand near the LED border, and the body still inside the billboard. Add LED-frame occlusion, contact shadows, glass reflections, wet pavement reflections, and pedestrians looking up. No Chinese characters, no Chinese signage, no captions, no UI, no watermark, no giant hand, no hand close-up, no distorted fingers.
```

## Subject Recipes

### Animal Or Mascot

```text
A massive L-shaped naked-eye 3D LED billboard on a foreign downtown commercial building. Inside the LED screen, [animal/mascot] moves toward the street audience. One paw/head/tail crosses beyond the LED frame into the real street space, while the body remains partly inside the screen. The LED frame occludes part of the body, fur/skin reflects screen light, and the animal casts shadows on the frame and pavement. Pedestrians, cars, traffic lights, wet pavement, and glass reflections provide scale. 5-8 seconds, 9:16, cinematic photorealistic outdoor advertising. No Chinese signage, no captions, no UI, no watermark, not a flat poster.
```

### Product Burst

```text
A massive L-shaped naked-eye 3D LED billboard on a foreign downtown shopping block. Inside the screen, [product] rotates forward from a premium ad environment. The product crosses beyond the LED frame into the real street foreground, with [liquid / petals / ice / light particles / fabric / smoke] spilling out of the screen. Add frame occlusion, contact shadows, glass reflections, wet pavement reflections, pedestrians looking up, cars, and English or abstract storefront signage. 5-10 seconds, 9:16, cinematic photorealistic product advertising. Preserve the product identity; no random text, no Chinese signage, no watermark, not a flat poster.
```

### Vehicle Or Robot

```text
A huge naked-eye 3D LED billboard wraps around a glass commercial building in a foreign downtown block. Inside the LED screen, [vehicle/robot] powers up and moves toward the viewer. The front wheel, hood, hand, or mechanical part crosses beyond the LED frame into the real street foreground, while the rest remains inside the screen volume. Add strong LED-frame occlusion, realistic shadows, reflections on glass and wet pavement, traffic, pedestrians, and scale cues. 7-12 seconds, 9:16, cinematic photorealistic outdoor advertising. No Chinese characters, no UI, no watermark, no distorted architecture.
```

### Character Or Fantasy Hero

```text
A massive L-shaped naked-eye 3D LED billboard in a foreign downtown commercial district. Inside the screen, [character] appears in a deep cinematic environment, then flies or steps toward the viewer. One hand, weapon, cape, magical effect, or prop crosses beyond the LED frame into real street space. The body remains partly inside the screen, with the frame creating strong occlusion. Add particles, cloth motion, contact shadows, glass reflections, pedestrians, cars, and street-scale cues. 5-10 seconds, 9:16, cinematic photorealistic or requested style. No captions, no UI, no watermark, no Chinese signage unless requested.
```

## Negative Prompt Bank

Use or adapt:

```text
No flat poster, no ordinary big-screen playback, no indoor TV, no phone screen, no UI, no captions, no subtitles, no watermark, no Chinese characters, no Chinese signage, no unreadable shop signs, no random logos, no malformed buildings, no bent roads, no floating shadowless subject, no broken body geometry, no extra hands, no distorted fingers, no awkward dangling arm, no multiple competing heroes, no cartoon style unless requested.
```

## Quality Checklist

Before finalizing, make sure the prompt includes:

- A real physical LED billboard or building facade, not just an image on a screen.
- L-shaped or wraparound screen geometry for a strong anamorphic illusion.
- One clear hero action crossing the LED frame.
- The LED border partially occluding the crossing element.
- Three depth layers: real street, out-of-screen element, inside-screen body/subject.
- For human hand gestures, subtle scale: slightly outside the LED plane, medium-sized, near the border, not a giant foreground close-up.
- For human clips longer than 6 seconds, a multi-beat action sequence instead of one repeated hand pose.
- Shadows, reflections, pedestrians, vehicles, traffic lights, and storefronts for scale.
- Explicit no-Chinese-signage rules for foreign-street outputs.
- Negative constraints against flat posters, UI, watermarks, malformed buildings, awkward hands, and distorted fingers.
