---
name: y2k-camcorder
description: >
  Upload a photo, become a Y2K camcorder memory. VHS timestamp overlay,
  Japanese street scenes, whip pan transitions, DV nostalgia.
allowed-tools: generate_image analyze_image generate_animation
metadata:
  makaron:
    icon: "📹"
    color: "#FFB347"
    tags: [Y2K, VHS, camcorder, streetwear, 2000s, nostalgia, japan]
    faceProtection: default
    defaultAspectRatio: "9:16"
---

# Y2K Camcorder — 千禧年 DV 实拍

⚠️ 用户上传照片即开始，不问任何问题。

## 输出
一条 10s 9:16 Y2K DV 短片。像 2002 年日本街头有人拿 Sony Handycam 拍的你。VHS 时间戳 + 色散 + 花屏结尾。

## 核心理念

**身份幻想**：用了它我变成千禧年日本街头的 DV 录像主角

**对标**：2000 年代日系街头 DV 实拍——便利店霓虹、斑马线黄昏、地铁站台。不是 MV，是"这个录像带是 2002 年拍的"。

**分享场景**：TikTok / 小红书 / IG，9:16 直接发。

## 工作流

### Step 1: 角色穿搭图（唯一参考图）

只用一张角色图保证全片着装一致：

```bash
makaron-cli chat --project auto --image <user_photo> --json -b "<prompt>"
```

```
Transform this person into Y2K Japanese street style. Keep face 100% recognizable. Outfit: oversized black graphic t-shirt (abstract design), baggy light-wash wide-leg jeans, backwards black baseball cap, silver chain necklace, chunky black-and-white sneakers. Full body against plain wall. Relaxed confident look. 9:16 vertical. Clean lighting. No text, no logos.
```

### Step 2: 视频生成

用单张参考图 + Seedance，脚本用纪录片描述而非舞台场景描述：

```bash
makaron-cli video create --model seedance --duration 10 --image <cdn_url> --script "<script>"
```

**Script**（关键：用"found footage"叙事，非"scene 1/2"叙事）：
```
Found footage from a 2002 Sony Handycam, 9:16 vertical. The person from <<<media_1>>> wears exactly this outfit in every scene — oversized black graphic tee, baggy light-wash wide jeans, backwards black cap, silver chain. Outfit NEVER changes. NOT staged — real DV footage of someone hanging out in Tokyo.

0-2s: Crosswalk at dusk — walks through pedestrian crossing, hands in pockets, pink-orange sunset sky, blurred passersby. Unposed.

2-4s: Raw handheld motion blur — camera swings across the street, urban lights trail past. Not cinematic.

4-6s: Convenience store at night — stands by colorful vending machines, warm neon glow, looks around casually. Not posing.

6-8s: Walking on a street at dusk — walks away from camera, glances back naturally.

8-10s: Subway platform at night — leans against tiled wall, train lights blur past, slight natural smile, looks away coolly.

Warm nostalgic colors. Slight DV grain. Handheld wobble. Low contrast. No text, no effects.
```

### Step 3: VHS 后期

**FFmpeg 后处理**（色散 + 噪点 + 时间戳 + 渐变花屏结尾）：

```bash
# Step A: Main clip with DV effects (first 9.3s)
ffmpeg -y -threads 1 -i raw.mp4 \
  -vf "rgbashift=rh=-3:bv=3,noise=alls=5:allf=t,drawtext=text='13 00 28':fontcolor=yellow@0.85:fontsize=26:x=8:y=h-th-16,scale=720:1280,format=yuv420p" \
  -ss 0 -t 9.3 -c:v libx264 -profile:v baseline -level 3.1 -preset ultrafast -crf 28 \
  -pix_fmt yuv420p -movflags +faststart -c:a aac -b:a 64k -ar 44100 \
  main.mp4

# Step B: Gradual glitch ending (0.7s — light noise → fade to black)
ffmpeg -y -threads 1 -f lavfi -i "color=black:s=720x1280:d=0.7:r=24" \
  -vf "noise=alls=15:allf=t,eq=contrast=1.3:brightness=0.03,drawgrid=w=iw:h=6:color=white@0.08:replace=1,fade=out:st=0.3:d=0.4,format=yuv420p" \
  -c:v libx264 -profile:v baseline -level 3.1 -preset ultrafast -crf 23 \
  -pix_fmt yuv420p -movflags +faststart -an glitch.mp4

# Step C: Concat
echo "file 'main.mp4'
file 'glitch.mp4'" > concat.txt

ffmpeg -y -threads 1 -f concat -safe 0 -i concat.txt \
  -c:v libx264 -profile:v baseline -level 3.1 -preset ultrafast -crf 30 \
  -pix_fmt yuv420p -movflags +faststart -c:a aac -b:a 64k -ar 44100 \
  output.mp4
```

### Step 4: QC

| 项目 | 标准 |
|------|------|
| 面部 | 100% 可辨认 |
| 穿搭一致 | 全片同款不变（单参考图保证） |
| 场景 | 5 个场景（十字路口/whip pan/便利店/街景/地铁站） |
| 转场 | whip pan 运动模糊 |
| VHS | 竖排黄色时间戳 + 色散 + 噪点 |
| 结尾 | 渐变花屏 fade to black |
| 编码 | h264 baseline, yuv420p, faststart |
| 时长 | 10s 9:16 |

## 品味指引

**对标大作**：2002 Sony Handycam 实拍 × 日系街头 Y2K 怀旧视频

**核心元素**：
- VHS 时间戳 `13 00 28` 黄色左侧竖排
- 日系街头（斑马线+贩卖机+地铁站）
- 黄昏/夜景暖色调
- Whip pan 转场
- 不摆 pose，像真实 DV 拍到的
- 渐变花屏收尾不突兀

**反面教材**：
- ❌ 稳定三脚架画面
- ❌ 道具堆砌（翻盖手机/蝴蝶夹）
- ❌ 舞台/影棚场景
- ❌ 场景切换换衣服
- ❌ 硬切到 VHS 雪花
- ❌ H.264 High Profile（用 Baseline）

## Rules
1. 零输入 — 上传即开始
2. 面部 100% 保留
3. 单张参考图保着装一致
4. 脚本用"found footage"叙事，非"scene"叙事
5. Y2K 日系街头穿搭（oversized 黑T + 宽牛仔裤 + 反戴帽 + 银链）
6. VHS 竖排黄色时间戳 + 色散 + 噪点
7. 渐变花屏结尾（gentle → fade out）
8. h264 baseline + yuv420p + faststart
9. 9:16 竖屏，10s
10. 输出即发
