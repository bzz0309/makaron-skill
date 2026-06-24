---
name: fb-ad-creator
description: |
  Facebook 投放素材视频一键生成器。给定 Makaron Skill 的效果视频、App 操作录屏、自拍原图和 Logo CTA 动画，
  自动生成一条完整的 9:16 竖屏 Facebook 广告视频，包含英文旁白、BGM、字幕和品牌 CTA。
  输出结构：Hook（效果先行）→ 自拍反转 → App 操作教程 → 效果展示 → Logo CTA。
allowed-tools: [read, write, exec]
summary-cn: 一键生成 Facebook 投放素材视频
summary-en: One-click Facebook ad creative video generator
version: 0.2.0
tags: [Video, Advertising, Facebook]
trigger-words: [投放素材, 投放视频, 广告视频, Facebook广告, FB ad, ad creative, 投放素材视频, 做一条广告, 生成投放视频]
---

# Facebook 投放素材视频生成器

当用户需要为 Makaron 的某个 Skill 制作 Facebook 投放广告视频时，使用此工作流。

最终输出：一条 **9:16 竖屏**、约 **12-15 秒**的 Facebook 广告视频，包含：
- 英文旁白（FOMO 风格）
- 节奏感 BGM（旁白段自动降低）
- 上方全大写粗体字幕
- 品牌 Logo CTA 结尾

## STEP 0: 确认素材

需要用户提供 4 个素材：

| 素材 | 必须 | 说明 |
|------|------|------|
| **效果视频** | ✅ | Skill 生成的最终效果展示（如棒球直播、打歌舞台等） |
| **App 操作录屏** | ✅ | Makaron App 内选 Skill → 点击创建的操作过程，必须全英文界面 |
| **自拍原图** | ✅ | 用于 "before" 对比展示的自拍照片 |
| **Logo CTA 动画** | ✅ | Makaron 品牌动画，用于结尾 CTA，必须是 9:16 竖屏且无水印 |

如果用户缺少某个素材，提示具体需要什么。
如果录屏界面有中文，提醒用户切换到英文界面后重新录制。

额外确认：
- 效果视频对应的 **Skill 名称**（英文，用于旁白文案，如 "Broadcast Candid"）
- 是否有**竞品参考视频**（可选，用于参考风格节奏）


## STEP 1: 分析素材 & 准备片段

### 1a: 探测素材参数

用 ffprobe 获取每个素材的分辨率、时长、宽高比。

### 1b: 准备效果视频

根据效果视频的宽高比决定处理方式：

- **横屏（如 16:9）**：使用模糊背景填充，保留完整画面内容。
  方法：`split[original][blur]; [blur]scale=1080:1920,boxblur=30:30[bg]; [original]scale=1080:-1[fg]; [bg][fg]overlay=(W-w)/2:(H-h)/2`
- **竖屏（如 9:16）**：直接缩放到 1080x1920。

输出两个片段：
1. **Hook 片段**：前 2-3 秒，用于开场抓眼球
2. **效果展示片段**：完整视频加速到 3-4 秒（用 `setpts=PTS/N`，N 根据原始时长计算）

### 1c: 准备操作录屏

- 缩放到 1080x1920
- 裁剪到 3-5 秒（保留最关键的操作流程：浏览 → 点击 Skill → 预览/创建）
- 去掉原始音频

### 1d: 准备自拍片段

- 将静态图片转为 1-1.5 秒的视频片段
- 如果图片比例不是 9:16，用黑色填充适配到 1080x1920
- 方法：`-loop 1 -i selfie.png -vf "scale=1080:1440,pad=1080:1920:0:240:black" -t 1.5`

### 1e: 准备 Logo CTA

- 缩放到 1080x1920
- 如果时长超过 3 秒，加速到 2.5-3 秒
- 去掉原始音频


## Audio Normalization (MANDATORY — before any mixing)

All audio sources must be converted to the same format before mixing:

```bash
# Convert TTS voiceover to PCM WAV 44100Hz stereo
ffmpeg -y -i voiceover.mp3 -ar 44100 -ac 2 -c:a pcm_s16le voiceover_pcm.wav

# Convert BGM to PCM WAV 44100Hz stereo
ffmpeg -y -i bgm.mp3 -ar 44100 -ac 2 -c:a pcm_s16le bgm_pcm.wav
```

**WHY**: TTS output is typically 24kHz mono MPEG v2. BGM is 44.1kHz stereo. Mixing mismatched sample rates causes VO to disappear silently from the final export. Always normalize both to 44100Hz stereo PCM WAV before mixing.

## STEP 2: 生成旁白文案 & 语音

### 2a: 根据 Skill 名称生成旁白文案

模板（根据具体 Skill 调整）：

```
"Everyone's posting their [skill场景描述] right now.
All you need — one selfie.
Open Makaron. Pick [Skill名称].
Done. Your version is waiting."
```

