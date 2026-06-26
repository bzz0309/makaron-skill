---
name: makaron-rain-control-v3
allowed-tools: [generate_video, analyze_image]
metadata:
  makaron:
    icon: "🌧️"
    color: "#2563EB"
    tags: [video, vfx, rain-control, magic, cinematic]
    faceProtection: default
    defaultAspectRatio: "9:16"
    models: [seedance, seedance-fast, kling, grok]
---

# Makaron Rain Control V3

## Core Concept

用户提供人物参考图/视频或文字主体描述，本 skill 生成一段“掌心控雨”电影感短视频。默认效果是 v3 稳定版：人物在雨夜中走近镜头，停步后把一只手掌正对镜头，前景雨水从掌心附近开始减速并凝固成自然悬停的散点水滴，最后形成清晰的英雄镜头。

这个 skill 是通用能力，不绑定任何电影、城市、演员、品牌或固定人物。任何 agent 都必须根据输入生成 `plan.json`、`prompt_used.md`、`qc_report.md` 和最终视频。

## Input Schema

| 字段名 | 必填 | 类型/格式 | 说明 |
|---|---:|---|---|
| `primary_reference` | 否 | 文件 / URL / null | 主参考图或视频；用于保留人物身份、服装、脸、镜头或动作逻辑。 |
| `subject_description` | ✅ | 字符串 | 主体描述，例如“戴眼镜的年轻男性魔术师”。 |
| `scene_setting` | 否 | 字符串 | 场景描述；未提供时默认“generic rain-soaked urban night street”。 |
| `opening_action` | 否 | 字符串 | 控雨前动作；未提供时默认“walks slowly toward the camera through heavy rain”。 |
| `trigger_action` | 否 | 字符串 | 触发动作；未提供时固定为“一只手掌正对镜头，五指自然张开”。 |
| `effect_progression` | 否 | 字符串 | 雨水变化机制；未提供时使用 v3 默认机制。 |
| `style_constraints` | 否 | JSON / 字符串 | 风格要求；未提供时默认 photorealistic cinematic live-action VFX。 |
| `identity_constraints` | 否 | JSON / 字符串 | 保脸、保服装、保发型、保表情等约束。 |
| `negative_constraints` | 否 | JSON / 字符串 | 额外负面约束；默认包含禁止泡水、水环、水墙、遮脸、手部畸变等。 |
| `output_format` | ✅ | JSON | 输出比例、时长、格式；必须包含 `aspect_ratio`、`total_duration_seconds`、`file_format`。 |

### Complete JSON Example

```json
{
  "primary_reference": "person_reference.jpg",
  "subject_description": "a calm young man wearing gold-rim glasses, a black suit jacket, and a white shirt",
  "scene_setting": "a generic rain-soaked urban night street with wet pavement and soft city bokeh lights",
  "opening_action": "walks slowly toward the camera through heavy rain",
  "trigger_action": "he stops, locks eyes with the camera, and raises one open hand with the palm facing directly toward the lens",
  "effect_progression": "rain nearest the palm slows first, vertical rain streaks break into individual droplets, then the whole foreground control zone freezes into suspended droplets",
  "style_constraints": {
    "visual_style": "photorealistic cinematic live-action VFX",
    "lighting": "cool blue night lighting with wet pavement reflections",
    "camera": "single video-model run, slow backward tracking shot, then close hero portrait"
  },
  "identity_constraints": {
    "preserve_face": true,
    "preserve_glasses": true,
    "preserve_outfit": true,
    "preserve_expression": true
  },
  "negative_constraints": [
    "no flood",
    "no lake",
    "no waterline across the body",
    "no droplets covering the face or glasses",
    "no circular water ring",
    "no water wall",
    "no extra fingers"
  ],
  "output_format": {
    "aspect_ratio": "9:16",
    "total_duration_seconds": 5,
    "file_format": "mp4"
  }
}
```

## Safety

### Allowlist

- Fictional cinematic magic, rain control, suspended droplets, harmless water manipulation, high-speed-camera style VFX.
- User-provided original人物、普通路人、虚构角色、非品牌服装、通用城市雨夜场景。
- Non-graphic, non-violent spectacle where the effect is environmental and harmless.

### Blocklist

Block or rewrite requests involving:

- Weapons as the main effect, realistic injury, blood, gore, torture, or harm to real people.
- Sexual content, nudity, fetish content, or sexualized minors.
- Real celebrity imitation or face replacement unless the platform policy and rights are explicitly cleared.
- Protected movie titles, exact film scene recreation, copyrighted character costumes, brand logos, sponsor marks, UI overlays, map UI, score overlays.
- API keys, access tokens, private credentials, or hidden production configuration.

### Identity / Face Rules

