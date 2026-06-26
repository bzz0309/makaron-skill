---
name: creative-transition
description: >
  Turn 3-7 photos into a seamless zoom-through transition video. The agent
  finds color, texture, shape, light, and motion anchors between scenes,
  creates short macro bridge moments, then animates push-in / zoom-through /
  pull-out camera moves so one scene appears to transform into the next.
  创意无缝转场。
allowed-tools: generate_image analyze_image generate_animation Bash
metadata:
  makaron:
    icon: "🌀"
    color: "#6C3BAA"
    tags: [transition, creative, seamless, zoom, video, texture, viral]
    tipsEnabled: true
    tipsCount: 4
    faceProtection: none
    defaultAspectRatio: "9:16"
    modelPreference: [openai]
---

# Creative Transition — 创意无缝转场

Create a short seamless camera-transition video from user photos or from a
designed demo sequence. The signature move is:

`Scene A → push into an anchor → macro bridge → pull out into Scene B`

The user should feel that the camera dives into a real material, travels
through it, and emerges inside a new world. The result should look like a
premium viral transition preset, not a slideshow, not a morph collage, and not
a single-theme concept video.

This skill is intentionally platform-neutral. Use whatever capabilities the
host agent provides:

- Image understanding: vision model, image analysis tool, manual inspection.
- Image generation/editing: any still image model or local compositor.
- Video generation: image-to-video, text-to-video, animation model, or editor.
- Post-processing: FFmpeg, Pillow/OpenCV, NLE, motion graphics, or equivalent.

If the host is Makaron, `analyze_image`, `generate_image`, and
`generate_animation` can be used directly. Other agents should map those steps
to their own tools.

## Modes

### User Photo Mode

Use when the user provides 3-7 photos. Analyze the photos, choose the best
sequence, create transition anchors, generate/describe bridge moments, then
assemble the final video.

### Cover / Demo Mode

Use when creating a marketplace cover, template preview, or demo without user
photos. The goal is to demonstrate the motion mechanic quickly and elegantly.
Do not make the cover a product ad or a single-theme mood film.

Recommended premium demo chains:

**Silver Noir / reflection chain** (most stable for polished covers):

1. Fashion editorial portrait in a rain-night hotel lobby.
2. Push into a subtle eye reflection of vertical elevator seams or revolving
   door glass panels. Avoid crescent, ring-light, and moon-like shapes.
3. Empty hotel revolving door / curved metal and glass.
4. Rain trails on black car glass or another unbranded reflective surface.
5. Crystal glass rim / restaurant light reflections.
6. Empty theater spotlight or glass conservatory dome.
7. Polished floor or water reflection for a smooth unfinished ending.

**Material chain** (use only when the model handles anatomy reliably):

1. Fashion editorial gesture with a real material anchor such as fabric fold,
   button, seam, shadow opening, or subtle edge reflection. Avoid hand, wrist,
   sleeve, cuff, and jewelry close-ups when anatomy is unstable.
2. Satin / high-fashion corridor.
3. Glass, water, architecture, or bokeh scene.
4. Circular architectural light / dome / oculus.
5. Reflective final scene with a loopable push.

The opening should feel candid and editorial. A watch, jewelry, phone, logo, or
luxury object may appear only as an incidental anchor, not as a centered
product presentation.

Do not use artificial sparkle blobs, floating particles, isolated glowing dots,
neon garment edges, magic jewelry, or moon-like eye reflections as anchors.
They often look pasted onto clothing or skin. Anchors should be physically
motivated by real surface reflections, geometry, texture, or material structure.

## Core Concept — Anchor / Bridge / Reveal

Each transition has three parts:

```text
Scene A              Macro Bridge             Scene B
push in              zoom through             pull out / reveal
to anchor     ->     abstract texture    ->    from matching anchor
```

- Exit Anchor: the object, texture, color area, light spot, shape, or motion in
  Scene A that the camera dives into.
- Macro Bridge: a brief close-up texture or light moment that can be read as
  both the exit anchor and entry anchor.
- Entry Anchor: the matching element in Scene B that the camera pulls out from.

The bridge is not the star. The camera move is the star. Viewers should notice
the seamless transition before they notice the bridge frame.

## Inputs

Required for User Photo Mode:

- 3-7 photos.

Optional:

- Theme or mood: travel, fashion, food, seasons, daily life, premium, dreamy.
- Preferred order. If absent, optimize automatically.
- Target length or platform.
- Music or sound preference.

Best source images:

- Clear textures: water, sand, fabric, food, wood, metal, leaves, paper.
- Strong color fields: sky, wall, water, dress, light, road.
- Shapes: circles, doors, windows, arches, wheels, plates, sun, moon.
- Light anchors: bokeh, reflections, sun glints, window beams.
- Foreground objects that can plausibly receive a push-in camera move.

## Output Defaults

