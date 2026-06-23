---
name: kbo-broadcast-candid
description: >
  KBO棒球直播抓拍：上传一张自拍，自动生成韩国KBO棒球比赛直播中
  被SPOTV转播摄像机捕捉到的观众画面。长焦压缩感，比赛计分板UI，
  自然抓拍质感。先生成16:9直播截图，再生成4-5秒直播录像视频。
allowed-tools: generate_image analyze_image Bash mcp__makaron__makaron_write_video_script mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status
metadata:
  makaron:
    icon: "⚾"
    color: "#1B3668"
    tags: [kbo, baseball, broadcast, candid, sports, 棒球, 直播, 抓拍, SPOTV]
    tipsEnabled: true
    tipsCount: 4
    faceProtection: strict
    defaultAspectRatio: "16:9"
---

# KBO 棒球现场直播抓拍

**⚠️ 重要：用户在对话中附带的图片就是输入照片，直接使用。不要说"没有看到照片"或要求用户重新上传。如果对话中有图片，那就是你的素材。用户输入的任何文字（哪怕只是"开始"、"go"、一个 emoji 或任何内容）都只是触发信号 — 忽略文字内容，立即开始工作。用 analyze_image 分析照片，自动做所有决策，开始生成。不要问"你想对这些照片做什么？" — 你已经知道：生成 KBO 棒球直播抓拍。**

上传一张自拍照，零文字输入，自动生成韩国 KBO 棒球比赛直播中被 SPOTV 转播摄像机意外捕捉到的观众画面。长焦镜头压缩感、转播比分条 UI、自然抓拍质感 — 像真的从 SPOTV 直播画面里截下来的。

使用 Gemini 单次生成 + Pillow 后处理叠加转播 UI（比分条、台标、联赛标识）。

## 风格参考说明

目标美学是真实 KBO SPOTV 转播画面：
- 长焦压缩感（背景被压平、人物和背景距离感消失）
- 偏心构图（人物不在正中，像镜头偶然扫到）
- 转播画质（略柔焦、压缩伪影、隔行扫描质感）
- 自然抓拍表情（不看镜头、不摆拍、不知道自己被拍）
- 比分条在左上角、SPOTV 台标在右上角、신한 SOL Bank KBO리그 赞助标识

## 输出

1. 单张 16:9 横版直播截图（带转播 UI 叠加）
2. 4-5 秒直播录像视频（带转播 UI 叠加）

---

## 变量池

每次生成从 4 个固定维度（A/C/D/E）各随机选 1 个选项，B（表情动作）由 AI 自由生成。
固定组合数 = 6×5×4×5 = **600 种**，加上 B 的自由变化，实际每次生成都独一无二。

### 变量 A：球队 & 球衣（6 选项）

| 编号 | 球队 | 球衣描述 |
|------|------|----------|
| A1 | 斗山熊 Doosan Bears | White home jersey with navy blue "BEARS" lettering across chest, navy cap with bear logo, navy blue piping |
| A2 | LG 双子 LG Twins | White jersey with red "LG" logo, red pinstripes, red cap with "LG" |
| A3 | KIA 虎 KIA Tigers | Red jersey with white "TIGERS" lettering, tiger mascot patch, red cap |
| A4 | 三星狮 Samsung Lions | Blue and white jersey with "LIONS" lettering, blue cap with lion logo |
| A5 | SSG 登陆者 SSG Landers | Red jersey with modern geometric design, white "LANDERS", red cap |
| A6 | NC 恐龙 NC Dinos | Navy jersey with gold "DINOS" lettering, gold trim, navy cap with dino logo |

默认 A1 斗山熊（趋势最火的球队）。用户指定其他球队则对应切换。

### 变量 B：表情 & 动作（AI 自由生成）

不设固定选项池。AI 根据已选中的其他变量（球队 A、构图 C、灯光 D、背景 E）以及用户照片的气质，自动构思一个合理、自然、有趣的表情和动作组合。详见 Prompt 模板中的 EXPRESSION & ACTIVITY 段落。

