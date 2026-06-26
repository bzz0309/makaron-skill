---
name: rainy-kiss
description: >
  Turn any two characters/people into a passionate rainy kiss scene.
  Step-by-step workflow: enhance then add rain + wet clothes then intensify kiss then generate video script.
  Activate when user mentions: 雨中热吻, rainy kiss, 热烈亲吻, wet scene, 下雨接吻, or wants a romantic rainy video.
allowed-tools: generate_image analyze_image generate_animation
metadata:
  makaron:
    icon: "🌧️"
    color: "#C2185B"
    tipsEnabled: true
    tipsCount: 3
    modelPreference: [qwen]
    faceProtection: default
    tags: [romance, rain, kiss, video, workflow]
---

# Rainy Kiss 雨中热吻工作流

You are executing a 4-step cinematic romance workflow that transforms any photo of two people into a passionate, rain-soaked kissing video.

## Workflow Overview

Step 1: Dreamy Enhancement
Step 2: Rainy Atmosphere
Step 3: Passionate Kiss
Step 4: Video Script

Execute steps in order. After each step, briefly confirm the result and ask the user if they want to proceed to the next step. OR if the user says "全部做" / "一键完成" / "all steps", execute all 4 steps automatically without pausing.

---

## Step 1: Dreamy Enhancement

Goal: Make the scene romantic and ethereal — the visual foundation.

editPrompt template:
Dreamy romantic enhancement for this scene with two characters: add soft ethereal glow to the background elements, create a gentle bokeh effect on the background, add warm rose-gold color grading to the lighting, enhance the atmosphere with subtle light particles or petals drifting through the air. The overall mood should feel like a romantic movie still — soft, luminous, and emotionally charged. Preserve each person's face exactly as in the current photo. Do NOT change face shape, eyes, skin, or any facial features. Preserve exact composition and all people's positions. Do NOT add any text, watermarks, or borders.

Adapt the scene description to match what is actually in the photo (e.g. cherry blossoms, night club, street, forest, etc.).

---

## Step 2: Rainy Atmosphere

Goal: Add heavy rain, wet clothing, and cinematic storm energy.

editPrompt template:
Add a dramatic rainy atmosphere to this scene: heavy rainfall with clearly visible rain streaks diagonal across the frame, both characters clothes appear soaked through — wet fabric clinging to their bodies, darkened by water absorption, with glistening wet texture. Hair is wet and plastered to their faces/necks. Ground has puddles reflecting the background scene. Rain splashes visible on surfaces. The overall mood is stormy, intense, cinematic — like a pivotal scene in a romantic drama. Preserve each person's face exactly. Do NOT change facial features. Preserve exact composition and all people's positions. Do NOT add any text, watermarks, or borders.

Model: Use model qwen for wet clothing effects.

---

## Step 3: Passionate Kiss

Goal: Transform the characters interaction into an intense, passionate kiss.

editPrompt template:
Make the two characters kiss more passionate and intense — one character pulls the other close with both hands on their face/neck, bodies pressed together, lips locked in a deep kiss. The rain continues to pour heavily, water running down their faces and soaking their intertwined forms. Their eyes are closed, completely lost in the moment, oblivious to the storm. The kissing should feel urgent and emotionally overwhelming — like they have been waiting for this moment. Preserve each person's facial features and identity exactly. Do NOT change face shape, eyes, skin tone. Preserve the rainy atmosphere and wet clothing from the current photo. Do NOT add any text, watermarks, or borders.

### Step 3 Critical: Female Character Outfit Preservation
- If the female character wears a WHITE dress/top originally, the outfit MUST remain WHITE even when wet.
- Wet white fabric should become translucent/semi-sheer — clinging to the body, slightly see-through, glistening with water — NOT turn dark or black.
- Explicitly state in the editPrompt: "Her white dress must remain white — soaked and translucent/semi-sheer from rain, clinging to her body, NOT darkened or changed in color."

Model: Use model qwen for kiss intensity edits.

---

## Step 4: Video Script

Goal: Write a cinematic video script using the generated snapshots.

Image mapping:
- Step 1 result = dreamy/enhanced version, use for wide beauty shots or final pull-out
- Step 2 result = rainy atmosphere — SKIP if it doesn't add unique value vs Step 3
- Step 3 result = passionate kiss scene — use as the HOOK, core, and most repeated image

### Video Script Principles (learned from production)

**Duration**: Default 10-15 seconds. If user requests 15s, target 7 shots total.

**Shot composition**: Prioritize CLOSE-UPS. At least 4-5 out of 7 shots must be close or extreme close-up on the kiss. Wide shots should be rare and reserved for the final pull-back only.

**The "Wall Pin" shot (must include)**: Add a shot where the male character pins the female against a door/wall — hands pressing her wrists above her head, forceful kiss, rain running down both faces. This is a signature high-tension shot. Describe it with full physical detail:
- "The man slams the woman against a wooden door, both hands pressing her wrists above her head, leaning in forcefully to kiss her. Her soaked white dress presses against the door. Rain streams down both their faces. Orange lantern light glows on their profiles."

**Shot variety for close-ups**: Vary the angle each time — straight-on, side-profile low angle, orbiting, tilted handheld. Even if using the same source image, different camera descriptions will produce different feels.

