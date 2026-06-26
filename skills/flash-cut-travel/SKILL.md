---
name: flash-cut-travel
description: >
  上传一张自拍，自动生成10秒超速闪切旅行自拍视频。20个全球地标，
  每0.5秒硬切一个城市。服装根据性别、年龄和地点随机生成，
  每次运行都不同。自拍杆广角视角，电影级色彩。
allowed-tools: generate_image analyze_image Bash mcp__makaron__makaron_write_video_script mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status mcp__makaron__makaron_create_music mcp__makaron__makaron_get_music_status
metadata:
  makaron:
    icon: "⚡"
    color: "#FF4500"
    tags: [travel, flash-cut, selfie, video, landmarks, montage, rapid, 闪切, 旅行, 快剪]
    tipsEnabled: true
    tipsCount: 4
    faceProtection: strict
    defaultAspectRatio: "9:16"
    modelPreference: [openai]
    videoModel: seedance
---

# 10秒闪切 — Flash-Cut Travel Selfie

**⚠️ 重要：用户在对话中附带的图片就是输入照片，直接使用。不要说"没有看到照片"或要求用户重新上传。用户输入的任何文字都只是触发信号 — 立即开始工作。**

上传一张自拍照，零文字输入，自动生成一段10秒超速闪切旅行自拍视频。20个全球地标，每0.5秒硬切一次，服装随机生成。

This skill uses **videoModel: seedance** for one-shot 10-second video generation.

## Core Concept