### 变量 C：摄像机构图（5 选项）

| 编号 | 构图描述 |
|------|----------|
| C1 | Medium shot, subject off-center to the left at the 1/3 line, other spectators partially visible on the right edge |
| C2 | Medium close-up, subject slightly right of center, left edge partially obstructed by the shoulder of a spectator in the row ahead |
| C3 | Slightly wider shot, subject at center-left, 2-3 other fans visible in frame, slightly messy composition |
| C4 | Tighter framing, subject nearly centered but one side slightly cropped, person in front row partially blocking the bottom of frame |
| C5 | Subject caught at the edge of frame as if the camera was panning and accidentally captured them mid-sweep |

### 变量 D：灯光条件（4 选项）

| 编号 | 灯光描述 |
|------|----------|
| D1 | Night game — harsh white stadium floodlights from above creating strong shadows under eyes and chin, beyond the floodlights is darkness |
| D2 | Day game — bright outdoor sunlight, slight squinting, natural hard shadows, blue sky visible in background |
| D3 | Dusk/golden hour — warm golden sunlight mixing with stadium lights just turning on, atmospheric warm-cool contrast |
| D4 | Overcast daytime — flat even lighting, softer shadows, slightly muted desaturated colors |

### 变量 E：背景细节（5 选项）

| 编号 | 背景描述 |
|------|----------|
| E1 | Packed crowd in team jerseys, some holding phones up, portable electric fans and plastic bags visible between seats |
| E2 | Ad boards visible behind the seating sections, a SPOTV camera crew in the distant background |
| E3 | Green playing field partially visible in background blur, distant scoreboard glowing |
| E4 | Mix of occupied and empty seats (mid-week game feel), drinks and snack boxes scattered on seats |
| E5 | Light rain atmosphere — some fans with clear rain ponchos or umbrellas, tarp partially visible on the field edge |

---

## 工作流

### Step 1：读取照片（零输入）

直接读取用户已上传的照片，不问任何问题。
- 1+ 张照片 → 取第一张作为身份参考，直接进入 Step 2
- 0 张照片 → 请求上传自拍

### Step 2：analyze_image 分析照片

调用 `analyze_image` 分析用户自拍：

**提取信息：**
- 性别（决定球衣描述用词、是否有帽子等）
- 面部特征：脸型、发型、发色、肤色、五官特征
- 肤质（后续 prompt 中保持一致）
- 整体气质（用于 AI 自由生成表情动作时参考）

### Step 3：随机选变量 + 单次 generate_image

从 A/C/D/E 各随机选 1 个固定变量，B 由 AI 自由生成。**单次**调用 `generate_image`：

- **skill**: creative
- **useOriginalAsReference**: true
- **aspectRatio**: 16:9

**Prompt 模板：**

