---
name: map-tap-transition
description: >
  Upload full-body photo(s) + destinations → generate a map-tap transition
  video. Overhead shot of a finger tapping a map location → zoom-in → person
  appears at that destination in matching outfit. Tap next spot → zoom → next
  destination. Repeat for a dreamy travel montage.
allowed-tools: generate_image analyze_image generate_animation Bash
metadata:
  makaron:
    icon: "📍"
    color: "#E74C3C"
    tags: [travel, transition, video, map, fashion, vlog, creative]
    tipsEnabled: true
    tipsCount: 4
    faceProtection: strict
    defaultAspectRatio: "9:16"
    modelPreference: [openai]
---

# Map Tap Transition — 地图手指点击转场

**⚠️ 重要：用户在对话中附带的图片就是输入照片，直接使用。不要说"没有看到照片"或要求用户重新上传。**

生成一个「地图点击转场」短视频：俯拍手指点在地图上某个位置 → 画面 zoom in 放大涟漪效果 → 人物全身出现在该目的地场景中 → 画面 zoom out 回到地图 → 手指点下一个位置 → 重复。像在地图上"传送"一样旅行。

This skill uses **model: openai** for consistent face/body preservation and text rendering on map elements.

## Core Concept

**视频结构：**
1. **俯拍地图**：一张手绘/复古地图平铺桌面，手指从画面外伸入
2. **点击**：手指按在某个城市标记点上，产生涟漪/发光效果
3. **Zoom in**：画面从地图上该点快速放大 → 过渡到实景
4. **到达**：人物全身照出现在目的地场景中，摆 pose
5. **Zoom out**：画面缩回地图视角
6. **重复**：手指移动到下一个点 → 点击 → zoom → 到达

**视觉关键**：地图是"上帝视角"的叙事线索，每次手指点击 = "传送"到那里

## Input Modes

### Mode A: 单张照片（AI 全自动）
- 用户上传 1 张全身照
- AI 自动生成每个目的地的穿搭 + 场景
- 合成地图转场视频

### Mode B: 多张照片（AI 换背景）
- 用户上传多张不同穿搭的全身照
- AI 保留穿搭，只换背景为对应目的地
- 合成地图转场视频

### Input Requirements
**必须：**
1. 全身照（至少1张）

**可选：**
2. 目的地列表（如 "东京、巴黎、巴厘岛"）
3. 地图风格偏好（复古/水彩/简约）
4. 穿搭偏好

**判断输入模式：**
- 1张照片 → Mode A
- 2+张照片 → Mode B
- 无目的地 → AI 自动选 3-4 个风格反差大的热门目的地

## Workflow

### Step 1: Analyze Input

调用 `analyze_image` 分析照片：
- 人物特征：面部、身材、发型
- 当前穿搭细节
- 如果多张：记录每张的穿搭差异

### Step 2: Plan Video Sequence

**视频时间轴（9:16 竖版，20-30秒）：**

| 段落 | 时长 | 内容 |
|------|------|------|
| 开场地图 | 2s | 俯拍桌面地图全景，手指进入画面 |
| 点击 #1 | 1s | 手指点在目的地1，涟漪发光 |
| Zoom + 到达 #1 | 3s | 画面放大过渡 → 人物在目的地1 |
| 回到地图 | 1s | 画面缩回地图俯拍 |
| 点击 #2 | 1s | 手指移到目的地2，点击 |
| Zoom + 到达 #2 | 3s | 放大 → 人物在目的地2 |
| 回到地图 | 1s | 缩回 |
| 点击 #3 | 1s | 手指点目的地3 |
| Zoom + 到达 #3 | 3s | 放大 → 人物在目的地3 |
| 结尾 | 2-3s | 缩回地图全景，所有点亮点闪烁，地图折起 |

### Step 3: Generate Map Frames

**地图基础帧（俯拍视角）：**