- If `primary_reference` contains a real person, preserve identity only when the user is authorized to use that reference.
- Do not transform the subject into a different real person or celebrity.
- Face must remain clear in the final video: no foreground droplets covering eyes, nose, mouth, or glasses.
- If the face drifts, reroll with stronger identity preservation language.

### Brand / Logo / IP Rules

- Do not mention protected film names, famous magician names, exact costumes, logos, franchise marks, or branded places in the generated prompt.
- Convert inspirations into generic language such as “cinematic street-magic rain-control VFX”.

### Minors / Sexual / Violence Rules

- Minors are allowed only for safe, non-sexual, non-violent fantasy VFX.
- Any sexualized minor, coercive sexual content, realistic harm, or graphic violence is BLOCKED.

### BLOCKED Conditions

Stop and notify human if:

- The request requires protected IP recreation, celebrity impersonation, sexual content, graphic violence, or brand/logo insertion.
- Required subject information is missing and no safe generic fallback is possible.
- The subject is lost after all budgeted attempts.
- All three generation attempts fail QC.

## Budget

| 轮次 | 模型 | 说明 |
|:--:|---|---|
| 1 | seedance | 主生成，优先用于真人电影感 VFX 和主体连续性。 |
| 2 | kling | Reroll 1，用于修复手部、动作、雨滴形态或镜头问题。 |
| 3 | grok | Reroll 2，用于替代模型尝试。 |

If `seedance` is unavailable, use `seedance-fast` as the first fallback. After 3 failed attempts, mark BLOCKED and write the reason in `qc_report.md`.

## Workflow

### Step 1 — Validate Input

Confirm required fields exist: `subject_description` and `output_format`.

If missing optional fields, apply these defaults:

```json
{
  "scene_setting": "a generic rain-soaked urban night street with wet pavement, soft city bokeh lights, and cool blue cinematic lighting",
  "opening_action": "walks slowly toward the camera through heavy rain",
  "trigger_action": "he stops, locks eyes with the camera, and raises one open hand smoothly toward the lens, palm facing directly toward the camera, fingers spread naturally",
  "effect_progression": "rain nearest the palm slows first; vertical rain streaks break into individual droplets; the stopped zone expands from the hand to the whole foreground around the face and shoulders; the droplets hang motionless in midair",
  "visual_style": "photorealistic cinematic live-action VFX",
  "camera": "single video-model run; slow backward tracking shot during the walk, then settles into a close hero portrait as the hand reaches the camera"
}
```

Reject unsafe or protected-IP requests according to Safety.

### Step 2 — Analyze Reference Assets

If `primary_reference` is provided, call `analyze_image` or equivalent reference analysis.

Extract only execution-relevant facts:

- Face and identity anchors
- Hair, glasses, clothing, pose, expression
- Camera angle, framing, and background cues
- Elements that must not change

Write these facts into `plan.json`.

### Step 3 — Build Structured Plan

Create `plan.json`:

```json
{
  "subject": "...",
  "scene_setting": "...",
  "opening_action": "...",
  "trigger_action": "...",
  "effect_progression": "...",
  "final_hero_moment": "...",
  "style_constraints": {},
  "identity_constraints": {},
  "negative_constraints": [],
  "output_format": {},
  "safety_status": "PASS"
}
```

The plan must stay parameter-driven. Do not add fixed cities, famous people, movie names, brands, logos, or unrelated props.

### Step 4 — Fill Locked Prompt Template

Fill the English template below exactly. Do not translate, rewrite, reorder, delete, or add sections. Only replace `{placeholder}` values with validated values from `plan.json`.

Write the final prompt to `prompt_used.md`.

### Step 5 — Generate

Call `generate_video` with:

- Model from the budget order.
- `primary_reference` if provided.
- Prompt from `prompt_used.md`.
- Aspect ratio and duration from `output_format`.

### Step 6 — QC

Inspect the generated video. Use PASS / REROLL / BLOCKED.

Write `qc_report.md` with:

- Model used
- Attempt number
- Checks passed
- Checks failed
- Decision
- Reroll reason, if any

### Step 7 — Deliver or BLOCKED

If PASS, deliver:

- `final_artifact.mp4`
- `plan.json`
- `prompt_used.md`
- `qc_report.md`

If budget is exhausted or safety fails, do not deliver a misleading video. Mark BLOCKED and explain the failure in `qc_report.md`.

## Prompt Template

Do not translate, rewrite, reorder, delete, or add sections. Replace placeholders only.