**Sound design**: Each shot needs a specific sound cue. Build from rainstorm burst -> electric guitar -> orchestral strings -> music + rain fade. The arc is: explosive opening -> tension building -> emotional peak -> quiet fade.

**Script template for 15s (7 shots)**:

雨中烈吻

Shot 1 (2s): 极近特写，急速推进。IMAGE_STEP_3 — 两唇猛然相贴，雨水从嘴角滑落，白裙湿透贴身，呼吸交融。音效：雷声炸开，暴雨声骤然爆裂。
Shot 2 (2s): 超近景，手持颤抖感。IMAGE_STEP_3 — 男生一只手扣住女生后颈死死拉近，另一只手握住她的脸颊，两人嘴唇贴合，雨水顺着下颌线滑落，完全沉浸其中。音效：暴雨声盖过一切，低沉电吉他弦音撕裂进入。
Shot 3 (2s): 近景正面，手持晃动。IMAGE_STEP_3 — 男生将女生猛地抵在木质老门上，双手将她的手腕高举过头压住，俯身强吻，女生湿透白裙贴着门板，雨水从两人脸颊滑落，橙色灯笼暖光打在侧脸轮廓。音效：木门轻震声，暴雨声撕裂，电吉他弦音爆发。
Shot 4 (2s): 侧面近景，仰角。IMAGE_STEP_3 — 男生右手掌心平压在门板上、左手扣住女生腰部将她死死顶在门上无法动弹，俯身将嘴唇深深压在女生嘴上，女生双手被夹在身体与门板之间，头微微后仰承受着这一吻。音效：电吉他弦音持续，弦乐悄然入场。
Shot 5 (2s): 极近特写，环绕镜头。IMAGE_STEP_3 — 镜头缓缓绕行两人，侧面轮廓中男生手仍死死压住女生肩膀，女生白裙湿透若隐若现，两人嘴唇始终紧贴无法分离，樱花瓣粘在湿发上。音效：弦乐张力拉满，暴雨声渐成节拍。
Shot 6 (2s): 近景，正面，慢镜头。IMAGE_STEP_3 — 雨线如银针倾泻，男生双手缓缓从女生脸颊滑向她的腰间将她拉得更紧，嘴唇深深相贴，眼睛紧闭，橙色灯笼光晕在雨幕中扩散。音效：弦乐骤然爆发至高潮。
Shot 7 (3s): 广角，镜头缓缓后拉。IMAGE_STEP_1 — 两人紧紧相拥，周围樱花树与灯笼模糊成梦幻暖光晕，雨声与音乐交融渐渐淡出，只剩这一刻是清晰的。音效：弦乐与雨声交织，缓缓淡出。
Style: 电影质感，京都暴雨夜，手持镜头，极近特写主导，强烈情感张力，橙色灯笼暖光。

After writing the script, ask the user to confirm before calling generate_animation.

### Adjusting shot count for different durations:
- 10s -> 5 shots (keep Shots 1, 2, 3, 5, 7 from template)
- 7s -> 4 shots (keep Shots 1, 2, 3, 7)
- 5s -> 3 shots (keep Shots 1, 3, 7)
- 15s -> use all 7 shots above

---

## General Rules

1. Always use model qwen for Steps 2, 3, and any follow-up edits involving wet clothing or kissing — do NOT use Gemini for these steps.
2. Face preservation is critical — both characters facial identities must be maintained across all steps.
3. Build on previous steps — each step uses the previous steps result as the base image (not the original).
4. Adapt prompts to the actual scene — if it is not cherry blossoms, adjust environmental details accordingly.
5. The rain must be HEAVY and dramatic — light drizzle is not the target. Think monsoon, not mist.
6. The kiss must feel URGENT and emotional — not a gentle peck. Think passionate reunion scene in a movie.
7. If the user only wants one specific step, execute only that step.
8. If the user says "帮我做雨中热吻视频" or equivalent, execute all 4 steps automatically.
9. If Step 2 (rainy atmosphere) produces a result without visible differences from Step 3, skip it in the video script. Use Step 1 only for wide/pull-back shots.
10. Video scripts should default to 15s (7 shots) unless user specifies otherwise.

## Common Fix Patterns

**Female outfit color changed to dark/black after wet effects:**
-> Re-edit with explicit: "Her [white/original color] dress must remain [color]. Wet fabric should be translucent and clinging, NOT darkened. The dress color must stay [color]."

**Too many wide shots in video, not enough intimacy:**
-> Restructure: only 1 wide shot (final shot), all others must be close-up or extreme close-up.

**Video AI not understanding body position:**
-> Describe every physical detail explicitly: which hand is where, which direction the person is leaning, what is touching what, where the pressure is applied. Leave nothing to interpretation.

**Shot looks too similar to previous shot:**
-> Specify a different camera angle: straight-on vs side-profile vs orbiting vs low-angle vs tilted.

## Tips Directions

- 雨中热吻完整流程: Execute the full 4-step workflow automatically — dreamy enhancement then rainy atmosphere then passionate kiss then video script.
- 暴雨时刻: Add dramatic heavy rain to the scene with wet clothes, puddles, and rain streaks. Cinematic storm atmosphere.
- 热烈之吻: Transform the two characters into a passionate kiss — hands on face, bodies pressed together, completely lost in the moment.
