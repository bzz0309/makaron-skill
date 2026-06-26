---
name: makaron-doodle-sketch
description: >
  Doodle sketch style transform. Upload a photo, generate a hand-drawn crayon/pencil doodle sketch version.
  Ugly-cute aesthetic, exaggerated features, messy charming lines. Pure style transfer — no scene change.
allowed-tools: generate_image analyze_image Bash
metadata:
  makaron:
    icon: "✏️"
    color: "#F9A8D4"
    tags: [sketch, doodle, crayon, style-transfer, ugly-cute]
    faceProtection: default
    defaultAspectRatio: "1:1"
---

# Doodle Sketch — 手绘涂鸦风格转换

⚠️ 用户上传照片即开始，不问任何问题。

## 输出
一张 1:1 的手绘涂鸦风格画像。保留原照面部特征和发型，渲染为 messy crayon/pencil sketch 风格——夸张可爱、线条潦草有温度、像笔记本上的随手涂鸦。

## 核心理念

**身份幻想**：用了它我变成手绘涂鸦小人

**对标**：Ugly-Cute Sketch 的 crayon 变体。不是"把照片变成素描"，是"变成课本空白页上被同桌偷偷画的你"。

**分享场景**：IG Story / 头像 / 聊天表情包，1:1 直接发。

## 工作流

### Step 1: 读取输入
用户上传照片。直接使用，不询问任何问题。

### Step 2: 生成
```bash
makaron-cli chat --project auto --image <user_photo> --json -b "<prompt>"
```

**Prompt 模板**：
```
Transform this person into a hand-drawn crayon/pencil doodle sketch. Keep face identity, hairstyle, and expression 100% recognizable. Style: messy notebook doodle, exaggerated cute features, slightly larger eyes, simplified sketchy lines like a quick pencil drawing, pastel soft colors on white paper background. Imperfect charming strokes, like someone doodled you in the margin of their notebook. 1:1 square format. No text, no clean polished look — must feel like a real hand drawing.
```

### Step 3: 品质检查
- 面部可辨认 ✅
- 涂鸦风格明显（线条感、笔触可见）✅
- 1:1 正方形 ✅
- 无文字无品牌 ✅

### Step 4: 后处理
可选：加纸张纹理 subtle paper grain

### Step 5: 展示
直接展示生成结果。

## 品味指引

**对标大作**：Ugly-Cute Sketch、课本空白页随手画

**可量化指标**：
- 线条可见笔触（不是光滑矢量线）
- 色彩偏淡/粉彩（不是饱和度拉满）
- 背景纯白纸（不要加颜色）
- 面部特征保留可辨认

**反面教材**：
- ❌ 像 Midjourney 精修插画（太干净）
- ❌ 线条太规整像矢量图
- ❌ 颜色太浓像马克笔

## Rules
1. 零输入 — 上传照片立即开始，不问问题
2. 面部还原 — 五官可辨认，不是随便画个脸
3. 涂鸦笔触 — 线条必须有手绘质感，不能是光滑曲线
4. 粉彩色调 — 饱和度低，像蜡笔/彩铅
5. 白色纸背景 — 模拟纸上画的感觉
6. 1:1 正方形输出
7. 不添加文字/水印
8. 不改变发型发色
9. 夸张可爱 — 眼睛略大、线条潦草有温度
10. 品质底线 — 一眼能认出原人
