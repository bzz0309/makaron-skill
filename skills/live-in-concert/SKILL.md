---
name: concert-lipsync
description: >
  梦燃现场 — 上传照片，一秒站上万人体育场舞台。AI 演唱会视频，有口型、正面唱、拉麦高音、焰火、荧光棒。
  Live in Concert — Drop a photo and headline your own stadium concert. Lip-sync, front-facing, mic pull, pyro, crowd.
allowed-tools: generate_image analyze_image generate_animation
metadata:
  makaron:
    icon: "🎤"
    color: "#8B00FF"
    defaultAspectRatio: "9:16"
    modelPreference: [openai, seedance]
    tipsEnabled: false
    tags: [video, concert, lipsync, music, stage, performance]
---

# Concert Lip-Sync — 梦燃现场

上传照片 → 三视图/脚本/分镜 → 确认 → 15s 演唱会视频。

**核心风格**：有口型 · 正面唱 · 拉麦高音 · 焰火 · 荧光棒海洋 · 零背影零剪影。

## Workflow

```
照片 → 角色三视图 → 9镜脚本 → 9宫格分镜故事板 → 用户确认 → 视频渲染
```

## Step 0: 角色三视图

先出角色舞台化三视角（正面/侧面/半身），用户确认后进脚本。

**女生 → Girl Crush**：
- 服装：银色亮片夹克 + 皮质胸衣 + 皮短裤 + 膝高靴
- 妆容：浓烟熏眼妆 + 飞翼眼线 + 酒红唇
- 配饰：大银圈耳环 + 层叠 choker + 无指皮手套

**男生 → Stadium Rock**：
- 服装：铆钉皮夹克 + 破洞牛仔裤 + 军靴
- 妆容：深邃眉骨 + 轻微烟熏下眼线 + 哑光裸唇
- 配饰：金属链项链 + 耳钉 + 皮质手环

## Step 1: 9 镜脚本

15s 9 镜四段结构。每镜六要素：编号/时长/景别运镜/画面内容/光影/Sound。

```
Shot 1 (2s): 侧颜开唱 — 中近景侧脸，话筒近嘴，嘴微张唱，柔追光，暗舞台
Shot 2 (2s): 正面推进 — 近景推进，转正面，嘴开口型清晰，眼神直视镜头
Shot 3 (1s): 观众沸腾 — 切观众，荧光棒挥舞，手机拍摄海洋
Shot 4 (2s): 伸展台走来 — 全身正面跟拍，手持话筒大步走来，一手伸向观众
Shot 5 (2s): 拉麦高音 ⚡ — 正面大特写 80%+，话筒拉远 20-30cm，嘴大张飙高音
Shot 6 (1s): 灯光海 — 切观众远景，万人荧光棒蓝色海洋，焰火远处炸开
Shot 7 (2s): 英雄绽放 — 低角度正面仰拍，双臂张开一手高举话筒，焰火炸开
Shot 8 (1s): 火花副歌 — 正面中近景，手臂张开唱副歌，话筒在手中，金色火花雨
Shot 9 (2s): 定格 — 正面定格，下巴微抬眼神凶狠，话筒近嘴如刚唱完，全灯光
```

### 核心规则

1. **所有表演镜头正面/侧脸对镜头**，零背影，零剪影
2. **口型可见**，每个表演镜头嘴在动/在唱
3. **话筒全程在手**，Shot 5 拉麦嘶吼（经典摇滚动作），Shot 7/8 一手高举话筒
4. **2 段观众切镜**（Shot 3 + Shot 6）
5. **人物占比 60%+**，场景只做背景

### 风格参数

- 电影级演唱会纪实摄影
- 冷蓝基调 + 金色暖光对比
- 重胶片颗粒，浅景深
- 9:16 竖屏，无文字覆盖

## Step 2: 9 宫格分镜故事板

用角色参考图生成 3×3 分镜图。黑色速写风格，每格标注镜头编号和关键动作方向箭头。发用户确认。

## Step 3: 用户确认

三视图 + 脚本 + 分镜 → 用户确认 → 进渲染。

## Step 4: 视频渲染

| 参数 | 值 |
|------|-----|
| 模型 | Seedance 2.0 |
| 时长 | 15s |
| 比例 | 9:16 竖屏 |
| Prompt | 9 镜完整脚本，带上角色三视图和分镜图作为参考 |

**Prompt 强制要求**：
- 使用 character reference 锁定面部/发型/服装
- 使用 storyboard reference 锁定镜头构图
- 每镜标注 "Face stable, no distortion"
- 口型必须在每个表演镜头中可见
- 话筒必须在 Shot 5 拉远、Shot 7/8 在手中
- 禁止背影，禁止剪影
- 2 段观众切镜

## Step 5: 音乐合成（可选）

Makaron 只出画面，音乐用 ffmpeg 后期合成：
```bash
ffmpeg -i video.mp4 -i music.mp3 -c:v copy -shortest output.mp4
```

## Rules

1. 三视图 → 脚本 → 分镜 → 用户确认 → 渲染，不跳步
2. 所有表演镜头正面或侧脸，零背影零剪影
3. 口型必须在每个表演镜头可见
4. 话筒全程在手不穿帮（Shot 5 拉麦，Shot 7/8 高举）
5. 2 段观众切镜（Shot 3 + Shot 6）
6. 人物占比 60%+，场景做背景
7. 禁止旧版"闭眼/背影躲口型"策略