```
Generate a realistic Korean KBO baseball broadcast screenshot. This must look like a frame captured from a live SPOTV sports broadcast — NOT a posed photo, NOT a studio portrait, NOT an influencer shot.

The person from the reference photo is sitting in the spectator stands of a KBO baseball stadium. They are wearing a {A: 球衣描述}.

EXPRESSION & ACTIVITY — AI FREE GENERATION:
Based on the stadium atmosphere described below, invent a natural, candid expression and activity for this person. They are a real spectator at a KBO game — think about what real people actually do at baseball games.

Possible directions (for inspiration, not exhaustive):
- Watching the game with various emotions (focused, distracted, bored, excited, nervous about the score...)
- Interacting with food/drinks (beer, fried chicken, corn dog, cup noodles, snacks...)
- Using phone (texting, taking selfie with field behind, checking score app...)
- Reacting to a play (clapping, standing up, grabbing friend's arm, covering mouth in shock...)
- Social moments (talking to neighbor, laughing at something, sharing food...)
- Casual moments (yawning, stretching, adjusting cap, wiping sweat, fanning self with hand...)
- Props that real KBO fans have: thunder sticks, team towel, LED cheering baton, mini electric fan, baseball cap

KEY CONSTRAINTS on expression/activity:
- Must look CANDID and UNAWARE of camera
- Expression should be natural and slightly imperfect (NOT model-pose)
- Activity should match the lighting/atmosphere
- Keep facial expression natural — no exaggerated grimaces or overly dramatic reactions
- Hands should be doing something natural (holding something, resting on lap, clapping, etc.)

IDENTITY PRESERVATION — HIGHEST PRIORITY:
The person's face must be IDENTICAL to the reference photo. Same facial structure, same eyes, same nose, same mouth, same jawline, same skin tone, same hair. Do NOT beautify, smooth, enlarge eyes, slim jaw, or alter any facial feature. Preserve exact facial identity including all natural imperfections — visible pores, uneven skin texture, slight redness, oily shine, flyaway hair.

CAMERA & LENS:
{C: 构图描述}. Shot with a telephoto broadcast lens (120-150mm equivalent). Strong background compression — the crowd behind is flattened. Shallow depth of field — subject reasonably in focus, background slightly soft. Camera positioned from upper deck, slight downward angle. Subtle micro-jitter feel from handheld broadcast camera.

BROADCAST REALISM:
- Compression artifacts visible (this is broadcast TV, not 4K raw footage)
- Interlaced TV quality feel, slightly soft from zoom lens distance
- Color grading matches Korean broadcast TV — slightly desaturated, cool-neutral tones
- The person looks ACCIDENTALLY caught on camera — candid, not posed, not looking at camera
- Natural facial asymmetry preserved, visible skin texture, imperfect posture
- Slightly awkward candid posture, natural facial asymmetry, realistic skin texture, visible pores, flyaway hair, mild oily skin shine from humid stadium air

LIGHTING: {D: 灯光描述}
STADIUM ENVIRONMENT: {E: 背景描述}

WHAT THIS IS NOT:
- NOT a beauty photo, NOT retouched, NOT an influencer shot
- NOT a magazine photoshoot, NOT a posed portrait
- NOT a different person — must be recognizably the same person from reference
- Do NOT add beauty retouching, enlarged eyes, V-line jaw, porcelain skin
- Do NOT add any broadcast UI overlays, score tickers, logos, or text on the image (these will be added in post-processing)
- Do NOT add any date stamps, timestamps, or year numbers on the image

Only ONE main subject (the user). Background crowd are anonymous blurred spectators only. No extra prominent characters.
```

### Step 4：analyze_image 人脸检查

生成后调用 `analyze_image` 检查：
- 人脸与参考照片一致？（五官、发型、肤色）
- 只有一个主体人物？（背景只有模糊路人）
- 整体有转播截图质感？（长焦压缩、偏心构图）
- 画面上没有乱生成的文字/UI？

不合格 → 重新生成（最多重试 1 次）。

### Step 5：Pillow 后处理——叠加转播 UI

**⚠️ 关键设计决策：转播 UI 全部用 Pillow 后处理叠加，绝不让 AI 模型渲染。**

原因：AI 模型无法可靠渲染韩文字符、比分数字和 SPOTV 台标。Pillow 提供像素级精确控制。

**根据 Step 3 选中的球队变量(A)确定比分条中的队名。** 对手队从剩余球队中随机选一个。比分和局数随机生成。

调用 Bash 执行以下 Python3/Pillow 脚本：

