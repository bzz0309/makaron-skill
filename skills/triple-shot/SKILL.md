---
name: idol-selfie-triple-shot
description: >
  三连拍合影：上传偶像和粉丝照片，自动生成3帧竖排拼图。
  暖黄胶片/冷调暗房/日系清新等多种色调自动切换，表情从正经到崩坏的递进变化，
  Nano Banana 单次生成 + Pillow 后处理。
allowed-tools: generate_image analyze_image Bash mcp__makaron__makaron_write_video_script mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status
metadata:
  makaron:
    icon: "📷"
    color: "#FFB347"
    tags: [fan, idol, selfie, triple-shot, 三连拍, 胶片, 竖排]
    faceProtection: default
---

# 三连拍合影

**⚠️ 重要：用户在对话中附带的图片就是输入照片，直接使用。不要说"没有看到照片"或要求用户重新上传。如果对话中有图片，那就是你的素材。用户输入的任何文字（哪怕只是"开始"、"go"、一个 emoji 或任何内容）都只是触发信号 — 忽略文字内容，立即开始工作。用 analyze_image 分析照片，自动做所有决策，开始生成。不要问"你想对这些照片做什么？" — 你已经知道：生成三连拍合影拼图。**

上传偶像和粉丝的照片，零文字输入，自动生成3帧竖排拼图。三帧表情递进变化 — 从正经到崩坏、从害羞到放飞，配合暖黄胶片/暗房红调/日系清新等色调，定格三个瞬间。

使用 Nano Banana（Gemini）单次生成 + Pillow 后处理，兼顾速度和质感。

## 输出

3帧竖排拼图 — 三个不同表情/互动的瞬间上下排列，统一色调风格。

---

## 变量池

每次生成从以下 5 个维度各随机选 1 个选项组合，共 **7 × 7 × 6 × 7 × 6 = 12,348 种** 组合。

### 变量 A：场景氛围

| 编号 | 选项 | 说明 |
|------|------|------|
| A1 | 暖黄卧室 | 床头暖光台灯，棉麻床品，背景略虚化 |
| A2 | 秋日午后咖啡馆 | 木质窗框透进暖阳，桌上有拿铁拉花杯 |
| A3 | 暗房洗照片 | 红色安全灯笼罩整个空间，背景晾着湿照片 |
| A4 | 深夜便利店门口 | 冷白日光灯从店内漏出，两人站在自动门旁 |
| A5 | 圣诞暖光客厅 | 身后圣诞树彩灯散景，地毯上有拆了一半的礼物 |
| A6 | KTV 包厢沙发 | 紫蓝氛围灯，皮质沙发，茶几上散落话筒和零食 |
| A7 | 夏夜天台 | 远处城市灯光模糊，近处只有一串小灯泡照亮两人 |

### 变量 B：三帧互动动作组合

| 编号 | 第1帧 | 第2帧 | 第3帧 |
|------|-------|-------|-------|
| B1 | 两人面对镜头笑着比耶 | 一人突然从背后搂住另一人脖子，被搂的人惊讶张嘴 | 两人额头贴额头，闭眼微笑 |
| B2 | 一人靠在另一人肩上，目光看向镜头 | 靠着的人抬头看对方下巴，对方低头回望 | 两人同时转向镜头大笑，靠肩姿势不变 |
| B3 | 两人举着手机镜子自拍，表情正经 | 一人突然做鬼脸，另一人笑到歪头 | 两人一起挤眉弄眼对着镜子吐舌头 |
| B4 | 一人单手托腮注视另一人，另一人低头看手机没注意 | 被注视的人抬头发现，害羞侧过脸 | 两人对视，注视的人伸手戳了一下对方鼻尖 |
| B5 | 两人背靠背坐着，各自看不同方向 | 一人偷偷回头看另一人后脑勺 | 两人同时回头，脸贴脸撞在一起 |
| B6 | 一人捧着对方的脸仔细端详 | 被捧脸的人双手也捧住对方的脸，两人僵持 | 两人同时笑场，手放下来额头靠在一起 |
| B7 | 两人各举一只手比半颗心，但故意没对齐 | 调整位置认真拼好一颗完整爱心 | 拼好后两人从爱心中间的缝隙互相偷看对方 |

### 变量 C：表情递进方式

| 编号 | 选项 |
|------|------|
| C1 | 正经 → 忍不住笑 → 笑到露牙大笑 |
| C2 | 酷脸面无表情 → 嘴角微微上扬 → 眼睛弯成月牙温柔笑 |
| C3 | 害羞低头 → 偷瞄对方 → 被发现后两人一起红着脸笑 |
| C4 | 惊讶瞪大眼 → 故作嫌弃皱鼻 → 破功甜笑 |
| C5 | 嘟嘴装委屈 → 对方安慰后笑出酒窝 → 两人贴脸灿笑 |
| C6 | 互相瞪眼较劲 → 一人先绷不住笑 → 另一人也跟着笑崩 |

