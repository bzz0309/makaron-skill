---
name: world-cup-mvp
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "🏆"
    color: "#DC2626"
    tags: [world-cup, soccer, stadium, broadcast, reaction, sports]
    faceProtection: strict
    defaultAspectRatio: "9:16"
    defaultCoverStyle: sporty|attractive|confident
---
# World Cup MVP — 世界杯 MVP 直播反应
Turn a selfie into a live World Cup broadcast: caught on camera after the winning goal.
Pipeline: Selfie → Stadium crowd bg + broadcast overlay graphics → Reaction moment → Final broadcast card.
Safety: No real broadcaster logos. No real player likeness. Face preserved.
Budget: max 5 gen + 1 video. QC: PASS/REROLL/BLOCKED.
Delivery: world_cup_mvp.mp4 10-15s 9:16, cover_frame.jpg, prompt_used.md, qc_report.md.