```text
VIDEO SPEC
Create a {total_duration_seconds}-second {aspect_ratio} photorealistic cinematic live-action magic VFX video in {file_format} format.

SUBJECT
The main subject is {subject_description}.
If a reference asset is provided, preserve the subject identity according to {identity_constraints}.
Preserve the face, outfit, hairstyle direction, expression, and key accessories from the reference.

SCENE
The scene is {scene_setting}.
The subject is fully above the ground, standing and walking on visible wet pavement.
No flood, no pool, no lake, no waterline across the body.

SHOT TIMING
0.0-1.5s:
The subject {opening_action}. Heavy rain falls normally as clear vertical streaks around the subject. The camera slowly tracks backward in a medium portrait framing from head to waist. The subject looks calm and focused.

1.5-2.4s:
The subject stops walking. The gaze locks onto the camera. The subject performs this trigger action: {trigger_action}. The palm becomes the visual center of the frame. Keep the hand anatomically correct: five fingers, natural knuckles, no extra fingers, no warped palm.

2.4-3.4s:
As the palm faces the camera, an invisible pressure wave expands outward from the palm. {effect_progression}. The rain nearest the palm visibly slows first. Vertical rain streaks break into individual droplets. The stopped zone expands from the hand to the whole foreground around the face and shoulders.

3.4-{total_duration_seconds}s:
The rain in the foreground control zone is completely frozen in midair. Individual droplets hang motionless like irregular glass beads between the palm and the camera, around the face, and beside the shoulders. No raindrops continue falling in the foreground control zone. The palm remains facing the camera, close to the lens, slightly larger from perspective. The subject stands still, calm and powerful, framed by suspended droplets and wet city lights.

VISUAL STYLE
Use {visual_style}. High-speed camera feeling, realistic water refraction, sharp suspended droplets, wet pavement reflections, cool night tones, elegant cinematic street-magic illusion.
The suspended droplets must be sparse, irregular, and natural. They must not connect into rings, chains, walls, arcs, domes, cages, halos, or geometric curtains.

CAMERA
Use {camera}. Keep the motion smooth and physically readable. The final frame must clearly show the palm facing camera plus frozen rain droplets suspended around the subject.

CONTINUITY
Use one continuous video-model run with coherent temporal continuity.
Keep the subject identity stable. Keep hands natural and readable. Keep face clear and unobstructed.
No droplets may cover the eyes, nose, mouth, or glasses.

NEGATIVE CONSTRAINTS
Avoid: {negative_constraints}.
No flood. No lake. No pool. No waterline across the chest. Do not put the subject in water. Do not submerge the torso. No giant water surface covering the lower frame. No rising water column from the body. No circular water ring. No connected water chain. No splash ring. No water wall. No dome. No cage. No geometric droplet grid. No ice shards. No random symbols. No text. No watermark. No UI. No brand logo. No extra fingers. No fused fingers. No distorted hand. No face swap. No unrelated scene change.
```

## QC

| 结果 | 条件 | 动作 |
|---|---|---|
| PASS | 主体保留，手掌正对镜头，雨滴从掌心附近开始减速并在前景悬停，脸干净，身体没有泡水，输出符合时长/比例。 | Deliver all required files. |
| REROLL | 小失败：脸漂移、手部变形、雨还在前景继续下、雨滴连成水环/水墙、主体泡水、镜头丢失主体。 | Strengthen failed constraint, switch to next budget model, regenerate. |
| BLOCKED | 安全违规、主体丢失、3 次预算耗尽、prompt 偏离模板或缺失必要输入。 | Stop and notify human in `qc_report.md`. |

### QC Checklist

- [ ] Subject identity is preserved when a reference is provided.
- [ ] Opening has normal falling rain before the magic trigger.
- [ ] Trigger action is one readable open palm facing the camera.
- [ ] Hand anatomy is coherent with five natural fingers.
- [ ] Rain near the palm slows first.
- [ ] Foreground rain freezes into suspended individual droplets.
- [ ] Final droplets are sparse, irregular, and not connected into rings, walls, arcs, chains, domes, cages, or grids.
- [ ] Face, eyes, mouth, and glasses remain clear.
- [ ] Subject is fully above visible wet pavement, not submerged.
- [ ] No text, watermark, UI, logo, protected IP, or random symbols.
- [ ] Output duration, aspect ratio, and format match `output_format`.

## Output

Always produce or request the platform to store these files:

- `final_artifact.mp4`
- `plan.json`
- `prompt_used.md`
- `qc_report.md`

If generation is blocked, produce:

- `plan.json`
- `prompt_used.md` if safe to write
- `qc_report.md` with `decision: BLOCKED`

## Anti-Hardcoding Rules

- Do not hardcode any city, actor, movie, famous magician, brand, costume, logo, song, UI, or franchise.
- Do not mention protected film names or exact film scenes in the final prompt.
- Do not add directional left/right/overhead rain-control choreography unless the user explicitly asks for it.
- Do not default to circular water rings, water walls, domes, cages, ice shards, or connected water chains.
- Do not turn natural-language enum values into technical jargon inside the video prompt.
- Do not add extra effects beyond palm-triggered rain suspension unless needed for physical readability.
- Do not rely on a specific agent's hidden knowledge. Every execution decision must come from the input schema, workflow, safety rules, budget, prompt template, and QC.
