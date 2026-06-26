---
name: red-carpet
description: >
  Turn a portrait photo into a glamorous red carpet arrival video.
  Walk-stop-pose-flash rhythm at authentic awards show pace.
allowed-tools: [analyze_image, generate_image, generate_video]
metadata:
  makaron:
    icon: "🌟"
    color: "#C9A84C"
    tags: [video, red-carpet, glamour, awards, fashion, celebrity]
    modelPreference: [seedance]
    defaultAspectRatio: "4:5"
---

# Red Carpet / 红毯

把一张人像照片变成颁奖典礼级别的红毯入场视频。

**核心体验：** 走红毯→停下→对镜头摆 pose→闪光灯爆→转身→继续走。
真实 walk-stop-pose 节奏，不是慢动作走秀。

---

## 架构

本 Skill 单文件通用，适配 Makaron 市场和其他 Agent。

- **## 通用层**：平台无关的工作流、规则、质检标准
- **## Makaron**：Makaron 特定命令和参数（其他平台仿此节扩展）

上层定义"做什么"，平台节定义"用什么做"。

---

## 通用层

### 工作流

```
Step 1: 接收用户人像 → 提取人脸特征（保持骨相/性别/年龄/肤色）
Step 2: AI 妆造变换 → 红唇+钻饰+礼服+发型
Step 3: 图转视频 → walk-stop-pose 红毯节奏（12s）
Step 4: 质检 → 人脸/节奏/妆造/无UI
```

### Step 1: 接收输入

- 用户上传人像照片（正面或偏侧面，面部清晰）
- 不改变骨相、性别、年龄、肤色方向
- 不美颜、不网红滤镜

### Step 2: 妆造变换

**必须添加：** 明显唇色 / 精致眼妆 / 钻石耳环 / 项链 / 闪钻露肩礼服 / 好莱坞波浪发型

**必须保持：** 人脸骨相 / 肤色方向 / 性别年龄表达

**通用 Prompt：**
> 将此人转换为红毯妆造。保持骨相和面部特征。添加：明显唇色、精致眼妆、钻石耳环和项链、好莱坞波浪发型、闪钻露肩礼服。暖金布光，自信微笑。超写实杂志质感。

### Step 3: 视频生成

**节奏铁律：walk-stop-pose，不是慢动作。**

| # | 时间 | 动作 |
|---|------|------|
| 1 | 0-2s | 自然向前走 |
| 2 | 2-5s | 停下→面对右侧→手叉腰pose→闪光灯爆 |
| 3 | 5-8s | 转身面对左侧→换pose微笑→闪光灯连闪 |
| 4 | 8-10s | 转正面→对视镜头→微笑→优雅挥手 |
| 5 | 10-12s | 放下手→继续向前走 |

**禁止：** 慢动作 / 环绕运镜 / 电视UI / 字幕水印 / 无人机 / 走过回眸

**场景：** 红毯+金色绳栏+两侧狗仔虚化+闪光灯+暖金主光

### Step 4: 质检

| 检查项 | 标准 | 失败处理 |
|--------|------|---------|
| 人脸 | 骨相不偏离原图 | 降低妆造力度 |
| 节奏 | walk-stop-pose 清晰 | 调整时长 |
| 妆造 | 唇色+眼妆+耳环+项链+礼服齐全 | 强化 Step2 |
| UI | 无任何叠加文字图标 | 加负面词 |

### 变量

| 变量 | 默认 | 可选 |
|------|------|------|
| 礼服颜色 | 白色 | 红/黑/金/蓝 |
| 时长 | 12s | 8-15s |
| 珠宝 | 钻石 | 珍珠/金色 |

---

## Makaron

### 妆造变换

```bash
npx makaron-cli chat --project auto \
  --image <用户原图.png> --json \
  -b "Transform this person into a glamorous red carpet look. KEEP facial bone structure. ADD bold lipstick, smoky eye makeup, diamond drop earrings, layered necklace, Hollywood waves, sparkling white off-shoulder gown. Warm golden light. Confident smile. Hyper-realistic editorial. 4:5 portrait."
```

### 图转视频

```bash
npx makaron-cli video create \
  --model seedance \
  --image <CDN角色图URL> \
  --duration 12 --json \
  --script "A 12-second red carpet arrival (4:5 vertical), awards show pace. No slow motion, no TV graphics. Subject in sparkling gown, diamond jewelry, red carpet with gold stanchions, paparazzi flashes. Walk forward (2s). Stop, pose right, hand on hip, flash burst (3s). Turn left, pose with smile, more flashes (3s). Face center, eye contact, warm smile, elegant wave (2s). Walk forward past camera (2s). Warm golden light, real red carpet rhythm. No orbiting, no drones."
```

### 负面词

```
No slow motion, no TV graphics, no logos, no text, no subtitles,
no watermark, no UI, no drone shots, no camera orbiting, no gimmicks.
```

### 尺寸

| 参数 | 值 |
|------|-----|
| 角色图 | 4:5 (1080×1350) |
| 视频 | 4:5 (1080×1350) |
| 安全区上 | 80px |
| 安全区下 | 120px |
