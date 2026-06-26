---
name: ai-fruit-drama
description: >
  Analyze photo vibe → generate cinematic 3D fruit character drama scene.
  NOT transforming the photo — creating a fresh Pixar-quality fruit character
  that captures the photo's mood, colors, and energy. Movie poster style with
  dramatic lighting, text overlays, and miniature props. Optimized for Gemini.
  Activate when user wants fruit characters, food animation, anthropomorphic food,
  AI fruit story, or fruit drama.
allowed-tools: generate_image analyze_image generate_animation
metadata:
  makaron:
    icon: "🍓"
    color: "#FF6B6B"
    tags: [fruit, animation, drama, anthropomorphic, 3d, cinematic, viral, short-form, food, gemini, seedance, video]
    tipsEnabled: true
    tipsCount: 5
    modelPreference: [gemini, seedance]
    faceProtection: default
    defaultAspectRatio: "9:16"
---

# AI Fruit Drama — 水果大戏

Analyze the photo's mood → pick fruit from vibe table → generate cinematic 3D fruit drama scene. **Create from scratch, never transform.** Result: Pixar-quality movie poster with dramatic lighting, text overlays, and miniature props.

## ⚠️ Critical Rules (Tested & Confirmed 2026-05-27)

| Rule | Why |
|------|-----|
| `model: gemini` | OpenAI produces generic fruit; Gemini captures photo vibe better |
| `useOriginalAsReference: false` | ON = human in fruit costume; OFF = actual fruit character |
| "NOT human. NOT animal. A FRUIT." | Without this, AI generates people with orange skin |
| Full drama prompt REQUIRED | Short prompts = boring "fruit on counter"; drama = movie poster |
| Fruit name disambiguation | `kiwi fruit` not `kiwi`; `orange fruit` not `orange` |

## editPrompt (THE TEMPLATE THAT WORKS)

```
Look at this photo. Vibe: {vibe_keywords}.

Generate a 3D-animated {FRUIT_TYPE} FRUIT character (the fruit, NOT the color/human/animal). NOT a human. NOT an animal. A REAL {fruit_appearance} — {texture_details}, cute face directly on the fruit surface, tiny arms and legs attached to the fruit body. {personality_description}. {accessory}.

DRAMATIC SCENE: {scene_setting} — {scene_details}. Dramatic {lighting_type} lighting, volumetric god rays, rim lights haloing the character. Shallow depth of field. Background: {secondary_characters} in soft bokeh, {reaction}. Miniature props: {props}.

TEXT OVERLAY: top '{DRAMATIC_TITLE}' in bold cinematic serif font, movie poster style. bottom '{SUBTITLE}' in clean sans-serif italic.

9:16 vertical. Pixar/DreamWorks 3D animation film screenshot quality. Rich saturated colors, dramatic cinematic lighting, subtle film grain and professional color grading.

model: gemini, skill: creative.
```

## Fruit Name Disambiguation (MANDATORY)

| Write | NOT | Why |
|-------|-----|-----|
| kiwi fruit | kiwi | Generates a bird |
| orange fruit | orange | Generates the color |
| date fruit | date | Calendar confusion |
| All fruits | Just the name on first use | Safety |

## Character System

### Fruit Characters
| Fruit | Personality | Accessory | Role |
|-------|------------|-----------|------|
| 🍓 Strawberry | Sassy dramatic diva | Tiny golden crown | Main Character |
| 🍌 Banana | Goofy clumsy lovable fool | Oversized sunglasses | Comic Relief |
| 🍍 Pineapple | Regal villainous arrogant | Spiky cape / scepter | Villain |
| 🍋 Lemon | Sour-faced perpetually annoyed | Tiny reading glasses | Skeptic |
| 🫐 Blueberry | Tiny cute easily flustered | Over-sized bow tie | Sidekick |
| 🍉 Watermelon | Chill wise zen master | Tiny meditation cushion | Mentor |
| 🍑 Peach | Flirtatious soft-spoken romantic | Silk scarf | Love Interest |
| 🍇 Grape (bunch) | Cliquey gossipy | Matching tiny hats | Mean Girl Squad |
| 🍊 Orange fruit | Enthusiastic competitive | Sweatband / whistle | Jock |
| 🥝 Kiwi fruit | Shy secretly fierce | Tiny hoodie | Underdog |
| 🍒 Cherry (pair) | Inseparable duo | Connected by stem | Best Friends |
| 🥭 Mango | Smooth talker charming | Gold chain | Smooth Operator |
| 🍐 Pear | Awkward self-deprecating | Tiny backpack | Everyman |