参考效果：[Kōda "20 Cities in 10 Seconds with Gemini Omni"](https://x.com/i/status/2057157014397264350)

- AI 视频模型一次性生成整段10秒视频（非图片拼接）
- 20个城市地标，每0.5秒硬切
- 同一人物严格身份一致
- 自拍杆 POV，广角镜头
- 每个城市不同服装、不同姿势、不同光照
- **服装不固定**：AI 根据性别/年龄/城市随机搭配，每次运行结果都不同

## 去同质化机制

**服装不写死具体单品**。只给规则让 AI 自由发挥：
- 根据角色性别和年龄选择合适风格
- 根据城市气候和文化氛围适配
- 20个城市的服装必须视觉差异明显（不同色系、不同轮廓、不同风格）
- 每次生成应该产出不同的搭配组合

**姿势/表情保留参考方向**（与地标有关联性），但 AI 可自由发挥变体。

---

## 地标 × 姿势参考（20个）

| # | 城市 · 地标 | 姿势/表情方向 |
|---|------------|-------------|
| 1 | Paris · Eiffel Tower | 微笑挥手 |
| 2 | Tokyo · Shibuya Crossing | 比V、俏皮眨眼 |
| 3 | New York · Times Square | 兴奋大笑 |
| 4 | Rome · Colosseum | 回望镜头、沉思 |
| 5 | Cairo · Pyramids | 惊叹遮阳 |
| 6 | Rio · Christ the Redeemer | 欢乐仰头大笑 |
| 7 | London · Big Ben | 看手表坏笑 |
| 8 | Sydney · Opera House | 灿烂微笑 |
| 9 | Agra · Taj Mahal | 双手合十 |
| 10 | Beijing · Great Wall | 胜利握拳 |
| 11 | Moscow · Red Square | 冬日温暖微笑 |
| 12 | Istanbul · Hagia Sophia | 欢迎微笑 |
| 13 | Venice · Canals | 迷人侧头 |
| 14 | Dubai · Burj Khalifa | 抬头惊叹 |
| 15 | Peru · Machu Picchu | 幸福喘息 |
| 16 | Athens · Acropolis | 自信风吹发 |
| 17 | Berlin · Brandenburg Gate | 点头眼神接触 |
| 18 | Amsterdam · Windmills | 放松微风 |
| 19 | Barcelona · Sagrada Familia | 张嘴惊叹 |
| 20 | Seoul · Gyeongbokgung | 比心、最终微笑 |

---

## Workflow

### Step 1：读取照片

直接读取用户已上传的照片。
- 1+ 张照片 → 取第一张作为身份参考
- 0 张照片 → 请求上传自拍

### Step 2：analyze_image 分析照片

调用 `analyze_image` 提取：
- 性别、年龄范围
- 面部特征（发型、发色、肤色、五官）
- 整体气质

### Step 3：生成视频

**直接调用 makaron video 生成整段10秒视频。**

**生成工具**：makaron-cli（推荐）或 MCP tool

**makaron-cli 方式：**
```bash
export MAKARON_API_KEY=<key>

# 上传照片获取 CDN URL
RUN_ID=$(npx makaron-cli chat --project auto \
  --image "<用户自拍>" \
  --json -b "Keep this image as reference." | jq -r '.runId')

# 等待获取图片 URL
IMG_URL=$(npx makaron-cli responses get $RUN_ID --pick first_image_url)

# 提交视频渲染
npx makaron-cli video create \
  --script "<下方 Prompt 模板>" \
  --image "$IMG_URL" \
  --duration 10 \
  --aspect-ratio "9:16" \
  --model seedance
```

**MCP tool 方式：**
```
mcp__makaron__makaron_create_video:
  script: <Prompt 模板>
  images: [<CDN URL>]
  duration: 10
  aspectRatio: "9:16"
  videoModel: "seedance"
```

**Prompt 模板：**

```
The main character is <<<media_1>>>. Create a 10-second hyper-speed fast-forward selfie travel video. Strict identity consistency — <<<media_1>>> must be the same person in every single shot throughout the entire video.

20 distinct tourist spots worldwide with hard cuts on every single beat. Handheld selfie-stick camera angle, wide-angle lens capturing the character's face, outfit, and iconic landmark. High definition, vibrant cinematic color grading.

OUTFIT RULES:
- Character is {性别}, approximately {年龄} years old
- For each city, automatically choose an outfit that matches the local climate, culture, and fashion
- All 20 outfits must be visually distinct (different color palettes, different silhouettes, different styles)
- AI freely decides specific garments — do NOT repeat similar looks
- Outfits should look natural and fashionable for someone actually traveling to each location
- Each run should produce DIFFERENT outfit combinations

Locations and poses (1-20):
1. Paris, Eiffel Tower | Smiling, classic hand wave
2. Tokyo, Shibuya Crossing | V-sign, playful wink
3. New York, Times Square | Wide-eyed excited laugh
4. Rome, Colosseum | Thoughtful expression, looking back at camera
5. Cairo, Pyramids | Amazed expression, shielding sun
6. Rio de Janeiro, Christ the Redeemer | Joyful laugh, head tilted back
7. London, Big Ben | Subtle smirk, looking down at watch
8. Sydney, Opera House | Sunny bright smile at camera
9. Agra, Taj Mahal | Serene positive expression, hands together
10. Beijing, Great Wall | Victory fist, determined expression
11. Moscow, Red Square | Warm smile, breath visible in cold air
12. Istanbul, Hagia Sophia | Warm welcoming smile
13. Venice, Canals | Charming smile, slight head tilt
14. Dubai, Burj Khalifa | Admiring smile, looking up in awe
15. Peru, Machu Picchu | Breathless happy smile, scenic backdrop
16. Athens, Acropolis | Proud confident expression, wind in hair
17. Berlin, Brandenburg Gate | Friendly nod, direct eye contact
18. Amsterdam, Windmills | Relaxed content smile, gentle breeze
19. Barcelona, Sagrada Familia | Mouth open amazed expression
20. Seoul, Gyeongbokgung | Finger heart gesture, final cute smile

CRITICAL RULES:
- Every location is INSTANT hard cut — NO transitions, NO fades, NO dissolves
- Each location approximately 0.5 seconds
- The person MUST be the same face throughout — strict identity from <<<media_1>>>
- Selfie-stick POV with wide-angle lens throughout
- Person always facing camera
- Vibrant cinematic color grading
- High energy, fast rhythm
```

### Step 4：轮询视频状态

调用 `makaron_get_video_status`：
- 每 15 秒轮询
- 预计 3-5 分钟
- 完成后获取 videoUrl

### Step 5：叠加 BGM（后处理）

视频完成后，用 ffmpeg 叠加卡点音乐：

```bash
# 生成 BGM（或使用预设音乐）
npx makaron-cli music create "Fast electronic travel montage, BPM 150, percussive beats for hard cuts, building energy, dramatic stop at end"

# 等待音乐完成后叠加
ffmpeg -y -i video.mp4 -i bgm.mp3 \
  -c:v copy -c:a aac -b:a 192k \
  -map 0:v:0 -map 1:a:0 -shortest \
  final_video.mp4
```

**⚠️ 绝对不使用 -an 参数，必须保留音频。**

### Step 6：展示结果

```
⚡ 10秒闪切旅行视频已完成！

[视频]

20个城市 · 10秒极速闪切 · AI随机服装

你可以：
1. ✅ 保存当前结果
2. 🎲 重新生成（新的随机服装组合）
3. 🎵 换一段BGM
```

---

## Tips Directions

1. **环球闪切**: Upload your selfie — 10 seconds, 20 cities, instant hard cuts. Different outfit at every stop, all randomly generated to match each location. Every run is unique.
2. **风格随机**: Your face stays the same but AI picks completely different outfits for each city based on local fashion and climate. Paris chic, Tokyo street, Cairo explorer — all auto-generated.
3. **卡点节拍**: Fast electronic beats synced with every hard cut. 20 beats, 20 cities, 10 seconds of pure travel energy.
4. **再来一次**: Same cities but completely different random outfits each time. Say "re-roll" for a fresh combination.

---

## Core Rules

1. **身份一致是最高优先** — 10秒视频中人脸必须始终一致，不能出现不同的人
2. **硬切是核心** — 只用硬切，不用任何过渡效果（无渐变/溶解/闪白）
3. **10秒 × 20城市** — 每城市约0.5秒，总时长10秒
4. **自拍杆 POV** — 广角镜头，人物面向镜头
5. **服装随机** — 不固定具体单品，AI 根据性别/年龄/城市自由搭配
6. **服装不重复** — 20个场景视觉差异必须明显
7. **seedance 模型** — 一次性生成整段视频，不做图片拼接
8. **BGM 后叠加** — 视频生成后用 ffmpeg 叠加卡点音乐
9. **零输入** — 上传照片即开始，不问问题
10. **视频必须保留音频** — ffmpeg 不用 -an

### What to NEVER Do

- 不要用静态图片 + ffmpeg 拼接（效果像幻灯片，没有闪切感）
- 不要写死具体服装单品（导致同质化）
- 不要用渐变/溶解/闪白过渡（破坏硬切节奏）
- 不要让每个场景停留超过1秒（太慢）
- 不要生成不同性别/不同人的画面（严格身份一致）
- 不要跳过 BGM 叠加步骤