例如棒球直播：
```
"Everyone's posting their stadium cam moment right now.
All you need — one selfie.
Open Makaron. Pick Broadcast Candid.
Done. Your version is waiting."
```

### 2b: 生成英文女声旁白

- 风格：年轻、自信、有活力，TikTok 创作者推荐语气
- 情绪：happy/excited，FOMO 能量感
- 语速：略快（speed 1.1），总时长控制在 8-10 秒
- 品牌名 "Makaron" 发音标注为 "mack-a-ron"

### 2c: 拆分旁白并对齐时间轴

旁白生成后，**必须按完整句子拆分**，不得按时间估测切分：
1. "Everyone's posting their [场景] right now."
2. "All you need — one selfie."
3. "Open Makaron."
4. "Pick [Skill名称]."
5. "Done." or "Create."
6. "Your version is waiting."

### 2c-1: 找句子边界

三种方式，按优先级使用：

**优先**：每句单独 TTS 生成独立 wav，天然有边界。
```bash
# 逐句生成，每句一个 wav
# 句1: "Everyone's posting their captain moment right now." → seg0.wav
# 句2: "All you need — one selfie." → seg1.wav
# ...
```

**fallback**：整段 TTS + silencedetect 找边界。
```bash
ffmpeg -i voiceover_pcm.wav -af "silencedetect=noise=-30dB:d=0.15" -f null - 2>&1 | grep silence
```

**禁止**：手估切在单词中间（如"段1≈2.0s"）→ 导致吞音。

### 2c-2: 用 adelay 对齐

根据 silencedetect 结果，按句子边界 atrim，然后用 adelay 对齐到视频时间轴：

| 旁白段 | 对应画面 | 说明 |
|--------|---------|------|
| 句子 1 | Hook (0-2.5s) | adelay=0ms |
| 句子 2 | 自拍 (2.5-4s) | adelay=2500ms |
| 句子 3 "Open Makaron." | 录屏开始 (4-5s) | adelay=4000ms |
| 句子 4 "Pick [Skill]." | 录屏中段 (~6s) | adelay=6000ms |
| 句子 5 "Create." | 录屏末端 (~7s) | adelay=7000ms |
| 句子 6 | 效果展示 (8-11s) | adelay=8000ms |

> **关键**：UI 教程段（Open Makaron / Pick Skill / Create）必须拆成 3 个独立 clip，每个对齐到对应的录屏视觉动作，不得作为一个长段落整体移动。

### 2c-3: 防吞音

每个 clip 的 atrim 在 silencedetect 边界上切，末尾加 150–250ms silence pad，再加 fade in/out 防吞音：

```bash
ffmpeg -i voiceover_pcm.wav -filter_complex "
  [0:a]atrim=0.22:2.28,apad=pad_len=250,afade=t=in:d=0.03,afade=t=out:d=0.03[seg0];
  [0:a]atrim=2.65:3.71,apad=pad_len=250,afade=t=in:d=0.03,afade=t=out:d=0.03[seg1];
  ...
  [seg0]adelay=0:all=1[a0];
  [seg1]adelay=2500:all=1[a1];
  ...
  [a0][a1]...[a5]amix=inputs=6:normalize=0[vo]
" -map "[vo]" -ar 44100 -ac 2 -c:a pcm_s16le vo_aligned.wav
```

> **关键**：每个 VO clip 末尾加 150–250ms silence pad 留尾音，避免词尾被下一段冲掉。


## STEP 3: 生成 BGM

生成一段节奏感强的电子/流行纯音乐 BGM：
- 风格：energetic electronic pop, upbeat, K-pop energy, modern ad music
- 无人声
- 时长会超过需要，后续会裁剪

如果 BGM 生成服务不可用，可跳过此步先出纯旁白版本，服务恢复后再添加。


## STEP 4: 用户确认

将以下内容展示给用户确认：
- 旁白文案
- 效果视频的模糊填充/缩放处理效果
- 各片段时长

高成本操作（合成）在确认后进行。


## VO / Subtitle / Timeline Sync Rules

These rules are production-critical for paid social ad creatives. Do not skip.

### 1. Split voiceover by visual action

For UI/tutorial segments, split narration into independent clips:

```text
Open Makaron.
Pick {skill_name}.
Create.
```

Each line must align to its own visual action in the app recording.

### 2. Recommended UI tutorial timing

For a 12-15s ad with a 4-8s app tutorial segment:

```text
4.2s-4.9s: Open Makaron. -> app opens / home screen visible
5.8s-6.6s: Pick {skill_name}. -> skill card is selected / highlighted
6.9s-7.5s: Create. -> create / generate action happens
```

Adjust timing to the actual app recording, but keep each phrase tied to its visual action.

### 3. Prevent swallowed word endings

- Cut at silencedetect boundaries, not manual time estimates.
- Check word endings in final MP4: `now`, `selfie`, `{skill_name}`, `Create`, `waiting`.
- If a word ending is swallowed, regenerate or re-time that clip. Do not hide under BGM.

