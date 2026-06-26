# FPV Drone Flythrough Video

## Skill goal

Turn one scene image into a vertical FPV drone flythrough shot. The result should feel like a small drone or first-person camera flying through the environment, passing foreground objects, following a readable route, covering meaningful distance, and revealing a destination.

This skill is not tied to one fixed scene type. It can work for coastal resorts, villas, cities, museums, theme parks, event venues, interiors, retail spaces, product worlds, and other environments with a clear travel path.

For marketplace demos, prefer a city-scale or destination-scale route over a single small scene when possible. The opening can feel like a fast FPV tour across different places in one city: skyline, bridge, street canyon, plaza, rooftop, station, museum, hotel lobby, or event venue.

This is not a tutorial video. Do not add presenter footage, social media screenshots, voiceover, subtitles, UI, or explanation cards. The output is the cinematic flythrough itself.

## Output

- Format: 9:16 vertical video
- Duration: 10 seconds recommended; 5-10 seconds supported
- Frame rate: 24-30 fps
- Motion: continuous forward FPV flight
- Look: cinematic, immersive, smooth but energetic
- Audio: optional ambient whoosh only if requested
- No text, no captions, no UI, no watermark

## User inputs

1. `scene_image`: required. A single image of the environment to fly through.
2. `scene_prompt`: optional. Describe the scene if the image is abstract or incomplete.
3. `route`: optional. Describe the flight route. Default: start wide, fly forward in an S-curve, pass close to foreground objects, reveal the main landmark.
4. `speed`: optional. `slow`, `medium`, or `fast`. Default: `medium`.
5. `style`: optional. Default: cinematic realistic FPV.
6. `destination`: optional. The final subject to reveal, such as a castle gate, tower, skyline, stage, room, product, or portal.
7. `people`: optional. Add small, natural lifestyle figures only when the scene benefits from scale and realism.
8. `route_length`: optional. `short`, `medium`, or `long`. Default: `long` for marketplace demos.
9. `route_mode`: optional. `single-scene`, `long-route`, or `city-waypoints`. Default: `long-route`.

## Core behavior

The model should preserve the source image as the world layout. It can add depth, parallax, atmosphere, and realistic motion, but should not replace the scene with an unrelated environment.

## Route guide image rule

A route guide image with a red line or arrows may be used internally to design the camera motion, but it must not be submitted as the final video source image.

Workflow:

1. Use the red-line route image only to decide and write the flight path.
2. Create or select a clean source image with no route line, arrows, markers, annotations, text, UI, or overlays.
3. Submit the clean source image to the video model.
4. Describe the same route in words, such as "follow an invisible S-curve through the canyon, pass close to the bridge, then rise toward the villa terrace."
5. Add a negative instruction: no red line, no arrows, no drawn path, no graphic overlays.

Never let route arrows or path lines appear in the final generated video. They are production notes, not visual content.

The camera should:

- Start from a slightly wide view of the scene.
- Move forward continuously, like a drone.
- Follow a clear path through the image.
- Prefer a pulled-back starting point when possible, so the route covers distance before the final reveal.
- Travel through multiple visual zones when the image supports it, such as overlook to road to bridge to terrace to interior.
- In city-waypoints mode, connect several recognizable locations in one city through fast FPV movement or invisible match transitions.
- Pass close to one or more foreground objects to create speed and depth.
- Bank, tilt, or drift gently around obstacles.
- When the source supports it, move from exterior to interior, such as flying over a bridge, past a terrace, and through open doors into a room.
- End on the destination, room, product, or strongest visual landmark.

People can make the shot feel more real and premium, but they should stay secondary: small in frame, natural, stable, and not presented as close-up faces or the main subject.

## Default generation prompt

```text
Create a vertical 9:16 FPV drone flythrough video from the provided scene image.

Preserve the original scene layout, architecture, landmarks, colors, and overall composition. Convert the still image into a deep 3D-feeling environment with strong parallax. The camera flies forward continuously like a small drone, starting from a wide view, moving along a smooth S-curve path, passing close to foreground objects, then revealing the main destination at the end.

Motion should be immersive, stable, cinematic, and energetic: confident forward acceleration, visible distance covered, gentle banking, close parallax passes, slight handheld drone vibration, realistic depth, atmospheric haze, and dynamic lighting. Keep the camera path readable and avoid sudden cuts.

No text, no subtitles, no UI, no logos, no watermark.
No red line, no arrows, no drawn path, no route markers, no graphic overlays.

Scene description: {{scene_prompt}}
Route: {{route}}
Speed: {{speed}}
Style: {{style}}
Destination: {{destination}}
Duration: {{duration}} seconds
Route length: {{route_length}}
Route mode: {{route_mode}}
```

## Route presets

### Fantasy castle route

```text
Fly low over the water or ground, curve around foreground rocks or trees, rise slightly toward the castle, pass near a tower or bridge, and finish facing the main gate. Epic fantasy, cloudy sky, cinematic haze.
```

### City canyon route

```text
Fly between tall buildings, skim past windows and signs, bank left and right through the street canyon, then reveal the skyline or central tower. Fast urban FPV, strong parallax, sunlight reflections.
```

### City waypoint route

