---
name: world-cup-live-candid
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "📺"
    color: "#EA580C"
    tags: [world-cup, live, candid, stadium, broadcast, reaction, sports]
    faceProtection: strict
    defaultAspectRatio: "9:16"
    defaultCoverStyle: sporty|lively|attractive|confident
    tipsEnabled: true
    tipsCount: 4
    modelPreference: [seedance, kling, gemini]
---
# World Cup Live Candid — 世界杯现场直击
POV: the live camera caught you right after the goal. Turn one photo into a World Cup stadium reaction.
Pipeline: Selfie → Stadium crowd + live camera HUD → Reaction → Broadcast replay card.
Safety: No real broadcaster logos. No real player names. Face preserved.
Budget: max 5 gen + 1 video. QC: PASS/REROLL/BLOCKED.
Delivery: world_cup_live_candid.mp4 10-15s 9:16, cover_frame.jpg, prompt_used.md, qc_report.md.

## 球队选择规则（一键默认）

首次用户不需要写 prompt，系统自动根据人脸族裔匹配支持的国家队。

**优先级：**
1. 用户明确指定支持球队 → 用指定球队配色
2. 用户未指定 → 识别图片中人脸族裔，按配色表自动匹配
3. 族裔识别不确定 → **默认巴西队 🇧🇷**

## 球队配色表

| 族裔 | 国家队 | 球衣主色 | 围巾/配件色 | 文字色 |
|------|--------|----------|------------|--------|
| 东亚脸 | 日本 🇯🇵 | 深海军蓝 + 白 | 蓝白条纹 | 银白 |
| 东亚脸 | 韩国 🇰🇷 | 红 + 白 | 红白条纹 | 金 |
| 欧美脸 | 巴西 🇧🇷（默认） | 黄 + 绿 | 黄绿条纹 | 金 |
| 欧美脸 | 阿根廷 🇦🇷 | 蓝白条纹 | 蓝白条纹 | 金 |
| 欧美脸 | 英格兰 🏴 | 白 + 深蓝 | 白蓝条纹 | 金 |
| 欧美脸 | 法国 🇫🇷 | 深蓝 + 金 | 蓝金条纹 | 金 |
| 非洲脸 | 非洲 🌍 | 绿 + 黄 | 绿黄条纹 | 金 |
| 中东/南亚 | 通用 | 白 + 绿 | 白绿条纹 | 金 |

**暗黑底色固定，无真实广播商 logo，人脸保留不变。**