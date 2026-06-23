---
name: kpop-stage
description: >
  韩国打歌舞台：模拟Inkigayo/Music Bank/M Countdown等韩国音乐节目打歌直播，
  支持横屏全景和9:16竖屏直拍两种模式。包含电视台舞美系统、编队舞蹈、Ending Fairy定格。
  K-pop music show broadcast stage with Korean TV production system,
  supports both 16:9 full stage and 9:16 vertical fancam modes.
allowed-tools: analyze_image Bash mcp__makaron__makaron_edit_image mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status
metadata:
  makaron:
    icon: "🎤"
    color: "#FF6B9D"
    tags: [kpop, music-show, broadcast, inkigayo, ending-fairy, choreography, idol, stage, fancam]
    defaultAspectRatio: "9:16"
    videoModel: seedance
---

# 韩国打歌舞台 — K-pop Music Show Stage

**⚠️ 重要：用户在对话中附带的图片就是面孔/角色参考，直接使用。不要要求用户重新上传。**

生成一段**韩国音乐节目打歌舞台视频**：模拟 Inkigayo / Music Bank / M Countdown 等韩国电视台打歌直播的视觉体验，包含电视台级舞美系统、C位+伴舞编队、多机位广播镜头语言，以及 Ending Fairy 定格结尾。后期叠加直播UI overlay。

## 输入类型

- **图片**：面孔/角色参考图（用于锁定人物外貌）
- **文字描述**：风格偏好（制服风/甜酷/嘻哈/优雅/暗黑酷飒等）、歌曲氛围

## 核心能力

1. **C位角色身份板**：基于参考图 + 指定风格，生成16:9角色身份板（多角度一致性验证）
2. **伴舞参考图**：3名伴舞并排展示，各自不同发型/体型/面孔，统一服装
3. **舞台场景设定图**：确定LED背景内容、灯光配色、地板质感、整体布景风格
4. **12宫格分镜故事板**：基于以上三张参考图，黑白铅笔手绘风
5. **Seedance视频生成**：同时喂入故事板+角色板+伴舞图+舞台图，生成15秒视频
6. **直播UI overlay**：生成韩国音乐节目风格的电视直播UI叠加层

## 六步工作流

### Step 1: C位角色身份板

用 openai 模型生成 16:9 角色身份板：
- 纯白背景，非对称编辑布局
- 一个大型全身锚点 + 多角度辅助视图 + 表情研究 + 剪影研究
- 角色ID文本块（名称/角色/核心情绪/视觉标志）
- **面孔必须锁定参考图**
- 根据角色身份板确定的风格，自动适配匹配的动作词库和舞台配色

→ 展示给用户确认

### Step 2: 伴舞参考图

用 openai 模型生成 16:9 伴舞设定图：
- 3名伴舞并排站立，全身展示
- 服装统一，与C位同风格但更简约（突出C位）
- **每人必须有明显不同**：不同发型（短发/马尾/双马尾等）、不同体型、不同面部特征
- 纯白背景，清晰展示每人差异
- 可加文字标注区分：Dancer A / B / C

→ 展示给用户确认

### Step 3: 舞台场景设定图

用 openai 模型生成 16:9 舞台效果图：
- 韩国电视台打歌舞台全景（无人物，纯场景）
- 包含：LED屏幕内容/配色、灯光设计、地板材质、舞台层次结构
- 匹配角色风格的整体色调和氛围
- 参考真实 Inkigayo/Music Bank/M Countdown 的舞美设计

→ 展示给用户确认

### Step 4: 12宫格分镜故事板

用 openai 模型生成黑白铅笔分镜（参考 Step 1-3 确认的角色/伴舞/舞台）：
- C位 + 3名伴舞（严格3名，不多不少）
- 编队走位变化：V字形/菱形/一字排开/散开/星形
- 颜色标注系统：红色=身体运动，蓝色=摄影机，绿色=构图，橙色=灯光，紫色=情感
- 最后一格必须是 Ending Fairy 定格

→ 展示给用户确认

### Step 5: Seedance 视频 prompt

**核心原则：决定"像不像KPOP打歌"的是「韩国电视台舞美系统」，不是 idol/kpop/girl group**

**多图输入**：makaron-cli 同时传入4张参考图
```bash
npx makaron-cli chat --project {id} \
  --media "storyboard.jpg" \
  --media "character_board.jpg" \
  --media "dancers_ref.jpg" \
  --media "stage_ref.jpg" \
  --wait-video "prompt..."
```

prompt 中引用：`<<<media_1>>>` 故事板 / `<<<media_2>>>` 角色板 / `<<<media_3>>>` 伴舞 / `<<<media_4>>>` 舞台

#### 必用关键词体系

| 类别 | 关键词（必须用） | 禁用词 |
|------|-----------------|--------|
| 电视台舞美 | Korean music show broadcast stage, South Korean live broadcast, Inkigayo/Music Bank style | concert stage |
| 舞台结构 | massive layered LED screens, dynamic LED graphics, stage risers, multi-layer platform | simple stage |
| 地面 | reflective glossy black mirror floor, polished stage floor | — |
| 摄影机 | broadcast camera shot, live TV camera framing, idol fancam style, ending fairy close-up | — |
| 灯光 | synchronized stage lighting, color changing beam lights, idol spotlight, volumetric stage light, backlight haze | concert lighting |
| 背景 | animated LED background, kinetic LED visuals, high budget korean stage production | — |

#### 视频 prompt 结构