### 4. Final export audio gate (MANDATORY)

Before sending any version for review:

```text
[ ] VO source file exists and is audible
[ ] Final MP4 contains audible VO, not only BGM
[ ] BGM ducks under VO (volume <= 0.12) and does not mask consonants
[ ] 5-8s UI tutorial VO matches the app recording actions
[ ] Subtitles exactly match the VO text
```

If final export has BGM only and no VO -> status is **BLOCKED**.

### 5. Subtitle / VO lock

Subtitles cover key marketing copy (3 lines), not every VO word. Subtitle text must not conflict with VO. If VO phrases change, check whether related subtitles need updating.

Example: if VO `Done.` → `Create.`, check both:
```text
VO: Open Makaron. Pick Football Captain. Create.
Subtitle lines: Hook / Selfie / Reveal — "Create" does not appear in these 3 subtitles, so no change needed.
```

### 6. Subtitle safe area

- Keep subtitles inside platform-safe area (Alignment=8, FontSize=42, MarginV=80).
- Do not place where app UI, face, logo, or platform overlays can cover them.
- Don't match the old spec values (Alignment=8, MarginV=200, FontSize=50) - those get covered.

### 7. QC failure labels

Use these labels when review fails:
```text
vo_missing
vo_cutoff
vo_swallowed_word
vo_visual_sync_mismatch
bgm_over_vo
subtitle_safe_area_issue
subtitle_vo_mismatch
```

---

## STEP 5: 合成视频

### 5a: 编写 concat 文件

按以下顺序排列片段：
```
file 'hook.mp4'
file 'selfie.mp4'  
file 'ui-tutorial.mp4'
file 'reveal-fast.mp4'
file 'logo-cta.mp4'
```

用 `ffmpeg -f concat` 拼接（所有片段必须是相同的分辨率 1080x1920、帧率 24fps、编码 H.264）。

### 5b: 编写 ASS 字幕

字幕风格：
- 位置：顶部安全区（Alignment=8, MarginV=80）
- 字号：42pt
- 粗体、全大写、白色、黑色描边（Outline=4）
- 字体：Helvetica

字幕只覆盖关键营销文案（3 条），不要求逐字匹配 VO；但字幕文本不能和 VO 表达冲突。VO 文案变化时，相关字幕必须同步检查：
1. Hook 段："EVERYONE'S POSTING THEIR [场景] RIGHT NOW"
2. 自拍段："ALL YOU NEED — ONE SELFIE"
3. 效果展示段："YOUR VERSION IS WAITING"
UI 教程和 CTA 段不加字幕。

### 5c: 合成最终视频

一条 ffmpeg 命令完成：视频拼接 + 字幕烧录 + 旁白混音 + BGM 混音

```
ffmpeg -f concat -safe 0 -i concat.txt \
  -i vo-synced.mp3 \
  -i bgm.mp3 \
  -filter_complex "[1:a]apad[vo]; [2:a]atrim=0:TOTAL_DUR,volume=0.15,afade=t=out:st=FADE_START:d=1.5[bgm]; [vo][bgm]amix=inputs=2:duration=first:normalize=0[aout]" \
  -vf "ass=subs.ass" \
  -map 0:v -map [aout] \
  -c:v libx264 -crf 18 -c:a aac -b:a 192k -shortest \
  output.mp4
```

BGM 处理：
- 音量降到 0.10-0.12（始终在旁白下方，不遮盖辅音和词尾）
- 最后 1.5 秒渐弱淡出


## STEP 6: 展示结果

1. 保存到会话文件（`hub_save_file_to_session`）
2. 放到画布上（`hub_canvas_write_media_node`）
3. 聚焦到节点（`hub_canvas_focus_nodes`）
4. 用 markdown 内联展示给用户

展示时列出：
- 最终视频时长
- 各段落时间轴
- 可优化方向（如调整节奏、换 BGM 风格、修改文案）


## 迭代修改

用户常见的调整请求及处理方式：

| 请求 | 处理 |
|------|------|
| 音画不同步 | 调整旁白段的 adelay 值，重新混音 |
| 效果视频太长/太短 | 调整 setpts 加速倍率 |
| 替换录屏 | 重新缩放裁剪，替换 concat 列表中对应行 |
| 替换 CTA | 重新处理 CTA 片段，替换 concat 列表 |
| 字幕位置/大小 | 修改 ASS 文件的 MarginV/FontSize |
| 换 BGM | 重新生成 BGM，重新混音 |
| 改旁白文案 | 重新生成语音 → 拆分 → 重新对齐时间轴 |

**快速替换流程**：如果只是替换某个片段，不需要重新生成旁白和 BGM，只需：
1. 处理新片段（缩放/加速/裁剪）
2. 更新 concat 文件
3. 重新拼接 + 烧字幕 + 混音频