```python
import sys, random, os
from PIL import Image, ImageDraw, ImageFont, ImageEnhance, ImageFilter

input_path = sys.argv[1]
output_path = sys.argv[2]
team_name = sys.argv[3] if len(sys.argv) > 3 else "두산"
opponent = sys.argv[4] if len(sys.argv) > 4 else "LG"

img = Image.open(input_path).convert('RGB')
w, h = img.size

overlay = Image.new('RGBA', (w, h), (0, 0, 0, 0))
draw = ImageDraw.Draw(overlay)

# --- Font Setup ---
font_path_bold = "/System/Library/Fonts/AppleSDGothicNeo.ttc"
font_path_fallback = "/System/Library/Fonts/Supplemental/AppleGothic.ttf"
used_font = font_path_bold if os.path.exists(font_path_bold) else font_path_fallback

def get_font(size, index=0):
    try:
        return ImageFont.truetype(used_font, size, index=index)
    except:
        try:
            return ImageFont.truetype(used_font, size)
        except:
            return ImageFont.load_default()

# Scale factor based on image width (reference: 1920px)
sf = w / 1920.0

font_team = get_font(int(28 * sf), index=0)
font_score = get_font(int(36 * sf), index=3)
font_inning = get_font(int(22 * sf), index=0)
font_bso = get_font(int(14 * sf), index=0)
font_sponsor = get_font(int(18 * sf), index=0)
font_spotv = get_font(int(32 * sf), index=3)
font_spotv_live = get_font(int(16 * sf), index=0)
font_commentator = get_font(int(14 * sf), index=0)

# --- Random Game Data ---
home_score = random.randint(0, 8)
away_score = random.randint(0, 8)
inning = random.randint(1, 9)
inning_half = random.choice(["▲", "▼"])
inning_text = f"{inning}{inning_half}"

balls = random.randint(0, 3)
strikes = random.randint(0, 2)
outs = random.randint(0, 2)

# Base runners (diamond display)
base1 = random.choice([True, False])
base2 = random.choice([True, False])
base3 = random.choice([True, False])

# Team colors
team_colors = {
    "두산": {"bg": (27, 54, 104), "text": (255, 255, 255)},
    "LG": {"bg": (200, 30, 40), "text": (255, 255, 255)},
    "KIA": {"bg": (200, 30, 30), "text": (255, 255, 255)},
    "삼성": {"bg": (30, 60, 160), "text": (255, 255, 255)},
    "SSG": {"bg": (200, 30, 40), "text": (255, 255, 255)},
    "NC": {"bg": (27, 44, 84), "text": (210, 180, 60)},
    "롯데": {"bg": (27, 44, 84), "text": (255, 255, 255)},
    "한화": {"bg": (240, 120, 30), "text": (255, 255, 255)},
    "키움": {"bg": (120, 20, 40), "text": (255, 255, 255)},
    "KT": {"bg": (0, 0, 0), "text": (255, 255, 255)},
}

home_color = team_colors.get(team_name, {"bg": (27, 54, 104), "text": (255, 255, 255)})
away_color = team_colors.get(opponent, {"bg": (200, 30, 40), "text": (255, 255, 255)})

# --- Score Ticker (upper-left) ---
ticker_x = int(20 * sf)
ticker_y = int(20 * sf)
row_h = int(32 * sf)
name_w = int(70 * sf)
score_w = int(40 * sf)
ticker_w = name_w + score_w + int(100 * sf)

# Away team row
draw.rectangle([ticker_x, ticker_y, ticker_x + name_w, ticker_y + row_h],
               fill=away_color["bg"] + (220,))
draw.text((ticker_x + int(8*sf), ticker_y + int(3*sf)), opponent,
          font=font_team, fill=away_color["text"] + (255,))
draw.rectangle([ticker_x + name_w, ticker_y, ticker_x + name_w + score_w, ticker_y + row_h],
               fill=(240, 240, 240, 220))
draw.text((ticker_x + name_w + int(12*sf), ticker_y + int(1*sf)), str(away_score),
          font=font_score, fill=(30, 30, 30, 255))

# Home team row
draw.rectangle([ticker_x, ticker_y + row_h, ticker_x + name_w, ticker_y + row_h * 2],
               fill=home_color["bg"] + (220,))
draw.text((ticker_x + int(8*sf), ticker_y + row_h + int(3*sf)), team_name,
          font=font_team, fill=home_color["text"] + (255,))
draw.rectangle([ticker_x + name_w, ticker_y + row_h, ticker_x + name_w + score_w, ticker_y + row_h * 2],
               fill=(240, 240, 240, 220))
draw.text((ticker_x + name_w + int(12*sf), ticker_y + row_h + int(1*sf)), str(home_score),
          font=font_score, fill=(30, 30, 30, 255))

# Diamond (base runners) - to the right of score
diamond_cx = ticker_x + name_w + score_w + int(30*sf)
diamond_cy = ticker_y + row_h
ds = int(10 * sf)

def draw_diamond(cx, cy, filled):
    color = (255, 200, 50, 255) if filled else (180, 180, 180, 120)
    points = [(cx, cy - ds), (cx + ds, cy), (cx, cy + ds), (cx - ds, cy)]
    draw.polygon(points, fill=color, outline=(100, 100, 100, 200))

draw_diamond(diamond_cx, diamond_cy - ds - int(2*sf), base2)       # 2nd base (top)
draw_diamond(diamond_cx - ds - int(2*sf), diamond_cy, base3)       # 3rd base (left)
draw_diamond(diamond_cx + ds + int(2*sf), diamond_cy, base1)       # 1st base (right)

# Inning display
inning_x = diamond_cx + int(25*sf)
draw.text((inning_x, ticker_y + int(5*sf)), inning_text,
          font=font_inning, fill=(255, 255, 255, 230))

# BSO count (below ticker)
bso_y = ticker_y + row_h * 2 + int(5*sf)
bso_x = ticker_x

def draw_bso_dots(x, y, label, count, max_count, active_color):
    draw.text((x, y), label, font=font_bso, fill=(200, 200, 200, 200))
    dot_x = x + int(16*sf)
    for i in range(max_count):
        color = active_color if i < count else (80, 80, 80, 150)
        draw.ellipse([dot_x + i*int(14*sf), y + int(2*sf),
                      dot_x + i*int(14*sf) + int(10*sf), y + int(12*sf)],
                     fill=color)

draw_bso_dots(bso_x, bso_y, "B", balls, 4, (60, 180, 60, 230))
draw_bso_dots(bso_x + int(80*sf), bso_y, "S", strikes, 3, (220, 180, 40, 230))
draw_bso_dots(bso_x + int(150*sf), bso_y, "O", outs, 3, (220, 60, 60, 230))

# --- Sponsor + KBO League (upper-right area, left of SPOTV) ---
sponsor_text = "신한 SOL Bank KBO리그"
sponsor_x = w - int(380 * sf)
sponsor_y = int(22 * sf)
draw.text((sponsor_x, sponsor_y), sponsor_text,
          font=font_sponsor, fill=(230, 230, 230, 200))

# --- SPOTV Logo (upper-right corner) ---
spotv_x = w - int(130 * sf)
spotv_y = int(18 * sf)

# White background box for SPOTV
spotv_box_w = int(110 * sf)
spotv_box_h = int(50 * sf)
draw.rectangle([spotv_x - int(5*sf), spotv_y - int(2*sf),
                spotv_x + spotv_box_w, spotv_y + spotv_box_h],
               fill=(255, 255, 255, 40))

draw.text((spotv_x, spotv_y), "SPOTV",
          font=font_spotv, fill=(255, 255, 255, 240))
draw.text((spotv_x + int(22*sf), spotv_y + int(34*sf)), "LIVE",
          font=font_spotv_live, fill=(255, 80, 80, 230))

# --- Composite overlay onto image ---
img_rgba = img.convert('RGBA')
composited = Image.alpha_composite(img_rgba, overlay)
result = composited.convert('RGB')

# --- Broadcast compression simulation ---
result = ImageEnhance.Color(result).enhance(0.93)

result.save(output_path, 'JPEG', quality=82)
print(f"KBO broadcast overlay applied: {output_path}")

# --- Also save transparent overlay PNG for video ffmpeg compositing ---
overlay_output = output_path.rsplit('.', 1)[0] + '_overlay.png'
overlay.save(overlay_output, 'PNG')
print(f"Transparent overlay saved: {overlay_output}")
```