```
editPrompt for map overhead shot:

A top-down overhead photograph of a beautiful {map_style} map spread on a wooden desk/table.

MAP STYLE: {style_description}
The map shows {geographic_region} with these locations clearly marked:
{for each destination:}
- {city_name}: marked with a {marker_style} pin/dot at the correct geographic position

MAP DETAILS:
- The map fills about 80% of the frame
- Slightly wrinkled/folded edges for authenticity
- Surrounding props: a coffee cup corner visible, maybe a pen, a passport edge
- Warm ambient lighting from above (like a desk lamp)

HAND: A clean, well-manicured hand/finger entering from the bottom of the frame, index finger extended, pointing at / about to tap {current_destination} marker.

The {current_destination} marker has a subtle glow/ripple effect emanating from it — like a GPS pulse or a droplet hitting water — indicating it's being "selected".

FRAMING: 9:16 vertical, bird's eye view (camera directly above looking down).
LIGHTING: Warm desk lamp lighting, slight shadow from the hand.
STYLE: Cozy, editorial, travel-planning aesthetic.
```

**地图风格选项（根据目的地区域自动选择）：**

| Style | Description | Best for |
|-------|-------------|----------|
| 复古航海 | 羊皮纸质感，棕褐色调，手绘海岸线 | 欧洲、环球旅行 |
| 水彩插画 | 彩色水彩渲染，鲜艳活泼 | 热带、东南亚 |
| 极简现代 | 白底黑线，几何化，设计感 | 城市游、日韩 |
| 牛皮纸手绘 | kraft纸底色，铅笔手绘线条 | 文艺范、探险风 |

### Step 4: Generate Destination Frames

**人物在目的地的帧（正常视角）：**

Mode A (AI 生成穿搭):
```
editPrompt for destination frame:

A full-body fashion photo of the same person from the reference photo, standing at {destination_scene}.

PERSON: Exact same face, body, hair as reference. Wearing {destination_outfit}: {outfit_details}.

BACKGROUND: {destination} — {specific_scene_description}. The location is immediately recognizable. Natural lighting matching the scene. Some depth of field — person sharp, background slightly soft.

POSE: Confident travel-blogger pose — {pose_description}. Relaxed, natural, like they just "arrived" and are taking it all in. Full body visible head to toe.

FRAMING: 9:16 vertical, full body centered.
STYLE: Travel vlog / fashion editorial hybrid. Vibrant, aspirational, real.

CRITICAL: Face identical to reference photo. Full body visible. Location must be instantly identifiable as {destination}.
```

Mode B (保留穿搭换背景):
```
editPrompt for background swap:

Keep the person and their complete outfit EXACTLY as shown in reference photo {n}. Replace ONLY the background with {destination_scene}.

PRESERVE: face, body, outfit, pose, accessories, shoes — everything about the person unchanged.
CHANGE: background only → {destination_specific_scene_description}.

Adjust lighting on the person to match the new environment naturally. Ground contact must look real.
FRAMING: 9:16, same framing as original.
```

### Step 5: Generate Transition Frames

**Zoom-in 过渡帧（地图 → 实景）：**

```
editPrompt for zoom transition frame:

A creative transition frame — the image is MID-ZOOM between a map view and a real scene.

The top portion of the image still shows traces of the map texture ({map_style} paper, illustrated lines, marker dots). The bottom/center is transitioning into a real photographic scene of {destination}.

It looks like the camera is "diving into" the map — the map elements are stretching/blurring outward while the real scene materializes in the center.

A subtle radial blur / motion blur effect emanates from the center point (where the finger tapped).

COLOR: The map's color palette ({warm/cool/vintage}) blends into the real scene's colors.

FRAMING: 9:16, full frame transition effect.
```

### Step 6: Assemble Video

Use `generate_animation` for each segment, then combine:

**Motion specs per segment:**
- **Map overhead**: very slow drift / slight hand movement approaching the pin
- **Tap moment**: quick pulse/ripple on the marker (0.5s)
- **Zoom transition**: fast zoom-in effect (0.5-1s) — camera dives into the map point
- **Destination scene**: subtle camera drift or slow push-in (2-3s) — person is still, scene alive
- **Zoom out**: reverse zoom back to map (0.5-1s)

**Video assembly:**
- 9:16 vertical
- 20-30 seconds total
- 30fps
- Transitions: zoom-in/out effects (NOT hard cuts — this skill uses spatial zoom transitions)
- Music: upbeat travel vibe, each "arrival" syncs with a beat hit

### Step 7: Present Result

Show completed video. User can:
1. Keep as-is
2. Change a destination
3. Change map style
4. Swap outfit for a specific destination
5. Adjust timing
6. Change number of destinations (add/remove stops)

## Destination + Outfit + Pose Combos

| Destination | Outfit | Scene | Pose |
|-------------|--------|-------|------|
| Tokyo | 白T+阔腿裤+帆布包+运动鞋 | 涩谷十字路口/浅草寺雷门 | 单手比V，回头看镜头 |
| Paris | 碎花midi裙+贝雷帽+法棍 | 埃菲尔铁塔草坪/塞纳河桥 | 单手扶帽，侧身回眸 |
| Bali | 白色吊带裙+草帽+编织包 | 海神庙/无边泳池 | 双手张开，迎风感 |
| New York | 皮夹克+牛仔裤+马丁靴 | 时代广场/布鲁克林桥 | 走路中回头，酷飒 |
| Seoul | Oversized blazer+短裙+乐福鞋 | 北村韩屋/弘大壁画街 | 单手撩发，自信直视 |
| London | 风衣+围巾+切尔西靴 | 大本钟/红色电话亭 | 撑伞/拎包，优雅走路 |
| Santorini | 蓝白条纹衫+白裤+凉鞋 | 蓝顶教堂/白色阶梯 | 倚靠白墙，侧面放松 |
| Morocco | 长裙+流苏耳环+编织鞋 | 蓝色小镇/彩色市集 | 触摸墙面/布料，探索感 |

## Tips Directions

1. 亚洲三城: 地图上依次点击东京→首尔→曼谷，每站不同穿搭风格，从日系到韩系到度假风。
2. 欧洲环游: 手指在欧洲地图上点巴黎→伦敦→罗马，碎花裙→风衣→亚麻套装，优雅切换。
3. 只传1张照片: 上传一张全身照，AI自动匹配4个目的地+4套穿搭+完整地图转场视频。
4. 复古地图风: 使用羊皮纸航海地图风格，搭配暖色调目的地场景，整体复古旅行电影感。

## Core Rules

### Face Consistency
- 每一帧人物出现时面部必须与参考照片一致
- useOriginalAsReference: true
- 生成后 analyze_image 验证

### Zoom Transition 是核心美学
- 不是硬切！是空间缩放过渡（地图点 → zoom in → 实景）
- 每次"到达"目的地的感觉是"镜头从地图上钻进去了"
- zoom out 回地图的感觉是"镜头抽回上帝视角"
- 这个 zoom 效果是区别于 flight-transition 的关键差异

### 地图必须地理正确
- 标记的城市相对位置大致正确
- 手指移动轨迹 = 旅行路线顺序
- 地图风格统一全片（不要中途换地图）

### 目的地场景必须可识别
- 每个到达帧的背景必须一眼认出是哪里
- 选择最标志性的地标/场景
- 不要用通用的"城市街道"或"海滩" — 要有辨识度

### What to NEVER Do
- Never use hard cuts between map and destination (must zoom)
- Never show a map with wrong geographic positions
- Never lose full body in destination shots
- Never reuse the same pose across all destinations — each stop should feel like a different moment
- Never make the hand/finger look unnatural or AI-generated — it should look like a real person's hand
- Never use a plain/boring map — the map itself should be visually beautiful
