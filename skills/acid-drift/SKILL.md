---
name: acid-drift
description: >
  上传照片，一键生成酸性荒漠公路赛车风格。Acid Road × LEMONADE × 荒漠公路文化。
  Drop a photo, get Acid Road desert highway racing style.
allowed-tools: generate_image analyze_image generate_animation
metadata:
  makaron:
    icon: "🍋"
    color: "#FFE600"
    defaultAspectRatio: "4:5"
    modelPreference: [openai]
    tipsEnabled: false
    tags: [video, acid, road, racing, desert]
---

# Acid Drift — 酸性漂移

Acid Road × LEMONADE × 荒漠公路文化。把你的照片变成酸性荒漠公路赛车风格。

---

## Core Layer（平台无关）

### Workflow

```
输入 → 角色设计 → 场景图 ×3 → 用户确认 → 渲染 15s 动画
```

### Step 1: 角色设计

生成一张角色设计板（三视角：全身 / 面部特写 / 侧颜）

| 参数 | 值 |
|------|-----|
| 比例 | 4:5 竖屏 |
| 模型偏好 | openai（面部还原更好） |
| 输出 | 1 张角色参考板 |

**角色 Prompt：**
```
Character design sheet for Acid Drift. Korean female driver, neon pink hair, 
blue eyes with subtle acid green glow. 3 angles on one sheet:
[1] Full body standing on desert highway, black racing jacket with neon green trim
[2] Close-up face portrait, slight smirk
[3] Side profile, pink hair in wind

Style: photorealistic, K-fashion aesthetic, polished finish.
Desert road background, bright sunny lighting.
```

### Step 2: 场景图 ×3

生成三张关键帧，同一角色贯穿：

**Scene 1 — Desert Highway**
```
Wide establishing shot. Desert highway panorama, bright noon sun, 
heat shimmer on horizon. ACID ROAD retro motel sign glowing neon yellow. 
Yellow vintage car with LEMON SLICE wheels parked roadside.
Acid green drip melting border frame. Graffiti paint splatter edges.
Lemon yellow + neon green palette. 9:16 vertical.
```

**Scene 2 — Cockpit POV**
```
Racing cockpit POV through windshield. Leather steering wheel with 
LEMON SLICE center logo. Desert highway curving ahead. 
Acid green speedometer HUD overlaid on glass.
Dripping paint border. Graffiti splatter. 9:16 vertical.
```

**Scene 3 — Full Reveal**
```
Yellow convertible car with LEMON SLICE wheels on desert highway.
The character leans on car hood, pink-yellow gradient hair flowing, 
black patent leather jacket, holding neon green drink. 
DIE HAPPY retro road sign behind.
Acid drip melting border. Graffiti splatter edges. 9:16 vertical.
```

### Step 3: 用户确认

三张场景图必须用户全部确认后才进入渲染。

### Step 4: 渲染 15s 动画

| 参数 | 值 |
|------|-----|
| 时长 | 15 秒 |
| 比例 | 9:16 竖屏 |
| 三幕 | Desert(5s) → Cockpit(5s) → Reveal(5s) |
| 转场 | Acid green drip transitions |
| 风格 | Bright sunny desert, acid neon accents |

**动画脚本：**
```
Scene 1 (0-5s): Desert highway push-in. ACID ROAD sign → car with lemon wheels. 
Scene 2 (5-10s): POV cockpit. Hands on lemon wheel → desert road through glass. 
Scene 3 (10-15s): Full character reveal. Leaning on yellow car, 
DIE HAPPY sign, holding neon drink. Acid drip dissolves into black.
```

---

## Adapter Layer（平台特定，agent 自行配置）

### 图片生成
- Makaron: `npx makaron-cli edit --model openai --size 1080x1920 --prompt "..."`
- OpenClaw: 使用 `image_generate` 工具
- 其他: 使用任意支持 OpenAI DALL-E / GPT Image 的图片生成工具

### 视频渲染
- Makaron: `npx makaron-cli chat --project auto --image <files> -b "<prompt>"`
- OpenClaw: 使用 `generate_animation` 工具（如有 seedance 集成）
- 其他: 使用 Runway / Pika / Kling 等视频生成工具

### 模型偏好
- 角色图：openai（面部还原更好）
- 场景图：openai 或 gemini（均可）
- 视频：seedance（首选）或等效视频模型

---

## Design Tokens

| 元素 | 值 |
|------|-----|
| 主色 | #FFE600（柠檬黄）, #39FF14（酸绿） |
| 字体风格 | Bold sans-serif, neon glow |
| 关键视觉 | 柠檬切片轮胎、荒漠公路、酸液滴落边框、DIE HAPPY 标语 |
| 轮胎设计 | 圆形柠檬切片——黄色轮辐+绿色轮边+白色果肉纹理 |
| 汽车 | 黄色复古敞篷/改装车 |
| 角色一致性 | 所有镜头同一张脸 |

## Rules

1. 三张场景图必须用户确认后才渲染——不跳步
2. 所有镜头同一角色，不换人
3. 车用柠檬切片轮胎，不悬浮
4. 酸性元素是点缀不是主导——底色是荒漠公路写实
5. before 图不与其他模板重复