**调用方式：**
```bash
python3 kbo_overlay.py input.jpg output.jpg "두산" "LG"
```

队名参数根据 Step 3 选中的球队变量(A)传入。对手队从以下列表随机选：두산, LG, KIA, 삼성, SSG, NC, 롯데, 한화, 키움, KT（排除已选的主队）。

**同时保存透明 overlay PNG** — 文件名为 `{output}_overlay.png`，供 Step 7 视频 ffmpeg 合成使用。

### Step 6：展示图片 + 立即生成视频脚本

**⚠️ 关键：展示图片后禁止停下来等用户回复，禁止列出"你可以：1. 保留 2. 重新生成..."等选项菜单。必须在同一条回复中，展示图片后紧接着说「正在为你生成视频脚本…」，然后立即调用 mcp__makaron__makaron_write_video_script。这是一个连续动作，不是两个分开的步骤。**

**视频脚本生成流程：**

1. 先调用 `analyze_image` 观察 Step 3 生成的图片（不含 UI overlay 的版本），识别人物当前的表情、动作、手持物品、身体朝向等
2. 基于图片中的状态，构建分镜故事板作为 userRequest

**分镜故事板模板：**

```
Storyboard for KBO baseball broadcast camera shot, 16:9, 4-5 seconds, single continuous shot with no cuts:

This is a live sports broadcast camera capturing a spectator in the crowd. Telephoto lens (120-150mm) positioned from upper deck, zoomed into one section of the crowd.

[0-2s]: The person sits in the crowd in the exact pose shown in the image: {根据 analyze_image 结果描述当前状态}. Minimal movement — natural breathing, slight head micro-movements. Camera has subtle broadcast-quality telephoto micro-shake (handheld feel). Background crowd has slight ambient movement (people shifting, turning heads).

[2-4s]: A natural reaction moment — {根据图片状态自由延伸动作，从图中冻结的瞬间自然地"动起来"。例如：如果在喝啤酒→放下杯子看到好球微笑；如果在看手机→抬头看球场发现精彩瞬间；如果在鼓掌→掌声渐停转头跟旁边人说话}. The home team makes a play — the person reacts naturally along with the crowd. Keep the reaction elegant and natural, not exaggerated or grotesque.

[4-5s]: Settling — shifts slightly in seat, returns to relaxed watching pose. Camera begins a very slow subtle drift as if the broadcast director is about to cut to the next shot.

CRITICAL CAMERA RULES:
- This is a BROADCAST CAMERA, not a cinematic camera
- Subtle telephoto micro-jitter throughout (not smooth gimbal)
- NO dramatic camera movements, NO cinematic pans, NO dolly moves
- The camera is essentially static with natural handheld vibration
- Shallow depth of field — subject sharp, background slightly soft

CRITICAL PERSON RULES:
- Face IDENTICAL to the image throughout — no morphing, no beauty filter
- Natural skin texture visible — pores, slight oil, imperfections
- Movement should be SUBTLE and NATURAL — this is a candid shot, not a performance
- The person should NOT look directly at camera (they don't know they're being filmed)
- Keep expressions natural and understated — no exaggerated reactions
- The motion must feel like a CONTINUATION of the still image — same pose, same props, same clothing
```

