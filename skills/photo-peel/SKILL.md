---
name: photo-peel
description: |
  写实摄影质感的人物撕纸剥离效果。用户提供一张含人物的照片，自动生成一条视频：
  手指从画面右上角捏住人物，像撕 2D 贴纸一样完整撕离画面，撕完后将人物贴纸举到镜头前展示，
  展示时贴纸边缘出现白色细切割线描边，最后定格。
  触发词：撕纸、贴纸撕离、照片撕掉、人物剥离、photo peel、sticker peel。
allowed-tools: generate_animation
metadata:
  makaron:
    icon: "🏷️"
    color: "#D4A574"
    tags: [Video, Effect, Photo]
---

# Photo Peel — 人物撕纸剥离效果

将照片中的人物像 2D 贴纸一样撕离画面，展示在镜头前。

## 最终 Prompt（经过 5 轮调优，2026-06-05）

```
原图开始，人物融入背景，无描边。少女手捏住人物右上角，把整个人物像贴纸完整撕离画面——必须100%撕掉，人物完全消失只剩背景。撕的过程中贴纸边缘不出现任何描边。完全撕离后手把完整人物贴纸举到镜头前展示，此时贴纸边缘才出现白色细切割线描边。轻快BGM。9:16竖屏，4-5秒。
```

## Prompt 关键点

| 要点 | 说明 |
|------|------|
| **无描边初态** | 原图人物完全融入背景，不能有任何描边/轮廓线 |
| **撕时无描边** | 撕离过程中贴纸边缘干净，不出现任何白边 |
| **100% 撕离** | 人物必须从画面中完全消失，不能只撕一半 |
| **展示出描边** | 只有举到镜头前展示时，贴纸边缘才出现白色细切割线 |
| **背景保留** | 撕离后露出的是原图背景（不是空白/纯色） |
| **轻快 BGM** | 活泼节奏，带撕纸音效 |
| **版权过滤** | 上传前检查知名品牌 logo、商标、copyright 地标 |

## 版权规避

Makaron 底层 Kling 模型对以下敏感：
- ❌ 知名品牌：FILA、Loewe、Dr. Martens、Nike、Adidas 等
- ❌ 知名地标：Hollywood Sign 等
- ❌ 球衣队标、大面积商标图案
- ✅ 非知名文字（如 "Smooth"、"GOOD DAY EVERY DAY"）一般能过

## 输出

- 9:16 竖屏视频
- 720×1280
- 4-5 秒，带 BGM 音频

## 多图拼接

多张图片批量生成后，用 ffmpeg concat 拼接，**保留音频**：

```bash
cat > concat.txt << 'EOF'
file 'video1.mp4'
file 'video2.mp4'
file 'video3.mp4'
EOF
ffmpeg -f concat -safe 0 -i concat.txt -c:v libx264 -preset ultrafast -crf 18 -c:a aac -b:a 128k -threads 1 output.mp4
```

⚠️ **不要加 `-an` 去音频！** makaron 视频自带 BGM。