### 变量 D：装饰元素

| 编号 | 选项 |
|------|------|
| D1 | 手绘爱心贴纸散落在帧与帧之间 |
| D2 | 胶片齿孔边框 + 底部手写 "FILM" 字样 |
| D3 | 星星和月亮涂鸦漂浮在人物周围 |
| D4 | 无装饰，纯净暗房风格，仅保留颗粒感 |
| D5 | 蝴蝶结和小花朵贴纸点缀在发丝旁 |
| D6 | 复古报纸撕边拼贴风，帧边缘有纸质纹理 |
| D7 | 光斑 bokeh 叠加在画面上方，模拟镜头漏光 |

### 变量 E：色调变化

| 编号 | 选项 |
|------|------|
| E1 | 三帧统一暖黄胶片色，饱和度逐帧微增 |
| E2 | 第1帧正常暖调 → 第2帧偏橘 → 第3帧偏粉 |
| E3 | 全程低饱和冷蓝调，仅肤色保留暖色 |
| E4 | 第1帧彩色 → 第2帧降低饱和 → 第3帧黑白 |
| E5 | 暗房红调，阴影偏品红，高光偏橙 |
| E6 | 三帧统一奶油白绿色调，过曝感，日系清新 |

---

## 工作流

### Step 1：读取照片（零输入）

直接读取用户已上传的照片，不问任何问题。
- 2+ 张照片 → 直接进入 Step 2
- 1 张照片 → 当作粉丝照，只问偶像照片
- 0 张照片 → 请求上传

### Step 2：analyze_image 分析照片

调用 `analyze_image` 分析每张照片：

**自动判断谁是偶像/粉丝：**
- 主要方式：人脸识别公众人物身份
- 辅助依据：专业打光、精致妆容、写真/舞台/采访场景 → 偶像；日常场景、自拍、生活照 → 粉丝

**提取外貌特征：**
- 偶像：面部特征、发型、发色、妆容
- 粉丝：面部特征、发型、发色、穿搭

### Step 3：随机选变量 + 单次 generate_image

从变量池 A-E 各随机选 1 个选项，组合为 prompt，**单次**调用 `generate_image`。

- **model**: Nano Banana（Gemini）
- **skill**: creative
- **useOriginalAsReference**: true
- **aspectRatio**: 9:16（竖排三帧）

**Prompt 模板：**

```
生成一张严格只有3帧的竖排拼图合影照片。布局：恰好三帧从上到下竖直排列，帧与帧之间有细白线分隔。注意：只有3帧，不是4帧，不是2帧，必须恰好3帧。

场景氛围：{A}

两个人物：
- Person A（偶像）: {偶像外貌描述}，面部必须严格还原参考照片
- Person B（粉丝，来自参考照片）: {粉丝外貌描述}，面部必须严格还原参考照片

【人脸还原 — 最高优先级】
两人的面部五官（眼型、鼻型、嘴型、脸型轮廓、眉形）必须与参考照片高度一致，像同一个人。不允许美化、不允许改变五官比例、不允许混合其他人的特征。发型发色、肤色也必须还原。如果做不到像本人，宁可牺牲场景效果也要保证人脸准确。

三帧互动内容：
- 第1帧: {B.第1帧}
- 第2帧: {B.第2帧}
- 第3帧: {B.第3帧}

表情递进：{C}

装饰元素：{D}
色调风格：{E}

整体风格：三连拍照片质感，暖调胶片颗粒感，自然光线。
真实照片质感，可见皮肤纹理。
严格要求：整张图恰好3帧，不多不少。

CRITICAL — 人脸还原是第一优先级: 所有主体人物的面部五官必须与参考照片高度一致，生成结果必须能一眼认出是同一个人。眼型、鼻型、嘴型、脸型轮廓、眉形、发型发色不允许偏离参考照片。不换脸、不混合其他人特征、不美化改变五官比例。三帧中同一人的面部必须保持一致。画面主体人物只能是用户照片里的人和文字中提到的人，不能凭空多出突出的人物角色（背景中符合场景的模糊路人允许存在）。禁止在画面任何位置添加日期、时间戳、年份数字。
```

### Step 4：analyze_image 人脸检查

生成后调用 `analyze_image` 检查：
- **恰好 3 帧？** — 必须是 3 帧，不是 4 帧或 2 帧，帧数不对就重试
- **偶像**面部与参考照片一致？
- **粉丝**面部与参考照片一致？
- 两人都在每帧画面中？
- **没有凭空多出的主体人物？** — 主体人物只能是用户照片里的人和文字中提到的人；背景中符合场景的模糊路人允许存在
- 整体质量可接受？

