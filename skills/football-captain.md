---
name: football-captain
description: >
  Turn a portrait into a premium sports editorial motion poster.
  Auto-matches team colors to face ethnicity. Pipeline: analyze → poster → video → QC → reroll.
allowed-tools: [analyze_image, generate_image, generate_video]
metadata:
  makaron:
    icon: "⚽"
    color: "#1A1A2E"
    tags: [video, sports, football, editorial, poster, pipeline]
    modelPreference: [seedance]
    defaultAspectRatio: "4:5"
---

# Football Captain / 足球队长

把人像变成体育编辑级动态海报。左下全身球员做足球动作，右上近景肖像静态不动。
球队配色自动匹配人脸族裔。Pipeline 思维：每一步可 QC，失败可 reroll。

---

## 球队配色规则

| 族裔 | 地区 | 球衣主色 | 条纹色 | 文字色 |
|------|------|----------|--------|--------|
| 东亚脸 | 日本 🇯🇵 | 深海军蓝 + 白边 | 蓝白渐变 | 银白 |
| 东亚脸 | 韩国 🇰🇷 | 红 + 白 | 红白渐变 | 金 |
| 欧美脸 | 英格兰 🏴󠁧󠁢󠁥󠁮󠁧󠁿 | 白 + 深蓝 | 白蓝条纹 | 金 |
| 欧美脸 | 巴西 🇧🇷 | 黄 + 绿边 | 黄绿渐变 | 金 |
| 欧美脸 | 阿根廷 🇦🇷 | 蓝白条纹 | 蓝白渐变 | 金 |
| 欧美脸 | 法国 🇫🇷 | 深蓝 + 金边 | 蓝金渐变 | 金 |
| 非洲脸 | 非洲 🌍 | 绿 + 黄 | 绿黄渐变 | 金 |
| 中东/南亚 | 通用 | 白 + 绿 | 白绿渐变 | 金 |

**暗黑底色固定不变。无商标（足球图标代替品牌 logo）。**

---

## Pipeline

```
Step 1: 解析输入 → 族裔识别 → 选配色
Step 2: 海报生成 → 布局 QC（左下全身 / 右上近景 / 文字右下不挡脸）
Step 3: 视频生成 → 动画 QC（右上完全静态 / 左下动作层次 / 结尾对视）
Step 4: 终检 → 通过则交付，失败则 reroll（带失败原因）
```

### Step 1: 解析输入

- 接收用户人像，识别族裔、性别、年龄
- 从配色表选配色方案
- 保持原图骨相和特征

### Step 2: 海报生成

**布局（固定）：**
- 左下：全身球员，站草地，球在脚边，队服 #7，队长袖标
- 右上：大近景肖像，汗水光感，斜条纹背景
- 右下：CAPTAIN DEBUT 小字，银色+金色，不挡脸
- 底部：JFA 风格徽标 + 足球图标（无品牌商标）

**QC 检查点：**
| 项目 | 标准 | 失败处理 |
|------|------|---------|
| 人脸 | 骨相和特征不变 | 降低妆造力度重试 |
| 配色 | 族裔匹配正确 | 修正配色参数 |
| 布局 | 左下全身 + 右上近景，非左右分屏 | 强化布局约束 |
| 文字 | 右下 CAPTAIN DEBUT，小字不挡脸 | 缩字+移位置 |
| 商标 | 无 Nike/品牌 logo | 替换为通用足球图标 |

### Step 3: 视频生成

**动画时间轴（8s）：**
| # | 时间 | 左下（动） | 右上（静） |
|---|------|-----------|-----------|
| 1 | 0-2s | 脚趾挑球起 | 完全静止 |
| 2 | 2-4s | 双膝快节奏颠球 | 完全静止 |
| 3 | 4-6s | 踩单车左右假动作 | 完全静止 |
| 4 | 6-8s | 踩球 + 直视镜头 | 完全静止 |

**QC 检查点：**
| 项目 | 标准 | 失败处理 |
|------|------|---------|
| 右上静态 | 零移动，完全冻结 | 强化 static/frozen 约束 |
| 动作层次 | 4 段不同动作，非单一重复 | 加动作变化描述 |
| 结尾对视 | 最后 2s 眼睛看镜头 | 强调 direct eye contact |
| 布局不变 | 海报布局不漂移 | 用原海报做 image 输入 |
| 文字固定 | CAPTAIN DEBUT 不动 | 加 text stays fixed |

### Step 4: 终检

全部通过 → 交付。任一项失败 → 记录原因 → reroll。

---

## 失败原因库（已知）

| 失败模式 | 原因 | 修复 |
|---------|------|------|
| 布局漂移 | 配色改变时 AI 改了构图 | 强化 "SAME layout, only change colors" |
| 文字挡脸 | CAPTAIN 大字横跨中间 | 缩小 40% 移到右下 |
| 动作单一 | 只有颠球重复 | 改为 4 段：挑球→膝颠→踩单车→对视 |
| 右上动了 | Seedance 把静态肖像也动了 | 强化 "completely static, frozen, zero movement" |
| 商标风险 | 海报含 Nike 标识 | 替换为通用足球图标 |
| 人脸变形 | 妆造太重盖骨相 | 降低妆造强度 |

---

## Makaron

### 海报生成

```bash
npx makaron-cli chat --project auto \
  --image <用户头像.png> --json \
  -b "Transform person into sports editorial poster. Layout: full-body lower-left + close-up upper-right. Team colors: [族裔配色]. Text bottom-right only: CAPTAIN DEBUT in silver/gold. No brand logos — generic football icon only. Dark background. Keep face recognizable. 4:5 vertical."
```

### 视频生成

```bash
npx makaron-cli video create \
  --model seedance \
  --image <海报CDN> \
  --duration 8 --json \
  --script "8-second motion poster (4:5). Lower-left player: toe flick-up (2s), knee juggle (2s), step-over feint (2s), ball-plant stare-at-camera (2s). Upper-right portrait: completely static frozen. Stripes pulse subtly. Text fixed. Only lower-left moves. No camera movement."
```