**调用 `mcp__makaron__makaron_write_video_script`：**
- **images**: [Step 3 生成的图片 URL]（不含 UI overlay 的干净版本）
- **userRequest**: 根据 analyze_image 结果填充上面的分镜模板
- **language**: "en"

等待 1-2 分钟脚本生成完成后，展示给用户：

```
🎬 视频脚本预览

基于你的 KBO 直播抓拍截图，生成了以下视频脚本（16:9，约4-5秒）：

{脚本内容原文}

---
你可以：
1. ✅ 确认 → 开始生成视频（约3-5分钟）
2. ✏️ 修改 → 告诉我想调整什么
3. ⏭️ 跳过 → 只保留图片
```

**等待用户回复：**
- 用户确认 → 进入 Step 7
- 用户要求修改 → 根据反馈编辑脚本，重新展示
- 用户跳过 → 结束，保留图片结果

### Step 7：生成视频

用户确认脚本后：

**调用 `mcp__makaron__makaron_create_video`：**
- **script**: 用户确认的脚本内容
- **images**: [同 Step 6 的图片 URL]
- **aspectRatio**: "16:9"
- **duration**: 5

获取返回的 Task ID 后，告知用户：「视频生成中，预计 3-5 分钟…」

**轮询 `mcp__makaron__makaron_get_video_status`：**
- 每 15 秒轮询一次
- 状态变为 `completed` 后提取 videoUrl

