---
name: workflow-contract
allowed-tools: [read, write, exec, analyze_image]
---

# Workflow Contract v0.1

Production QC → FB Ad Packaging → Deployment → Metrics. Apply this contract to any Makaron video skill entering promotion.

## Safety / Permissions

- `write`: only allowed for contract, report, failure log
- `exec`: only allowed for local check and packaging
- No auto-deploy, no external dispatch, no production config changes
- Status: approved for internal orchestration / not approved for autonomous ad deployment

## Pipeline

```
Skill QC Gate → FB Ad Creator → Deployment → Metrics Feedback
```

### Stage I/O Contracts

| Stage | Input | Output |
|-------|-------|--------|
| QC Gate | 3-5 test portraits + skill prompt | pass / reroll / blocked + failure log |
| FB Ad Creator | passed sample video + app recording + CTA assets | final ad video + campaign materials |
| Deployment | final ad package | upload-ready ad package; uploaded ad + receipt only after explicit human approval |
| Metrics | deployment ID + tracking link | feedback row + next action |

## Step 1: Production QC Gate

Before advertising, the skill must pass QC. Run this gate on 3-5 test portraits covering diverse faces.

### Static Asset / Keyframe QC (mark N/A where not applicable)

| # | Check | Pass Criteria | Fail Fix |
|---|-------|--------------|----------|
| 1 | Face Identity | Bone structure matches original | Reduce styling intensity, regenerate |
| 2 | Color / Theme | Theme / national-color styling matches prompt and avoids stereotyping | Fix color or styling parameters |
| 3 | Layout | Subject + UI positioned correctly | Strengthen layout constraints |
| 4 | Text Position | No text overlaps face | Shrink + reposition text |
| 5 | Brand Safety | No real brand logos | Replace with generic icons |

### Video QC (5 items)

| # | Check | Pass Criteria | Fail Fix |
|---|-------|--------------|----------|
| 1 | UI Stability | UI text/logos static, unaltered | Strengthen frozen/static constraints |
| 2 | Motion Layers | Distinct action beats (not repetitive) | Add action variety descriptions |
| 3 | End Eye Contact | Last 2s looks at camera | Emphasize direct eye contact |
| 4 | Layout Stability | Video layout matches poster | Use approved poster as image input |
| 5 | Text Fixed | Any display text stays in place | Add "text stays fixed" constraint |

### Reroll Strategy

- ≤2 QC fails → fix + reroll once
- 3+ QC fails → revise the prompt before rerolling
- Face deformation → always reroll (non-negotiable)

### Failure Library

Log every failure. Each entry: Skill name, fail type, root cause, fix applied, reroll result.

## Step 2: FB Ad Creator

Package the skill into a Facebook ad. Use this 5-segment structure.

**Prerequisite**: All 4 assets must be received before packaging begins: effect video + app recording + selfie image + Logo CTA.

**Audio rule**: Convert TTS and BGM to 44100Hz stereo PCM WAV before mixing. Mismatched sample rates cause silent VO.

**Subtitle rule**: Subtitles cover 3 key marketing lines (Hook / Selfie / Reveal), do not need to match VO word-for-word, but must not conflict. VO text changes → check related subtitles.

**Final export gate**: Before sending any version, verify: VO audible in final MP4 / BGM ducks under VO (≤0.12 volume) / UI VO matches app recording actions / subtitles in safe area.

### Structure

| # | Segment | Duration | Content | Caption |
|---|---------|----------|---------|---------|
| 1 | Hook | 0-2s | Final effect straight away | EVERYONE'S POSTING THEIR [SCENE] RIGHT NOW |
| 2 | Selfie Reversal | 2-4s | Plain selfie → effect smash cut | ALL YOU NEED — ONE SELFIE |
| 3 | App Tutorial | 4-7s | Upload → Pick → Generate (≤3s) | None |
| 4 | Effect Showcase | 7-12s | 2-3 variants | None |
| 5 | Logo CTA | 12-15s | Logo + FOMO VO + BGM | YOUR VERSION IS WAITING |

### FOMO Voiceover Formula

Hook (FOMO) → Solution (one selfie) → Action (open Makaron) → Call (go now) → Reward (yours is waiting).

### Ad QC (before upload)

- [ ] Hook grabs attention in first 2s
- [ ] No brand logos or sponsor marks
- [ ] Selfie reversal is instantly understandable
- [ ] App tutorial ≤3 seconds
- [ ] Effect showcase ≥2 variants
- [ ] CTA is clear and actionable

### Final Video QC

- [ ] First 2s clearly shows the end effect
- [ ] Face identity preserved throughout
- [ ] No motion deformities
- [ ] Captions don't block faces
- [ ] Last 2s has brand logo + explicit CTA

### Ad Failure Library

#### Existing Ad Failure Types

| Failure | Fix |
|---------|-----|
| Hook too slow | Move highlight shot to front |
| Selfie reversal weak | Add before/after split or wipe |
| Tutorial too long | Compress to 3 UI beats |
| Only 1 variant | Add 2+ different demos |
| IP risk | Remove protected IP/brand elements; use generic theme styling |
| Motion deformity | Reduce complexity |
| CTA weak | Fix last 2s to Logo + CTA |