### Vegetable Characters
| Veg | Personality | Accessory | Role |
|-----|------------|-----------|------|
| 🥑 Avocado | Health-conscious anxious | Tiny tote bag | Over-thinker |
| 🥕 Carrot | Overachiever type-A | Tiny clipboard | Boss |
| 🌽 Corn | Loud dad jokes | Tiny baseball cap | Dad Energy |
| 🧅 Onion | Emotional makes everyone cry | Tiny tissue box | Tragic Backstory |
| 🥦 Broccoli | Protective nurturing | Tiny umbrella | Guardian |
| 🌶️ Pepper | Spicy hot-tempered | Tiny matchstick | Loose Cannon |

### Vibe → Fruit Matching
| Photo Vibe | Fruit |
|-----------|-------|
| Warm, cozy, home, relaxed, fluffy hair | 🍊 Orange fruit |
| Confident, posing, sunglasses | 🍍 Pineapple |
| Smiling, warm, friendly | 🍓 Strawberry |
| Goofy, funny face, messy | 🍌 Banana |
| Serious, stoic | 🍋 Lemon |
| Small, cute, shy, pet | 🫐 Blueberry |
| Chill, relaxed, lounging | 🍉 Watermelon |
| Romantic, couple, soft light | 🍑 Peach or 🍒 Cherry |
| Group, squad, friends | 🍇 Grape bunch |
| Sports, action, energetic | 🍊 Orange fruit |
| Moody, dark, dramatic | 🌶️ Pepper |
| Awkward, candid, caught off-guard | 🥝 Kiwi fruit |
| Glamorous, luxury | 🥭 Mango |
| Overthinking, anxious, tired | 🥑 Avocado |
| Working, busy, focused | 🥕 Carrot |
| Nurturing, protective, parent | 🥦 Broccoli |
| Loud, joking, dad energy | 🌽 Corn |
| Emotional, teary | 🧅 Onion |
| Clean, casual, fresh, laid-back | 🍊 Orange fruit or 🍓 Strawberry |

### Drama Scenarios
1. **ROMANTIC BETRAYAL**: "Caught sneaking into the SMOOTHIE with someone else"
2. **WORKPLACE DRAMA**: "Day 47 at Fruit Bowl Inc. No promotion."
3. **REALITY SHOW**: "The most DRAMATIC fruit salad confession — live on Fruit Island"
4. **VILLAIN ORIGIN**: "They called me TOO SOUR. So I became the villain."
5. **EXISTENTIAL CRISIS**: "What if I'm NOT the main character?"
6. **COMEBACK ARC**: "Everyone counted me out. But ripening changes a fruit."
7. **LOVE TRIANGLE**: "Two fruits. One spot in the bowl."
8. **CASUAL VIBES**: "No plans. Just vibes." (for relaxed photos)

### Scene Settings
| Setting | Details | Lighting |
|---------|---------|----------|
| Kitchen Counter Cinematic | Marble surface, fruit bowl bokeh | Golden hour, god rays |
| Cozy Bedroom | Pink blankets bokeh, mini phone prop | Soft morning window light |
| Fruit Bowl Colosseum | Fruits on rim like spectators | Dramatic arena lighting |
| Smoothie Bar Noir | Blender shadows, dark moody | Cold blue, fog |
| Refrigerator Noir | Fog from open door | Cold blue rim light |
| Beach Sunset | Sugar sand, juice water | Golden sunset |

## Workflow (Image)

### Step 1: Analyze Photo Vibe
Look at the photo. Pick 3 keywords from the vibe table. Map to fruit.

### Step 2: Generate Image
`makaron-cli edit --model gemini --skill creative` with the full editPrompt template. Fill ALL fields — character, scene, lighting, text, props.
**Always include "NOT human. NOT animal. A FRUIT."**

### Step 3: Deliver Image
Present the generated movie-poster style fruit drama scene.

## Workflow (Video Short Drama) — 2026-06-01 定版

