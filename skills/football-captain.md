---
name: football-captain
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "⚽"
    color: "#1D4ED8"
    tags: [football, captain, team, leader, sports, cinematic]
    faceProtection: strict
    defaultAspectRatio: "9:16"
    defaultCoverStyle: sporty|authoritative|confident
---
# Football Captain — 足球队长
Turn a selfie into a team captain pose: armband, stadium tunnel, cinematic walkout.
Pipeline: Selfie → Tunnel/armband → Captain pose → Stadium reveal.
Safety: No real club/league logos. No real player likeness. Face preserved.
Budget: max 5 gen + 1 video. QC: PASS/REROLL/BLOCKED.
Delivery: football_captain.mp4 10-15s 9:16, cover_frame.jpg, prompt_used.md, qc_report.md.
