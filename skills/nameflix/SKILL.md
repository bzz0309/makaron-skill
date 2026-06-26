---
name: nameflix
description: >
  上传昵称+照片+类型，生成 Netflix 风格流媒体平台 UI 动画。
  Your name + photo + genre → Netflix-style streaming platform intro.
allowed-tools: generate_image analyze_image generate_animation
metadata:
  makaron:
    icon: "🎬"
    color: "#E50914"
    defaultAspectRatio: "4:5"
    modelPreference: [openai, seedance]
    imageGeneration: "Makaron CLI chat --project auto"  # bzz 2026-06-10: 图+视频全走 Makaron CLI
    tags: [video, ui, netflix, streaming, identity]
---

# Nameflix

上传昵称+照片+类型 → 生成 Netflix 风格个人流媒体平台 UI 动画。15s · 4:5 竖屏。

---

## Workflow

```
输入(昵称+照片+类型) → Logo → 登录页 → 主页 → 三张确认 → 渲染 15s 动画
```

## Step 1: 收集输入

| 字段 | 说明 |
|------|------|
| 昵称 | 平台名 = `{昵称}FLIX` |
| 照片 | 登录页 Profile 1 |
| 类型 | 动作谍战 / 霓虹赛博 / 犯罪纪录 / 史诗奇幻 / 科幻太空 / 恐怖惊悚 / 喜剧浪漫 / 动画奇幻 / 历史战争 / 西部冒险 / 悬疑推理 / 超级英雄 |

## Step 2: Logo（Makaron CLI · 1080×1350 · 4:5）

一张纯黑+红B。极简几何粗体，扁平无效果。

```
Pure black background #000000 filling entire 4:5 frame. Dead center: a single flat ultra-bold geometric sans-serif uppercase red letter "B" (#E50914). No 3D extrusion, no glow, no particles, no reflections, no floor, no text. Pure flat red B on pure black. Minimalist.
```

## Step 3: 登录页（Makaron CLI · 1080×1350 · 4:5）

```
Dark Netflix-style background #141414. Top center: "{昵称}FLIX" in bold red Netflix font. "Who's watching?" in white, ONE single line. 4 profile circles in a row:
1. bzz: user's real photo, label "bzz"
2. Alex: blue-toned avatar, label "Alex"
3. Fer: green abstract avatar, label "Fer"
4. Kids: yellow playful avatar, label "Kids"
Dark cinematic UI. 4:5 vertical, edge to edge, no white borders.
```

**bzz 头像：** 必须用真实照片裁圆合入，不 AI 生成。

## Step 4: 首页（Makaron CLI · 1080×1350 · 4:5）

```
Dark Netflix UI #141414. Top nav: "{昵称}FLIX" logo left, menu items right. Hero section: dark action movie poster with original title + tagline, cinematic hero shot. Red "▶ Play" button bottom-left. Content rows below with thumbnails. All titles 100% original fiction. 4:5 vertical, edge to edge, no white borders.
```

**类型映射：**

| 类型 | 英雄影片 | 行标签 |
|------|---------|------|
| 动作谍战 | SHADOW CODE | Action Thrillers / Spy Series |
| 霓虹赛博 | NEON VOID | Cyberpunk / Digital Noir |
| 犯罪纪录 | BLOOD TRAIL | True Crime / Investigative |
| 史诗奇幻 | CROWN OF ASHES | Fantasy Epics / Magical Worlds |
| 科幻太空 | BLACK HORIZON | Space Operas / Alien Encounters |
| 恐怖惊悚 | THE DEEP BELOW | Horror / Psychological Thrillers |
| 喜剧浪漫 | KISSING IN PARIS | Romantic Comedies / Feel Good |
| 动画奇幻 | THE LAST SPIRIT | Animated Adventures / Family Favorites |
| 历史战争 | IRON & HONOR | War Epics / Historical Dramas |
| 西部冒险 | DUST & VENGEANCE | Westerns / Survival Adventures |
| 悬疑推理 | THE 13TH FLOOR | Mystery / Mind-Bending Thrillers |
| 超级英雄 | PHOENIX RISING | Superheroes / Origin Stories |

## Step 5: 三张图确认

Logo + 登录 + 首页，全部必须用户确认后才渲染。不跳步。

## Step 6: 渲染 15s 动画（Seedance · 4:5）

| 段落 | 时长 | 内容 |
|------|------|------|
| Logo | 3s | 纯黑1s → 单竖红光闪过0.5s → 多竖线向两边扩散0.5s → 扁平粗体红B骤然成形1s → 切黑 |
| 登录 | 4s | UI淡入 → 光标移到bzz → 悬停辉光 → 点击 → 切黑 |
| 首页 | 3s | 首页加载 → 光标移到Play → 悬停 → 点击 |
| 结尾 | 5s | 谍战风：雨夜暗巷追踪+激光瞄准+冲刺拐角+HUD锁定 → 硬切黑 |

**禁止：** 汇聚回弹、粒子、棱镜、扫描光带、放射光、结尾B闪现。

## Design Tokens

| 元素 | 值 |
|------|-----|
| 品牌色 | #E50914 |
| 背景 | #000000 (Logo) / #141414 (UI) |
| 分辨率 | 1080×1350 (4:5) |
| Logo | 扁平极简红B · 无效果 · 纯黑底 |
| 动画 | 四步：纯黑→单竖光→多线扩散→B成形 |
| 结尾 | 谍战动作 · 单幕 · 动态紧张 |

## Rules

1. 三张 UI 图用户确认后才渲染——不跳步
2. Logo 四步动画：纯黑→单竖红光→多竖线向两边扩散→B成形。无汇聚回弹
3. 登录页 bzz 头像用真实照片，不 AI 生成
4. 所有片名虚构，绝不使用真实 IP
5. 全程 4:5 满屏 · 1080×1350 · 无黑边/白边
6. 结尾单幕谍战动作，不静止
7. 平台名格式 `{昵称}FLIX` 全大写