🚨 视频生成走 Seedance（不是 Kling）。Kling 自己编台词且读参考图文字当配音；Seedance 一字不差复述脚本 DIALOGUE。

### Pre-Production（视频前必做，7步链路）

```
Step 0: 照片分析 → vibe → 匹配水果角色
Step 1: 视频脚本（剧情+DIALOGUE+场景+角色）← 先定剧本
Step 2: 角色身份板（按脚本需要出，不限定数量）
Step 3: 场景设定图（按脚本地点出）
Step 4: 分镜图×N（按脚本镜头出，6/9/12镜）
Step 5: 分镜故事板拼图（N宫格）
Step 6: 生成视频提示词（基于故事板提炼）
Step 7: 发用户确认 → 渲染（Seedance）
Step 8: 字幕（silencedetect + STT）
```

> ⚠️ Step 1 必须先出脚本。脚本定义了角色、场景、镜头，后续 Step 2-5 都按脚本要求来。

#### Step 1: 视频脚本

剧情驱动。必须包含：
- DIALOGUE 段落（每角色台词）
- 场景描述（灯光/道具/情绪）
- 角色数量（不限定，按剧情需要）
- 分镜规划（几镜、每镜时长和内容）
- 灯光弧线（如暖→冷）

**脚本检查清单：**
1. 有因果链？每镜发生因为前一镜
2. 角色情绪对？拒绝不脸红、背叛不微笑
3. 有起承转合？Setup→Conflict→Climax→Resolution
4. 逻辑自洽？每个角色动机能解释

#### Step 2: 角色身份板

按脚本角色列表，逐个出图。数量不限（2 角色爱情片 / 5 角色群像剧 都可以）。
用 `makaron-cli edit --model openai --skill creative`。

标注：个性描述、配件、角色弧线（如 CONFIDENT → HEARTBROKEN → DIGNIFIED）。

```
CHARACTER IDENTITY BOARD — [角色名] ([身份标签])
Pixar-style 3D character design sheet，中性背景。
描述外观+个性标注。9:16竖屏。
```

#### Step 3: 场景设定图

按脚本场景列表，逐个出图。空场景，无角色。
标注：区域功能（告白区/拒绝区）、灯光方案、关键道具位置。

#### Step 4: 分镜图

按脚本分镜列表，每镜单独 `makaron-cli edit`。
标注：镜头号、时长、机位、灯光、情绪。

```
STORYBOARD — SHOT N/M: [标题] ([时长])
Pixar-style 3D storyboard frame。[场景描述+角色动作+情绪]
STORYBOARD MARKINGS: 'SHOT N — X-Ys'。[机位+灯光标注]
9:16垂直。
```

#### Step 5: 分镜故事板拼图

用 ffmpeg 将 N 张分镜拼成宫格（6镜=3×2，9镜=3×3，12镜=4×3）：

```bash
ffmpeg \
  -i shot1.jpg -i shot2.jpg ... -i shotN.jpg \
  -filter_complex "
    [0:v]scale=360:640,drawtext=text='SHOT 1':fontsize=14:fontcolor=white:box=1:boxcolor=black@0.5:x=5:y=5[v0];
    ...
    [v0][v1][v2]hstack=3[row0];
    [v3][v4][v5]hstack=3[row1];
    [row0][row1]vstack=2,format=yuv420p
  " -frames:v 1 storyboard-grid.jpg
```

#### Step 6: 视频提示词

基于分镜故事板，提炼为 Seedance 可用的视频提示词。

**提示词格式：**
- DIALOGUE 段落（精确台词，Seedance 会一字不差复述）
- 每镜的画面描述（角色/场景/动作/灯光/情绪）
- 灯光弧线（如 warm pink-orange → cold blue-gray）
- 字幕标注：NO TEXT OVERLAYS（字幕后期烧录）
- `<<<media_1>>>` 引用参考图
- 风格标注：Pixar 3D animation, 9:16 vertical

**生成后发用户确认，再渲染。不能跳过。**

### 视频脚本铁律

