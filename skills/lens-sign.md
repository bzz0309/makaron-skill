---
name: lens-signature-video
description: |
  根据用户上传的一张人物自拍或头像参考，生成“音乐节大屏直播镜头签名”短视频：人物作为巨型 LED 大屏里的直播近景出现，手持签字笔贴近镜头玻璃写出发光手写轨迹，签完后自然收尾。
  适用于“镜头签名视频”“音乐节大屏签名”“上传自拍生成同款签名视频”“复刻大屏直播签名效果”“lens signature video”等需求。不要用于普通自拍美化、账号搜索片尾、人物站在大屏前或无签名互动的视频。
trigger-words: [镜头签名视频, 音乐节大屏签名, 签名视频模板, 上传自拍生成同款视频, 复刻镜头签名效果, 自拍手写签名视频, festival screen signature, lens signature video]
---

# Lens Signature Video

Use this skill when the user provides a selfie, portrait, avatar, or character reference and wants a short “lens signature” video: the person appears as a live close-up on a giant music-festival LED screen, writes glowing signature strokes on the lens/glass surface with a visible pen, then naturally finishes with a small camera-facing gesture.

This skill is intentionally portable: it does not depend on a specific project, a specific reference video, or a specific model. Any orchestrator or media agent can follow the input/output contract and route image, video, and editing work to the tools available in its runtime.

## Output Target

Default deliverable:

- Format: short video.
- Aspect ratio: `16:9` unless the user explicitly asks for another ratio.
- Duration: approximately `6–8 seconds`.
- Structure: one continuous shot, not a multi-scene montage.
- Core action: live festival-screen close-up → visible pen touches lens glass → glowing signature forms on the foremost layer → signature completes → natural camera-facing outro gesture.
- Exclusions: no account search page, no platform end card, no black outro card, no ordinary selfie beautification, no person standing in front of or behind a big screen.

## STEP 0: Collect Inputs

Required input:

1. **Person reference image**: a selfie, portrait, avatar, or character image used as identity reference.

Optional inputs:

1. **Signature text**: a name, nickname, handle, short word, or custom handwritten mark.
2. **Outro gesture**: for example pen pullback, slight wave, hand near lens, small heart gesture, cold stare, smile, wink, or still pause.
3. **Festival screen intensity**: subtle LED-screen texture, obvious giant-screen frame, visible crowd/stage context, or abstract concert-light atmosphere.
4. **Audio preference**: native model audio, silent clip, light crowd ambience, pen-stroke sound, or later post-production audio.

Defaults when missing:

- If signature text is missing, use an abstract cursive signature stroke rather than asking the user to stop.
- If outro gesture is missing, choose a natural pen pullback followed by a brief camera-facing pause.
- If aspect ratio is missing, use `16:9`.
- If duration is missing, target `6–8 seconds`.

## STEP 1: Analyze the Person Reference

Before generation, extract only the identity and behavior signals needed for video consistency:

- Face shape and key facial features.
- Hair shape, length, fringe, accessories, glasses, hat, or other strong identifiers.
- Clothing silhouette and any identity-relevant styling.
- Expression and temperament: cold, cheerful, shy, confident, glamorous, casual, etc.
- What must not change when the person moves close to the camera.

Do not overfit to irrelevant background details from the input photo unless the user asks to keep them.

## STEP 2: Build the Creative Brief

Create a compact brief with these fields:

```yaml
person_identity: <key identity features to preserve>
signature_content: <provided text or abstract signature stroke>
festival_screen_style: <LED screen / live broadcast / stage context intensity>
outro_gesture: <natural gesture after signature completion>
aspect_ratio: <default 16:9 unless specified>
duration: <default 6-8 seconds>
audio: <native, silent, ambience, or post-production>
```

Important framing rule:

- The whole video should look like a giant festival or concert LED screen is showing a live close-up feed of the person.
- The person is **inside the screen feed**, not physically standing in front of the screen, not facing away from the screen, and not using a screen as a background wall.

## STEP 3: Generate or Prepare the Video Input

Choose the available route:

### Route A: Direct reference-to-video

Use the person reference image directly as the subject reference for video generation. This is preferred when the available video model supports reference images and subject consistency.

### Route B: First-frame route

If the video model is stronger with first-frame input:

1. Generate a first frame from the person reference.
2. The first frame must already show the person as a live close-up on a giant festival LED screen.
3. The person must visibly hold a pen near the lens/glass surface.
4. Use that first frame to generate the 6–8 second motion clip.