```
Use storyboard <<<media_1>>> as the complete visual and emotional narrative source for a 15-second video. Character reference <<<media_2>>> for center idol identity. Backup dancers reference <<<media_3>>> for dancer appearances. Stage design reference <<<media_4>>> for environment.

Scene: ultra realistic South Korean music show broadcast stage, [节目] style stage design, massive layered LED screens with animated kinetic visuals in [配色] palette, reflective glossy black mirror floor with dancer reflections, synchronized colorful beam lights, volumetric spotlight haze, multi-layer stage platform, broadcast studio lighting, live TV performance atmosphere, high budget Korean music program stage production, dynamic LED graphics, immersive stage environment.

Characters: Center idol — [外貌描述], headset mic, Korean beauty makeup, highly detailed face, realistic skin texture. 3 backup dancers as shown in dancer reference, each with distinctly different appearance. Dancers must NOT have identical faces.

0-3s: broadcast camera [运镜], [编队] formation [舞蹈动作], massive LED wall [背景视觉], beam lights, volumetric haze. Center [表情].
3-6s: camera [运镜], [编队变化] [舞蹈], LED background [变化], idol spotlight, broadcast studio lighting. Center [表情].
6-9s: camera [运镜], [C位solo动作], synchronized beam lights, dancers [走位]. Center [表情].
9-12s: [运镜], [高能动作], LED visuals intensify, color changing beam lights sweep. Center [表情]. High energy peak.
12-15s: ending fairy close-up freeze — broadcast camera dramatic push-in to center face extreme close-up, [ending表情] looking directly at camera, hold 1 second freeze.
```

→ 展示 prompt 给用户确认后再提交生成

#### 全程表情管理

- 群舞/力量段：专注认真、微微咬唇的集中感
- 被镜头捕捉瞬间：不经意的自然微笑、眼神接触
- 高能/甩发段：沉浸享受、嘴角微扬
- 转场/走位段：自信从容、轻微挑眉
- Ending Fairy：定格看镜头（甜笑/wink/轻呼吸感/回眸）
- 表情要自然不油腻

### Step 6: UI Overlay 后处理

用 openai 模型生成黑底16:9 overlay 图，包含：
- 左上角：韩国音乐节目 logo（pastel gradient，cute Korean typography）
- 右上角：LIVE 标记（soft coral/red）
- 中间完全黑色（用于 blend=screen 叠加后变透明）

ffmpeg 合成命令：
```bash
ffmpeg -y -i video.mp4 -i overlay.png -filter_complex "[0:v][1:v]overlay=0:0" -c:a copy final.mp4
```

## 推荐模式：9:16 竖屏直拍（Fancam）

基于实战验证，**竖屏直拍是最佳效果方案**：
- Seedance 单人聚焦效果远优于多人群舞
- 避免多人面孔克隆问题（Seedance 无法区分多人面孔）
- 主角占满画面，面孔一致性最佳
- 伴舞只在画面边缘偶尔露出手臂/身体局部

### 竖屏直拍工作流（推荐）

1. **角色身份板**（16:9，openai模型）— 确定面孔+服装+风格
2. **舞台场景图**（16:9，openai模型）— 确定LED/灯光/地板
3. **Seedance 9:16 视频** — 只传入角色板+舞台图，prompt聚焦单人
4. **无需额外 overlay** — Seedance 会自动在LED背景上渲染文字/logo，天然充当台标

### 竖屏直拍 prompt 模板

```
Use character identity <<<media_1>>> for center idol face and costume. Stage reference <<<media_2>>> for environment lighting.

Style: 9:16 vertical Korean music show FANCAM — camera tightly framed on center idol, she fills the entire vertical frame. Occasionally other dancers arms or shoulders visible at frame edges but camera never leaves center idol.

Scene: South Korean music show broadcast stage, [节目] style, massive LED screens with [配色] animated graphics, reflective glossy floor, [灯光色] beam lights, volumetric haze, multi-layer platform.

CENTER IDOL (fills entire frame): [外貌描述], headset mic, [妆容]. Highly detailed face, realistic skin texture.

0-3s: medium shot center idol facing camera, [动作], [LED效果], beam lights. [表情].
3-6s: [动作], dancers arms briefly at frame edge. [表情].
6-9s: [高能动作], hair flying. [表情切换].
9-12s: [互动动作], steps closer to camera. High energy peak. [表情].
12-15s: ending fairy — camera very close to face, [ending表情+动作], soft bokeh background, hold 1 second freeze.
```

## 横屏全景模式（16:9）

适用于需要展示完整编队走位的场景，但注意Seedance多人效果有限。

### 横屏六步工作流

与下方原始流程相同（角色板→伴舞图→舞台图→分镜→视频→overlay）。

**伴舞服装要求**：三名伴舞必须穿**统一服装**（同款同色），通过不同体型/发型区分。

## Rules

1. **推荐竖屏直拍**：除非用户指定横屏，默认使用9:16竖屏聚焦单人
2. 伴舞人数严格3名（横屏模式），竖屏模式伴舞只在边缘出现
3. 绝不使用 "concert stage" 或 "concert lighting" — 会变成欧美演唱会风
4. 必须用具体节目名绑定训练集：inkigayo / music bank / m countdown
5. 视频 prompt 必须强调 broadcast / camera movement / live TV
6. 每个时间段都要有表情描写，表情自然不油腻
7. Ending Fairy：最后一拍必须定格看镜头 + 镜头推进大特写
8. **不需要额外 UI overlay** — Seedance LED背景自带文字效果即可作为台标
9. 保留视频音频，ffmpeg 不加 -an 参数
10. 根据角色身份板确定的风格，自动适配动作词库和舞台配色
11. 每一步生成后必须展示给用户确认，确认后再进下一步
12. 伴舞服装必须**统一**（同款式同颜色），不能混搭