- ✅ 必须有完整剧情弧线（起承转合），不能是"一个角色摆pose"
- ✅ 情绪逻辑自洽（拒绝你的人不脸红心动，被背叛的人不对你微笑）
- ✅ 脚本里必须写 DIALOGUE 段落，标注每句台词
- ✅ 参考图必须无文字（Kling 会读图上的字当配音。Seedance 也建议用清洁图）
- ✅ 参考图用 `makaron-cli create --image` 上传拿公开 URL
- ⛔ **禁止灯光变化**：AI 无法渐变过渡（会硬切），脚本必须全片统一灯光。反复写 "Same warm light throughout" / "Uniform lighting. No lighting transitions."
- ⛔ **禁止重复动作**：脚本里每个动作只出现一次。"跳下"只写一次，否则 AI 会生成两次跳跃

### 渲染

```bash
makaron-cli video create \
  --script "$(cat script.txt)" \
  --image "<clean-reference-url>" \
  --model seedance \
  --duration 15
```

### ⚠️ 已知 AI 局限（写脚本时必须避开）

| 局限 | 表现 | 规避 |
|------|------|------|
| 灯光渐变 | 暖→冷 = 硬切，不会淡入淡出 | 全片统一灯光 |
| 重复动作 | "跳下"写两次 = AI 生成两次跳跃 | 每个动作只写一次 |
| 渐变过渡 | 无淡入淡出能力 | 不做场景间渐变 |
| 面部细节 | 表情可能鬼畜 | 不要求微表情变化 |

### 字幕（silencedetect 粗切 → STT逐段验证 → 修正 → 烧录）

```bash
# 1. 提取音频
ffmpeg -i video.mp4 -acodec pcm_s16le -ar 16000 -ac 1 audio.wav

# 2. silencedetect 粗切语音段
ffmpeg -i video.mp4 -af "silencedetect=noise=-30dB:d=0.5" -f null - 2>&1 | grep silence

# 3. ⚠️ 逐段 STT 验证（关键！silencedetect 三大陷阱）
#    陷阱A: 长句内部停顿被误判为分段（如 "There's" | "something I need to tell you"）
#    陷阱B: 背景音乐被当说话（短段<0.5s多半是音乐）
#    陷阱C: 画面开场可能1-2s无声（不要从0s开始字幕）
ffmpeg -i video.mp4 -ss START -t DUR -acodec pcm_s16le -ar 16000 -ac 1 segN.wav
miaoda-studio-cli speech-to-text --file segN.wav --lang en
# → 某段只拿半句话 → 和下一段合并
# → 某段无文字 → 跳过（音乐/噪音）
# → 验证段数 = DIALOGUE 行数时才算对齐

# 4. 修正后写 SRT，烧录
ffmpeg -i video.mp4 \
  -vf "subtitles=subs.srt:force_style='FontName=DejaVu Sans,FontSize=13,PrimaryColour=&HFFFFFF,OutlineColour=&H000000,Outline=0.8,Alignment=1,MarginV=60,MarginL=30'" \
  -c:v libx264 -preset ultrafast -crf 23 -c:a copy -y output.mp4
```

**字幕风格定版：** DejaVu Sans, FontSize=13, Outline=0.8, 白色, **左对齐**(Alignment=1), MarginV=60, MarginL=30。小字、薄描边、不抢画面。

**字幕时间轴铁律：**
- ⛔ 第一条字幕不从 0s 开始——用 STT 0-1s / 0.5-1s 抽查看开口时刻
- ⛔ silencedetect 结果不能直接用——必须逐段 STT 验证
- ✅ 验证段数 = DIALOGUE 行数 → 时间轴对齐

## Tips Directions

1. **Warm Home Vibe**: Upload cozy selfie → orange fruit in golden kitchen light, tiny mug with steam, "HOME SWEET HOME" / "The warmest fruit in the bowl."

2. **Boss Energy**: Confident photo → pineapple villain in refrigerator noir, dramatic cape, cold blue shadows, "THE BOSS" / "Respect the crown."

3. **Casual Saturday**: Laid-back selfie → orange fruit with sweatband, cozy bedroom bokeh, soft morning light, "CASUAL SATURDAY" / "No plans. Just vibes."

4. **Pet Energy**: Cute animal photo → kiwi fruit in tiny hoodie, autumn forest bokeh, "THE FUZZY ONE" / "Soft outside. Fierce inside."

5. **Group Drama**: Squad photo → grape bunch in fruit bowl colosseum, dramatic arena lighting, "MEET THE BOWL" / "Season 3 is wild."