#### Football Captain New Failure Types (2026-06-24)

| Failure | Description | Fix |
|---------|-------------|-----|
| vo_missing | Final export has BGM only, VO track missing | Normalize audio to 44100Hz stereo PCM WAV before mixing |
| vo_cutoff / vo_swallowed_word | Word endings cut off, especially skill name | Split VO by sentence, add 150-250ms silence pad after each clip, verify final MP4 |
| vo_visual_sync_mismatch | VO timing does not match app recording actions | Split UI VO into separate clips (Open Makaron / Pick Skill / Create), each adelay-aligned to visual action |
| bgm_over_vo | BGM masks VO consonants or word endings | BGM volume ≤ 0.12, duck under VO throughout |
| subtitle_safe_area_issue | Subtitle covered by app UI, face, or platform overlay | Alignment=8, FontSize=42, MarginV=80, Outline=4 |
| subtitle_vo_mismatch | Subtitle text does not match VO after script change | Subtitle and VO text locked to same source; when VO changes, check subtitles |
| asset_missing | Required asset not provided before packaging | Wait for all 4 assets (effect video + app recording + selfie + CTA) before entering packaging |
| audio_sample_rate_mismatch | TTS 24kHz mono MPEG v2 vs BGM 44.1kHz stereo causes silent VO | Always normalize both to 44100Hz stereo PCM WAV before mixing |

## Step 3: Deployment Deliverables

### Minimum Uploadable Asset

- **ad_9x16_main_15s.mp4** — 1 final 9:16, 12-15s ad video (this alone is the minimum uploadable unit)

### Campaign Setup Materials

- cover_frame.jpg
- caption_en.txt
- headline_en.txt
- CTA text

### Optional

- voiceover_en.txt
- subtitles.ass
- qc_final_video.md
- failure_log.csv
- Hook A/B variants (if A/B testing)

## Step 4: Metrics Feedback

After deployment, collect and write back:

| Metric | What it measures |
|--------|-----------------|
| Hook CTR | How many stopped scrolling |
| 3s View Rate | Viewer retention at 3s |
| 6s Hold Rate | Viewer retention at 6s |
| CTA Click Rate | Action conversion |
| Drop-off Points | Where viewers leave |
| QC-caused Rejections | Production failures that blocked deployment |

Write results into the running contract document. Compare against baselines from prior skill deployments.

## Running Baselines

Track deployed skills and their metrics. Use prior deployments as comparison baselines for new launches.

| Skill | Status | CTR | 3s View | 6s Hold | CTA Click |
|-------|--------|-----|---------|---------|-----------|
| Broadcast Candid | Deployed | _pending_ | _pending_ | _pending_ | _pending_ |
| K-Pop Stage | Deployed | _pending_ | _pending_ | _pending_ | _pending_ |
| Football Captain | Ad produced, bzz approved | _pending_ | _pending_ | _pending_ | _pending_ |

New deployments added to the baseline table after metrics collection.

## Football Captain Case — 2026-06-24

### Asset Status

| Asset | Status | Notes |
|-------|--------|-------|
| Effect video | ✅ Received | Football Captain 8s, 834×1112, 24fps |
| Before image | ✅ Received | Selfie, 1402×1122 |
| App recording | ✅ Received | 5.3s, 886×1920, 30fps — English UI required |
| Logo CTA | ✅ Received | Makaron brand animation, confirmed as reusable asset |
| Skill name | ✅ Confirmed | "Football Captain" |

### Ad Video Result

- **Output**: 13.6s, 1080×1920, H.264, full VO + BGM + subtitles + CTA
- **Status**: bzz confirmed OK ✅
- **Structure**: Hook (0-2.5s) → Selfie (2.5-4s) → UI Tutorial (4-8s, Open Makaron / Pick Football Captain / Create) → Effect Reveal (8-11s) → Logo CTA (11-13.5s)
- **VO**: "Everyone's posting their captain moment right now. All you need — one selfie. Open Makaron. Pick Football Captain. Create. Your version is waiting."

### Key Lessons Learned

1. **Audio normalization is mandatory**: TTS output (24kHz mono MPEG v2) + BGM (44.1kHz stereo) → ~mixed VO silently disappears. Fix: normalize both to 44100Hz stereo PCM WAV.

2. **Split VO by action, not by time**: UI tutorial VO (Open Makaron / Pick Football Captain / Create) must be 3 independent clips, each adelay-aligned to the corresponding visual action (~4.2s / ~6s / ~7s). Do NOT slide one long block.

3. **Prevent swallowed words**: Cut VO clips at silencedetect boundaries in sentence gaps, add 150-250ms silence pad after each clip, add 0.03s fade in/out.

4. **Subtitle safe area**: Alignment=8 (top), FontSize=42, MarginV=80, Outline=4 avoids platform/app UI covering subtitles.

5. **Subtitle/VO consistency**: When VO text changed from "Done" to "Create", subtitles needed no change (they cover Hook/Selfie/Reveal, not UI segment), but the check must always happen.

6. **Final export must be verified**: Before sending, confirm final MP4 has audible VO — not just BGM. If BGM-only, status is BLOCKED.