- Aspect ratio: 9:16 unless user asks otherwise.
- User Photo Mode length: 10-18 seconds.
- Cover / Demo Mode length: 8-10 seconds when showing several scene reveals;
  5-7 seconds only for a compact marketplace card.
- Frame rate: 24 or 30 fps.
- Style: photorealistic, cinematic, tactile, clean, no UI, no watermark.

## Workflow

### Step 1: Inspect Images

For each input image, identify:

- Dominant colors.
- Candidate objects for push-in anchors.
- Material and texture qualities.
- Geometry and repeated shapes.
- Light patterns and reflections.
- Foreground / midground / background.
- Mood, realism, and visual quality.
- Problems: text, logos, faces, clutter, low resolution, weak anchors.

Create an anchor list:

```text
Photo #N
- Object anchors:
- Texture anchors:
- Color anchors:
- Shape anchors:
- Light anchors:
- Motion implication:
- Risk notes:
```

### Step 2: Score Pairings

Score every possible pair of photos:

| Dimension | Weight | Meaning |
|---|---:|---|
| Color continuity | 25% | Shared or bridgeable palette |
| Texture continuity | 25% | Similar material rhythm or surface detail |
| Shape continuity | 20% | Circles, lines, arches, silhouettes, repeated forms |
| Light continuity | 15% | Similar highlights, bokeh, beams, reflections |
| Camera potential | 15% | A believable push-in and pull-out path |

For premium or cover work, also consider:

- Visual sophistication.
- Readability in a small marketplace card.
- Whether the transition mechanic is understandable in under 2 seconds.
- Whether the scene feels natural rather than like a product ad.

### Step 3: Choose Sequence

For 3-4 photos, use all photos in the best order.

For 5-7 photos, choose the best 4 unless the user explicitly wants all photos.
This avoids rushed transitions and keeps bridge quality high.

Default behavior: optimize and proceed. Do not stop for confirmation unless:

- The user explicitly asked to approve the order.
- The order changes the story in a sensitive or surprising way.
- Multiple options are equally strong and the choice is subjective.

Briefly explain the chosen sequence in the final response.

### Step 4: Design Transition Blueprints

For every adjacent pair:

```text
Transition #N: Scene A -> Scene B
- Exit anchor:
- Entry anchor:
- Match type: color / texture / shape / light / motion / scale
- Bridge concept:
- Camera move:
- Risk:
```

Good blueprint example:

```text
Coffee cup -> beach sunset
- Exit anchor: dark coffee swirl with amber highlights
- Entry anchor: wet sand ripples catching sunset light
- Match type: color + texture
- Bridge concept: warm brown macro swirl that reads as liquid and sand
- Camera move: push into coffee, fast zoom through swirl, pull out from sand
- Risk: avoid a digital spiral; keep it photographic and imperfect
```

## Bridge Generation

Use a bridge frame, bridge clip, or direct animation prompt depending on the
available tools.

If still images are used, one bridge image per transition is usually enough.
If the video model supports continuous transition prompts, describe the bridge
instead of generating a separate image.

Bridge prompt template:

```text
An extreme macro photographic texture that visually bridges two scenes.
It must read as both:
1. A close-up of {exit_anchor} from Scene A.
2. A close-up of {entry_anchor} from Scene B.

Palette: {shared_or_intermediate_colors}.
Texture: {material rhythm shared by both anchors}.
Composition: edge-to-edge macro texture, no horizon, no complete objects.
Motion feel: radial depth or directional flow for a fast zoom-through.
Style: real macro photography, tactile, organic imperfections, natural light.

Rules: no faces, no readable text, no logos, no UI, no split-screen, no collage,
no digital pattern look.
```

Bridge duration:

- User Photo Mode: 0.35-0.7 seconds.
- Cover / Demo Mode: 0.25-0.4 seconds.

If the bridge lasts too long, the illusion breaks. It should be felt more than
studied.

## Camera Motion

Every transition should follow this rhythm:

1. Establish Scene A briefly.
2. Push toward the exit anchor.
3. Accelerate into the anchor.
4. Zoom through the bridge.
5. Pull out from the entry anchor into Scene B.
6. Let Scene B breathe for a moment before the next push-in.

Scene motion prompts:

```text
Opening scene:
Camera starts in a natural establishing view, then glides toward {exit_anchor}.
The push-in accelerates in the final moment and dives into the anchor surface.

Bridge:
Rapid forward motion through {bridge_texture}. Crisp center, elegant edge
motion blur. No pause.

Middle scene:
Camera emerges from {entry_anchor}, pulls back smoothly to reveal the scene,
then drifts naturally before finding {next_exit_anchor}.

Final scene:
Camera pulls out to reveal the final scene and settles into a clean loopable
push, orbit, or drift.
```

## Cover / Demo Prompt Pattern

Use this when generating a cover video:

```text
Create a premium 8-10 second 9:16 cover video for a seamless transition skill.
The hero is the camera mechanic: push in, macro bridge, pull out to a new
scene. Show 4-5 recognizable premium scene reveals.

Opening: candid fashion/editorial human moment, natural movement, no product
presentation. A real reflection, geometry, or material detail becomes the first
anchor: eye reflection of vertical architecture, glass rim, metal seam, fabric
fold, button, shadow opening, or subtle surface reflection.
Bridge moments are fast, 0.25-0.35s each.
Scenes feel high-end: hotel lobby, revolving door, rain glass, wine glass,
theater spotlight, conservatory dome, polished floor or water reflection.
Photorealistic, cinematic, no text, no logos, no signage, no UI.
Do not center a product. Do not make it look like an ad for a watch, phone,
perfume, car, or bag. The object is only an anchor.
Avoid fake sparkle, glitter dots, magic particles, isolated glowing marks on
fabric or skin, neon lines on clothing, glowing jewelry, and crescent/moon/ring
shapes inside eyes.
```

## Verification

Before finalizing, inspect the video or key frames:

- Does the first second communicate the mechanic or at least feel premium?
- Are there at least 3 recognizable scene reveals?
- Do the transitions feel like camera movement, not hard cuts?
- Are bridge moments short and photographic?
- Are there unwanted readable words, logos, UI, watermarks, or signs?
- Does any object feel like an accidental product advertisement?
- Does any anchor look like a pasted-on sparkle, glitter sticker, floating
  particle, or physically impossible light blob?
- Do eye reflections read as plausible architecture or environment, rather
  than moon, crescent, ring light, or magic portal?
- If hands, wrists, cuffs, sleeves, or jewelry appear, are they anatomically
  correct and clearly incidental rather than product-focused?
- Are hands, faces, and bodies acceptable if people appear?
- Does the cover still work when viewed as a small vertical card?

If a problem appears:

- Product-ad framing: make the object incidental and move the camera anchor to
  a material fold, button, seam, shadow opening, edge reflection, glass rim,
  architectural reflection, or shape.
- Fake sparkle anchor: replace it with a real material structure such as a
  fabric crease, button, glass rim, metal edge, rain trail, architectural line,
  or natural reflection attached to a visible surface.
- Hand/cuff anatomy failure: avoid hands and cuffs entirely; use face-safe
  reflections, glass, fabric surfaces, architecture, or water instead.
- Moon-like eye reflection: replace the reflection with vertical/rectangular
  architectural geometry such as elevator seams, window panes, or revolving
  door panels.
- Long abstract tunnel: shorten bridge duration and increase scene reveal time.
- Text/logos/signage: replace the scene with no-sign architecture, abstract
  surfaces, nature, fabric, water, or bokeh.
- Weak continuity: choose a stronger color, shape, light, or texture anchor.

## Transition Types

| Type | Meaning | Examples |
|---|---|---|
| Color Match | Shared palette carries the cut | coffee -> sand, sky -> water |
| Texture Match | Similar surface rhythm | silk -> dunes, foam -> clouds |
| Shape Match | Similar forms | watch dial -> oculus, plate -> moon |
| Light Match | Similar highlights or bokeh | sun glint -> lamp, neon -> city |
| Motion Carry | Direction or energy continues | pouring -> waterfall |
| Scale Shift | Micro becomes macro | water droplet -> lake |
| Negative Space | Dark or empty area becomes portal | doorway -> tunnel |

Use variety. Do not make every transition the same type.

## Common Use Cases

1. Daily memory: coffee, street, book, window view.
2. Travel reel: beach, architecture, market, sunset.
3. Fashion / premium: eye reflection, revolving door, rain glass, wine glass,
   spotlight, dome, polished floor.
4. Food exploration: sauce swirl, noodles, table texture, street lights.
5. Seasons: flowers, green leaves, gold leaves, snow.

## Core Rules

- The skill is about seamless camera transitions, not just bridge frames.
- Never use a hard cut as the main transition.
- Never let bridge frames become long abstract tunnels.
- Never put recognizable faces, text, logos, or full objects inside bridge
  textures.
- Do not create random digital patterns; bridges should look like real macro
  photography.
- Do not make cover videos feel like product ads. Objects are anchors, not the
  subject.
- Do not use isolated sparkle blobs or floating light particles as transition
  anchors. Anchors must feel physically attached to the scene.
- Avoid unstable anatomy anchors in cover videos: hand, wrist, cuff, sleeve,
  and jewelry close-ups often become product-like or malformed. Prefer
  reflections, glass, metal, architecture, fabric surfaces, and water.
- Do not let eye reflections become moon, crescent, ring-light, or portal
  shapes unless the user explicitly asks for that surreal effect.
- Avoid readable signage and brand marks, especially in marketplace covers.
- Prefer 3-4 strong scene reveals over too many weak transitions.
- Explain the transition chain briefly when presenting the result.