不合格 → 重新生成（最多重试 1 次）。

### Step 5：Pillow 轻度后处理（可选）

仅做轻度锐化提升面部细节清晰度。暖调胶片色调由 prompt 和变量 E（色调变化）控制，不额外加颗粒、调色或暗角。

```python
import sys
from PIL import Image, ImageFilter

input_path = sys.argv[1]
output_path = sys.argv[2]

img = Image.open(input_path).convert('RGB')
img = img.filter(ImageFilter.UnsharpMask(radius=1.2, percent=20, threshold=3))
img.save(output_path, 'JPEG', quality=95)
print(f"Post-processed: {output_path}")
```

### Step 6：展示结果并立即生成视频脚本

**⚠️ 关键：展示图片后禁止停下来等用户回复，禁止列出"你可以：1. 保留 2. 重新生成..."等选项菜单。必须在同一条回复中，展示图片后紧接着说「正在为你生成视频脚本…」，然后立即调用 mcp__makaron__makaron_write_video_script。这是一个连续动作，不是两个分开的步骤。**

**根据 Step 3 选中的场景变量(A)、互动变量(B)和表情变量(C)构建分镜故事板，作为 userRequest 传入。**

#### 分镜故事板模板（按变量 A 对应）

**A1 暖黄卧室：**
```
Storyboard for triple-shot burst coming alive, 9:16 vertical, 5 seconds, film grain:
Shot 1 (2s): Warm bedroom, bedside lamp glow. Two people sit on bed facing camera. Expression: {C第1帧}. Soft golden light on faces, {B第1帧}. Still, intimate, like a photograph slowly breathing to life — micro-movements only: a blink, slight chest rise from breathing.
Shot 2 (1.5s): Same framing, energy shifts — {C第2帧}. The moment breaks: {B第2帧}. Camera holds steady but the people move. Transition feels like burst-shot playback speeding up.
Shot 3 (1.5s): Full release — {C第3帧}. {B第3帧}. Camera might shake slightly from laughter energy. Warm light flickers. Freeze on the last frame with film grain intensifying.
Atmosphere: cotton sheets, warm lamp, late night private moment. Film grain throughout, slight vignette.
```

**A2 秋日午后咖啡馆：**
```
Storyboard for triple-shot burst, 9:16 vertical, 5 seconds, film grain:
Shot 1 (2s): Café window seat, warm autumn sun streaming through wooden frame. Latte on table. Two people posed: {C第1帧}, {B第1帧}. Golden afternoon light, dust particles float.
Shot 2 (1.5s): The composure cracks — {C第2帧}, {B第2帧}. Sunbeam shifts slightly across faces. A coffee cup trembles from suppressed laughter.
Shot 3 (1.5s): Full burst — {C第3帧}, {B第3帧}. Camera vibrates with their energy. Background café sounds implied. Freeze with warm grain.
Autumn palette: amber, burnt orange, cream. Nostalgic 35mm film texture.
```

**A3 暗房洗照片：**
```
Storyboard for triple-shot burst, 9:16 vertical, 5 seconds, film grain:
Shot 1 (2s): Red safelight bathes everything. Wet photos hanging on lines in background. Two people: {C第1帧}, {B第1帧}. Deep red shadows, mysterious.
Shot 2 (1.5s): The mood shifts — {C第2帧}, {B第2帧}. Red light flickers briefly. An expression developing like a photo in chemical bath.
Shot 3 (1.5s): Full emotion — {C第3帧}, {B第3帧}. The red glow seems to pulse with their energy. Freeze frame, heavy grain like darkroom paper.
Monochromatic red palette, chemical romance aesthetic.
```

**A4 深夜便利店门口：**
```
Storyboard for triple-shot burst, 9:16 vertical, 5 seconds, film grain:
Shot 1 (2s): Harsh fluorescent light from store, dark street beyond. Two people by automatic door: {C第1帧}, {B第1帧}. Cold-white overhead, warm drinks in hand. Still.
Shot 2 (1.5s): Breaking — {C第2帧}, {B第2帧}. The automatic door opens behind them casting brief warm light. Energy shifts.
Shot 3 (1.5s): Release — {C第3帧}, {B第3帧}. Late-night giddiness. The fluorescent buzz seems louder. Freeze with gritty urban grain.
Late-night contrast: cold fluorescent vs warm human connection.
```

