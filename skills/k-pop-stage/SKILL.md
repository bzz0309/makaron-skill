---
name: kpop-stage
description: >
  韩国打歌舞台：模拟Inkigayo/Music Bank/M Countdown等韩国音乐节目打歌直播。
  上传一张照片，全自动生成打歌舞台视频。支持9:16竖屏直拍和16:9横屏全景。
  K-pop music show broadcast with Korean TV stage production.
  Upload one photo, auto-generate fancam video. Supports 9:16 and 16:9.
allowed-tools: analyze_image Bash mcp__makaron__makaron_edit_image mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status
metadata:
  makaron:
    icon: "🎤"
    color: "#FF6B9D"
    tags: [kpop, music-show, broadcast, inkigayo, ending-fairy, idol, stage, fancam, grok]
    defaultAspectRatio: "9:16"
    videoModel: grok
---

# 韩国打歌舞台 — K-pop Music Show Stage

**⚠️ 重要：用户在对话中附带的图片就是面孔/角色参考，直接使用。不要要求用户重新上传。**

生成一段**韩国音乐节目打歌舞台视频**：上传一张照片，全自动完成 — 舞台场景生成 → Grok 视频渲染 → 直接交付。模拟 Inkigayo / Music Bank / M Countdown 等韩国电视台打歌直播的视觉体验，包含电视台级舞美系统、广播镜头语言，以及 Ending Fairy 定格结尾。

## 输入类型

- **图片**：面孔/角色参考图（用于锁定人物外貌）
- **文字描述**：风格偏好（制服风/甜酷/嘻哈/优雅/暗黑酷飒等）、歌曲氛围
- **比例**：默认 9:16 竖屏直拍，用户说"横屏"时切换为 16:9 全景

## 舞台场景变量池

每次生成从以下 4 个维度各随机选 1 个选项组合，共 **6 × 6 × 4 × 5 = 720 种** 舞台变体。

### 变量 S1：LED 配色主题

| 编号 | 选项 |
|------|------|
| S1 | 电光蓝几何 — cool white + silver + electric blue geometric crystal/diamond patterns |
| S2 | 粉紫花海 — soft pink + lavender + rose gold floral/petal animations, dreamy shoujo aesthetic |
| S3 | 金色奢华 — champagne gold + warm amber + bronze, luxury palace/golden hour feel |
| S4 | 暗红烈焰 — deep crimson + black + orange fire, intense dramatic energy, dark concept |
| S5 | 霓虹赛博 — hot pink + cyan + electric purple, retro-futuristic cyberpunk/synthwave |
| S6 | 冰雪极光 — ice white + pale blue + silver, frozen crystal/aurora borealis, ethereal winter |

### 变量 S2：灯光风格

| 编号 | 选项 |
|------|------|
| S1 | 冷蓝锐利 — cool blue beam lights, sharp white spotlights, high contrast, clean modern |
| S2 | 暖金柔和 — warm golden spotlights, soft amber wash, romantic glow, sunset vibe |
| S3 | 赛博紫粉 — magenta + cyan cross beams, neon haze, club/festival energy |
| S4 | 黑白高对比 — stark white beams on dark stage, dramatic noir shadows, minimal but powerful |
| S5 | 彩虹旋转 — multi-color rotating beam array, concert finale energy, prismatic |
| S6 | 单色沉浸 — single dominant color wash (matching LED palette), monochromatic depth, artistic |

### 变量 S3：地板类型

| 编号 | 选项 |
|------|------|
| S1 | 镜面黑 — reflective glossy black mirror floor, classic K-pop music show standard |
| S2 | 反光白 — high-gloss white reflective floor, clean bright aesthetic, Music Bank style |
| S3 | LED 网格地板 — floor embedded with LED grid panels synced to background visuals |
| S4 | 渐变镜面 — gradient-tinted mirror floor (color-matched to LED palette), premium look |

### 变量 S4：舞台结构

| 编号 | 选项 |
|------|------|
| S1 | 钻石隧道 — geometric diamond-tunnel LED archways, depth illusion, Inkigayo signature |
| S2 | 层叠台阶 — wide multi-layer illuminated white steps ascending, grand entrance feel |
| S3 | 悬浮平台 — raised central platform with LED underglow, surrounded by lower stage area |
| S4 | 环形包围 — curved LED walls wrapping around performer in semi-circle, immersive 270° |
| S5 | 极简直线 — clean horizontal LED strips and flat stage, modern minimalist, M Countdown style |

## 工作流（全自动）