**视频完成后，用 ffmpeg 叠加转播 UI overlay：**

先用 Bash 下载视频到本地，然后用 ffmpeg 合成：

```bash
# Download video
curl -o raw_video.mp4 "{videoUrl}"

# Get video dimensions
VIDEO_SIZE=$(ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=p=0 raw_video.mp4)

# Resize overlay to match video dimensions
python3 -c "
from PIL import Image
import sys
overlay = Image.open('{overlay_png_path}')
vw, vh = {video_width}, {video_height}
overlay = overlay.resize((vw, vh), Image.LANCZOS)
overlay.save('resized_overlay.png')
"

# Composite overlay onto video (keep audio!)
ffmpeg -i raw_video.mp4 -i resized_overlay.png \
  -filter_complex "[0:v][1:v]overlay=0:0" \
  -c:a copy \
  final_video.mp4
```

**⚠️ 绝对不要使用 -an 参数，必须保留视频原始音频。**

展示最终视频结果。

---

## Tips Directions

1. **斗山熊观众**: Upload your selfie and become a Doosan Bears fan caught on the KBO broadcast camera. Sitting in the crowd with a beer, wearing a Bears jersey, the SPOTV camera captures your natural expression during the game. Full broadcast UI with score ticker and station logo.
2. **夜场比赛**: Night game at Jamsil Stadium — harsh floodlights overhead, you're in the packed cheering section, the broadcast camera zooms in and catches your candid moment. Complete with SPOTV score overlay and broadcast compression feel.
3. **啤酒时光**: Casual afternoon game, you're caught on camera in the stands, completely unaware of the broadcast camera. Off-center framing, telephoto compression, pure candid moment with KBO broadcast authentics.
4. **得分欢呼视频**: Generate a 4-5 second broadcast clip — the camera finds you in the crowd, the home team scores, and your natural happy reaction is captured on live TV. Complete with SPOTV UI and broadcast camera micro-shake.

---

## Rules

1. **单人 skill** — 只生成一个人（用户自己）在球场。背景观众是匿名模糊路人，不能凭空多出突出的人物角色。
2. **人脸身份第一优先** — 必须与上传照片一致。不美颜、不磨皮、不放大眼睛、不瘦脸。可见毛孔、肤质、自然不完美。不像就重试（最多 1 次）。
3. **零输入工作流** — 照片上传即开始，不问球队/场景/表情，所有决策自动完成。唯一交互点：视频脚本确认。
4. **转播 UI 必须用 Pillow 后处理** — 绝不让 AI 模型渲染比分条、SPOTV 台标或韩文文字。Prompt 中明确禁止生成任何 UI 文字。
5. **16:9 固定** — 转播画面格式，不生成竖版或正方形。
6. **useOriginalAsReference: true** — 所有 generate_image 调用必须设置。
7. **长焦镜头感必须有** — 背景压缩、浅景深、柔焦。这是远距离变焦，不是近距离人像镜头。
8. **不加时间戳/日期** — Prompt 中明确禁止。转播 UI 由后处理控制。
9. **默认斗山熊** — 除非用户指定其他球队。
10. **视频 UI 用 ffmpeg 叠加** — 视频渲染完成后合成静态 overlay，不写进 video prompt。
11. **视频脚本必须经用户确认** — 这是整个流程中唯一需要用户确认的环节。
12. **视频必须保留音频** — ffmpeg 合成时绝对不用 -an 参数。
13. **不生成违法、仇恨、色情内容** — 保持健康积极的体育文化。
