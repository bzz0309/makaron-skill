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
---
# World Cup Live Candid — 世界杯现场直击
POV: the live camera caught you right after the goal. Turn one photo into a World Cup stadium reaction.
Pipeline: Selfie → Stadium crowd + live camera HUD → Reaction → Broadcast replay card.
Safety: No real broadcaster logos. No real player names. Face preserved.
Budget: max 5 gen + 1 video. QC: PASS/REROLL/BLOCKED.
Delivery: world_cup_live_candid.mp4 10-15s 9:16, cover_frame.jpg, prompt_used.md, qc_report.md.