**用户只需提供照片，所有步骤自动完成，中间不问任何问题。**

### Step 1：openai 出真人舞台静态图

从变量池 S1-S4 各随机选 1 个选项，用 openai 模型生成舞台场景图（默认 9:16，用户指定横屏时 16:9）：

**必须包含**：
- 角色站在舞台中央，面向镜头（面孔锁定参考图）
- 角色服装根据风格偏好自动适配（制服风/甜酷/嘻哈/优雅/暗黑酷飒等）
- 完整舞台环境：{S4} + {S1} LED + {S3} 地板 + {S2} 灯光 + volumetric haze
- Inkigayo/Music Bank 广播级制作质感
- 纯画面，无文字、无 logo、无叠加层
- 这是视频的第一帧参考，必须像真实打歌直播截图

**prompt 模板**：
```
Generate a [aspect] photorealistic K-pop stage performance still image.
Performer matches reference photo face and appearance. Standing center stage, headset mic, facing camera with confident gaze.
Stage: {S4}, massive LED screens with {S1} animated graphics, {S3}, {S2}, volumetric haze, multi-layer platform. Inkigayo/Music Bank broadcast quality.
Face MUST match reference. No text, no logos, no overlays. Single photorealistic frame.
```
其中 [aspect] = "9:16 vertical"（默认）或 "16:9 horizontal"（用户指定横屏）。

→ 生成后自动进入 Step 2，不等待用户确认

### Step 2：Grok 生成视频（默认）

将 Step 1 的舞台场景图作为参考图，喂入 Grok。

**默认使用 Grok**（仅需 1 张参考图，$0.49/条），Seedance 作为 fallback。

```bash
npx makaron-cli video create --model grok --image "stage_scene.jpg" --script "..."
```

**Seedance fallback**：Grok 失败时自动切换

**prompt 模板（[aspect] 根据 Step 1 的比例自动填入）**：
```
Reference <<<media_1>>> shows the exact look — stage environment and character appearance. THIS is the first frame. Maintain this throughout.

[aspect] Korean music show FANCAM. Camera tightly framed on center idol. South Korean live broadcast Inkigayo/Music Bank style.

Scene: same as reference — {S1} LED, {S2} lighting, {S3} floor, {S4} structure.

CENTER IDOL: same face as reference, headset mic. Highly detailed face, realistic skin texture.

0-3s: starts exactly like reference, [动作], LED, beam lights, haze. [表情].
3-6s: [动作], camera pushes in. [表情].
6-9s: [高能动作], high energy peak. [表情].
9-12s: [动作], beam lights sweep. [表情].
12-15s: ENDING FAIRY — dramatic push-in to extreme face close-up, [ending表情], direct eye contact, soft bokeh, hold 1 second freeze.

Korean music show broadcast production quality.
```
其中 [aspect] = "9:16 vertical"（默认）或 "16:9 horizontal wide shot"（横屏）。

#### 全程表情管理

- 开场：冷静自信，眼神直接对镜头
- 中段动作：专注认真、沉浸享受
- 高能段：嘴角微扬、投入忘我
- Ending Fairy：甜笑/wink/轻呼吸感/回眸，定格看镜头
- 表情要自然不油腻

→ 直接提交生成，生成完成后展示视频给用户

#### 失败处理

Grok 失败 → 自动切 Seedance。Seedance 也失败 → 通知用户。

## Rules

1. **全自动零确认**：用户给照片 → 直接出视频，中间不打断、不提问、不等确认
2. **默认 Grok**：视频模型默认 Grok，仅 Grok 失败时 fallback 到 Seedance
3. **默认竖屏 9:16**：用户说"横屏"时切换为 16:9，同一条工作流、同一个 prompt 模板
4. 绝不使用 "concert stage" 或 "concert lighting" — 会变成欧美演唱会风
5. 必须用具体节目名绑定训练集：inkigayo / music bank / m countdown
6. 视频 prompt 必须强调 broadcast / camera movement / live TV
7. 每个时间段都要有表情描写，表情自然不油腻
8. Ending Fairy：最后一拍必须定格看镜头 + 镜头推进大特写
9. **不需要额外 UI overlay** — LED背景自带文字效果即可作为台标
10. 根据角色风格，从 S1-S4 各随机选 1 个选项构成舞台
11. 禁止在 prompt 里使用任何中文字符（Grok tokenizer 对中文不友好）
12. **Grok 链路**：openai 先出真人舞台静态图 → Grok 以此图为第一帧参考生成视频。Grok 仅支持 1 张参考图
