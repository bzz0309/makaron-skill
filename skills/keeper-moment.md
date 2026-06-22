---
name: keeper-moment
allowed-tools: [generate_image, generate_video, analyze_image]
metadata:
  makaron:
    icon: "🧤"
    color: "#059669"
    tags: [goalkeeper, save, diving, football, sports, action]
    faceProtection: strict
    defaultAspectRatio: "9:16"
    defaultCoverStyle: sporty|dramatic|athletic
---
# Keeper Moment — 门将时刻
Turn a selfie into a goalkeeper diving save: mid-air, outstretched, match-saving moment.
Pipeline: Selfie → Goal frame → Diving save pose → Ball deflection → Hero landing.
Safety: No real player likeness. No real league logos. Face preserved. No injury imagery.
Budget: max 6 gen + 1 video. QC: PASS/REROLL/BLOCKED.
Delivery: keeper_moment.mp4 10-15s 9:16, cover_frame.jpg, prompt_used.md, qc_report.md.