```text
Create a fast city-scale FPV tour through several places in the same non-Chinese city. Start from a pulled-back skyline or aerial approach, dive between modern buildings, cross a bridge or transit line, skim through a plaza or street canyon, pass a rooftop or cultural venue, then finish inside or in front of the destination landmark. Use invisible match transitions if needed, but keep it feeling like one continuous energetic FPV journey. No domestic city elements, no Chinese signs, no recognizable real-world logos, no text overlays.
```

### Interior room route

```text
Start near the doorway, glide into the room, pass close to furniture and lights, curve around the main subject, then settle into a clean reveal. Smooth indoor FPV, realistic lens, stable exposure.
```

### Theme park route

```text
Fly along the track or walking path, pass close to colorful props, dip and rise with playful motion, then reveal the main ride or castle. Bright, energetic, travel-video feeling.
```

### Product reveal route

```text
Start close to foreground texture, slide forward and around the product, pass over or beside details, then finish on a hero angle of the product. Premium cinematic macro FPV.
```

### Exterior-to-interior villa route

```text
Start low over foreground rocks or landscaping, fly into an exterior passage or canyon, skim past a bridge or terrace, pass near small natural lifestyle figures, then fly through open glass doors into a premium interior room. Faster luxury real-estate FPV, strong parallax, clean indoor light transition, cinematic final reveal.
```

### Long destination route

```text
Start far back from a pulled-out overlook or wide approach, accelerate through a long visible path, pass two or more spatial landmarks such as a road, bridge, courtyard, pool deck, hallway, gate, or plaza, then enter or arrive at the final destination. The shot should feel like it covers real distance rather than zooming into one static scene.
```

## Route length presets

`short`:

```text
Compact FPV move inside one scene zone, with one close pass and one clean final reveal.
```

`medium`:

```text
Start from a readable exterior or room entrance, pass through two connected zones, then reveal the main destination.
```

`long`:

```text
Pulled-back start, extended forward travel, multiple connected zones, visible distance covered, faster pacing, and a final reveal after passing several landmarks.
```

## Route mode presets

`single-scene`:

```text
One continuous FPV route inside one coherent scene. Use this for interiors, rooms, product worlds, and compact venues.
```

`long-route`:

```text
One extended FPV route through connected spaces in the same destination, such as overlook to bridge to terrace to lobby.
```

`city-waypoints`:

```text
A city-scale FPV tour across different locations in one city. The camera may use seamless speed-ramp or match-cut transitions between waypoints, but the rhythm should feel like an intentional route: skyline, bridge, street canyon, plaza, rooftop, venue, interior reveal.
```

## Speed presets

`slow`:

```text
Slow floating drone movement, graceful and stable, long parallax, gentle turns, luxury cinematic reveal.
```

`medium`:

```text
Balanced FPV movement, clear forward momentum, smooth S-curve, close passes, cinematic but easy to follow.
```

`fast`:

```text
Fast agile FPV movement, energetic acceleration, banking turns, close flybys, strong motion blur, but no chaotic camera shake.
```

## Negative prompt

```text
Do not change the main scene into a different place. Do not add captions, text overlays, social media UI, subtitles, logos, watermarks, split screens, tutorial frames, talking head, screenshots, red route lines, arrows, drawn paths, markers, or graphic overlays. Avoid teleporting camera jumps, warped buildings, melted objects, duplicated landmarks, flickering geometry, unreadable motion, and random scene cuts.
```

## Best source images

- Clear depth: foreground, midground, background.
- A visible destination: gate, tower, building, product, stage, room center, bridge, portal.
- Enough space for a path through the scene.
- For long-route demos, choose images with multiple connected zones and a pulled-back starting point.
- For city-waypoint demos, choose a source image that establishes the city style and destination, then describe 3-5 waypoints in the prompt.
- Strong perspective lines help: roads, rivers, hallways, bridges, tracks, aisles.

Avoid flat portraits, close-up faces, plain walls, text-heavy screenshots, or images with no route space.

## Quality checklist

- The output is one continuous FPV shot.
- The camera clearly moves through the scene, not just zooming into a flat image.
- Foreground objects create parallax and depth.
- When the concept supports it, the shot travels through more than one zone, such as exterior to terrace to interior.
- For long-route demos, the camera starts pulled back and clearly covers distance before reaching the reveal.
- For city-waypoint demos, the video should feel like a fast tour across several locations in one city, not a single facade push-in.
- The final destination is visible and satisfying.
- The original scene identity is preserved.
- Any people remain natural, small, stable, and secondary to the space.
- There is no tutorial text, subtitle, UI, or watermark.
- There is no red path line, arrow, route marker, or annotation in the final video.
- The submitted video source image is clean; any red-line route image was used only as a motion-planning reference.

## Marketplace positioning

Chinese name: 无人机穿越镜头

English name: FPV Drone Flythrough

One-line description:

上传一张场景图，生成第一人称无人机穿越镜头：前景掠过、S 型路径推进、最后揭示主体，适合城堡、城市、室内、乐园和产品展示。

Best cover:

A 3:4 cover or short video cover may show a red route line as an explanatory planning graphic, but the actual before image and generated video sample should use the clean no-line source image.