### Route C: Editing route

If the generated video includes extra end cards, black frames, search pages, or platform UI:

1. Trim them out.
2. Keep only the strongest continuous lens-signature segment.
3. Do not add subtitles unless the user asks.

## STEP 4: Video Generation Requirements

The generated video must satisfy all of these:

- The subject appears as a live broadcast close-up on a giant music-festival or concert LED screen.
- The LED screen can show subtle pixel grid, scan texture, stage-light reflection, screen edge, or a sense of crowd viewing, but the main image remains the live close-up feed.
- The subject clearly holds a pen or marker. A hand-only or empty-finger writing gesture is not acceptable.
- The pen tip approaches or touches the invisible lens/glass surface.
- A glowing, semi-transparent, smooth handwritten signature stroke appears on the foremost layer, above the subject and the broadcast image.
- The signature motion feels like writing on the camera lens or transparent glass, not on paper, a notebook, a wall, or an overlay floating randomly in space.
- The subject’s expression and temperament follow the input reference.
- After the signature completes, the subject performs a small natural outro gesture without cutting to a new scene.

Recommended timing:

- `0–2s`: subject close to the live camera feed; pen enters frame.
- `2–5s`: pen writes the glowing signature on the lens layer.
- `5–6s`: signature completes; pen pauses briefly.
- `6–8s`: pen pulls back or subject gives a natural camera-facing outro gesture.

## STEP 5: Prompting Pattern

When dispatching to a video agent, include a self-contained task description with:

- `model: <selected model>` if the orchestrator requires explicit model routing.
- `aspect_ratio: 16:9` unless user specified otherwise.
- `duration: 6-8s` or the closest supported value for the selected model.
- Reference image paths.
- The identity preservation list from Step 1.
- The festival-screen live-broadcast framing rule.
- The visible-pen requirement.
- The no-search-page / no-platform-outro exclusion.

Reusable core prompt:

```text
Generate a short lens-signature video from the provided person reference. The entire video should look like a giant music-festival LED screen is showing a live close-up feed of this person. The person is inside the screen feed, not standing in front of a big screen and not facing away from it. Preserve the person’s identity features from the reference. The person comes close to the live camera, clearly holds a pen or marker, touches the pen tip to the transparent lens/glass surface, and slowly writes a glowing semi-transparent cursive signature on the foremost layer of the image. The signature must look written on the camera lens, not on paper. After completing the signature, the pen pulls back and the person gives a small natural camera-facing outro gesture. Use subtle LED screen texture, stage-light reflection, and festival audience/stage atmosphere without distracting from the face and pen. No account search page, no platform outro, no subtitles, no black end card, no paper writing, no empty-hand writing.
```

Adapt the language to the user’s language when dispatching.

## STEP 6: Quality Check

Before presenting the result, verify:

- The subject still resembles the reference image.
- The entire visual logic reads as a giant festival LED screen live feed.
- The result is not a person standing in front of a screen, behind a screen, or using a big screen as background.
- A pen or marker is visible during the writing action.
- The signature stroke is on the foremost lens/glass layer.
- The action includes writing start, signature completion, and a natural outro gesture.
- The video has no account search page, platform end card, black outro, or unrelated UI.
- The video avoids dirty over-sharpening, excessive VFX, and flashy transitions.

## STEP 7: Failure Recovery

Common failures and fixes:

- **Looks like a person in front of a screen**: regenerate with “the whole frame is the LED screen’s live broadcast image; the person is inside the screen feed.”
- **No pen appears**: regenerate with “visible pen or marker in hand; pen tip touches lens glass; empty-hand writing is not acceptable.”
- **Writes on paper or wall**: regenerate with “transparent camera lens/glass surface; signature is the foremost overlay layer.”
- **Search page or platform outro appears**: trim it out or regenerate with strong exclusion.
- **Signature text is unreadable**: keep the abstract handwritten stroke if the lens-writing action is strong; do not over-retry text precision unless the user explicitly needs readable text.
- **Identity drifts**: generate a stronger first frame or identity anchor image, then use that for video generation.
- **Outro missing**: request a short pen pullback or camera-facing pause after the signature completes.

## STEP 8: Present Result

Report concisely:

- Input reference used.
- Signature text or abstract-signature strategy.
- Whether the festival-screen live-feed effect is present.
- Whether the visible pen requirement is satisfied.
- Outro gesture used.
- Duration and aspect ratio.
- Any remaining limitation that should be fixed in the next iteration.