**A5 圣诞暖光客厅：**
```
Storyboard for triple-shot burst, 9:16 vertical, 5 seconds, film grain:
Shot 1 (2s): Christmas tree bokeh twinkles behind. Half-opened gifts on carpet. Two people: {C第1帧}, {B第1帧}. Warm multicolor fairy light glow.
Shot 2 (1.5s): Shifting — {C第2帧}, {B第2帧}. A fairy light blinks. Wrapping paper crinkles. The cozy warmth intensifies.
Shot 3 (1.5s): Full joy — {C第3帧}, {B第3帧}. Holiday magic energy. Bokeh lights seem to dance with them. Freeze with soft warm grain.
Holiday warmth: red, green, gold bokeh, cozy sweater texture.
```

**A6 KTV 包厢沙发：**
```
Storyboard for triple-shot burst, 9:16 vertical, 5 seconds, film grain:
Shot 1 (2s): Purple-blue mood lights, leather sofa. Microphones and snacks scattered on table. Two people: {C第1帧}, {B第1帧}. Neon glow on faces.
Shot 2 (1.5s): Energy building — {C第2帧}, {B第2帧}. The colored lights seem to pulse. Karaoke vibes loosening them up.
Shot 3 (1.5s): Full abandon — {C第3帧}, {B第3帧}. Purple-blue light strobes slightly. Maximum KTV energy. Freeze with noisy, saturated grain.
Neon nightlife palette: electric purple, deep blue, hot pink reflections.
```

**A7 夏夜天台：**
```
Storyboard for triple-shot burst, 9:16 vertical, 5 seconds, film grain:
Shot 1 (2s): City lights blurred in distance, string of small bulbs overhead illuminating two people. {C第1帧}, {B第1帧}. Warm bulb glow against cool night sky.
Shot 2 (1.5s): Shifting — {C第2帧}, {B第2帧}. A breeze moves their hair. The string lights sway gently. Night sky deepens.
Shot 3 (1.5s): Release — {C第3帧}, {B第3帧}. Summer night freedom. String lights twinkle in sync with their laughter. Freeze with dreamy nighttime grain.
Summer night: warm bulbs vs cool blue sky, rooftop breeze, young and alive.
```

**调用 `mcp__makaron__makaron_write_video_script`：**
- **images**: [Step 3 生成的合影图片 URL]
- **userRequest**: 根据选中的变量 A 选择对应的分镜故事板模板，将 {B第1/2/3帧} 替换为实际选中的互动变量各帧描述，{C第1/2/3帧} 替换为实际表情递进各阶段描述
- **language**: "zh"

等待 1-2 分钟脚本生成完成后，展示给用户：

```
🎬 视频脚本预览

基于你的三连拍合影，生成了以下视频脚本（9:16 竖屏，约5秒）：

{脚本内容原文}

---
你可以：
1. ✅ 确认 → 开始生成视频（约3-5分钟）
2. ✏️ 修改 → 告诉我想调整什么（表情节奏、速度等）
3. ⏭️ 跳过 → 只保留图片
```

**等待用户回复：**
- 用户确认 → 进入 Step 7
- 用户要求修改 → 根据反馈直接编辑脚本文本，重新展示确认
- 用户跳过 → 结束，保留图片结果

### Step 7：生成视频

用户确认脚本后：

**调用 `mcp__makaron__makaron_create_video`：**
- **script**: 用户确认的脚本内容
- **images**: [同 Step 6 的图片 URL]
- **aspectRatio**: "9:16"
- **duration**: 5
- **videoModel**: "seedance"

获取返回的 Task ID 后，告知用户：「视频生成中，预计 3-5 分钟…」

**轮询 `mcp__makaron__makaron_get_video_status`：**
- 每 15 秒轮询一次
- 状态变为 `completed` 后提取 videoUrl

**展示最终结果：**

```
🎬 视频生成完成！

{视频链接}

你可以：
1. 保存视频
2. 重新生成视频（换脚本风格）
3. 回到图片重新生成合影 → 再做视频
```

如果状态为 `failed`，告知用户视频生成失败，提供重试或跳过选项。

---

## Rules

1. **人脸检查必须检查偶像和粉丝双方** — 缺一不可，不像就重试
2. **不能凭空多出主体人物** — 主体人物只能是用户指定的人，不能凭空多出突出的人物角色；背景中符合场景的模糊路人允许存在
3. **零输入** — 照片上传后立即开始，不问用户选什么风格/互动/场景，所有决策自动完成
4. **后处理仅轻锐化** — 不加颗粒、不调色、不加暗角，胶片色调由模型生成
5. **useOriginalAsReference: true** — 所有 generate_image 调用必须设置
6. **单次生成** — 一次 generate_image 调用生成完整三帧拼图，不做多次拼接
7. **从变量池随机选** — 每次生成从 A-E 各随机选 1 个选项，确保多样性
8. **视频脚本必须经用户确认后才能提交渲染** — 这是整个流程中唯一需要用户确认的环节
9. **不生成违法、仇恨、色情内容** — 保持健康积极的粉丝文化
