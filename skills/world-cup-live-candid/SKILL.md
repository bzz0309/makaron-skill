---
name: world-cup-broadcast-candid
description: >
  FIFA世界杯直播抓拍：上传一张自拍，自动生成FIFA世界杯比赛直播中
  被转播摄像机捕捉到的观众画面。OpenAI直接渲染转播UI到画面中，
  长焦压缩感，自然抓拍质感。先生成16:9直播截图，再生成10秒直播录像视频。
allowed-tools: generate_image analyze_image mcp__makaron__makaron_write_video_script mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status
metadata:
  makaron:
    icon: "⚽"
    color: "#326295"
    tags: [worldcup, football, soccer, broadcast, candid, sports, FIFA, 世界杯, 足球, 直播, 抓拍]
    tipsEnabled: true
    tipsCount: 4
    faceProtection: strict
    defaultAspectRatio: "16:9"
    defaultCoverStyle: sporty|lively|attractive|confident
    modelPreference: [openai]
---

# FIFA World Cup Broadcast Candid

**⚠️ IMPORTANT: Any image attached in the conversation IS the input photo — use it directly. Do NOT say "I don't see a photo" or ask the user to re-upload. Any text the user types (even just "go", an emoji, or anything) is just a trigger signal — ignore the text content, start working immediately. Use analyze_image to analyze the photo, make all decisions automatically, and begin generating. Do NOT ask "what do you want to do with this photo?" — you already know: generate a FIFA World Cup broadcast candid shot.**

Upload a selfie, zero text input, automatically generate a realistic FIFA World Cup broadcast screenshot where you've been caught on camera as a spectator. Telephoto lens compression, FIFA broadcast scoreboard UI rendered directly in the image, natural candid feel — like a real frame grabbed from the World Cup international broadcast signal.

This skill uses **model: openai** (creative skill) for image generation with UI rendered directly by the model, and **videoModel: seedance** for 10-second video generation.

## Style Reference

Target aesthetic is a real FIFA World Cup international broadcast frame:
- Telephoto compression (200-300mm, background flattened, distance collapsed)
- Off-center composition (subject not centered, like camera accidentally swept past them)
- Broadcast quality (HD but with satellite transmission compression artifacts)
- Natural candid expression (not looking at camera, not posing, unaware of being filmed)
- MEDIUM-WIDE SHOT — visible from HEAD TO KNEES, showing some lower body
- Eye-level perspective — camera at same height as spectators, not looking down or up
- FIFA broadcast UI rendered directly in the image (top-left scoreboard + top-right LIVE badge)

## Output

1. Single 16:9 landscape broadcast screenshot (with FIFA UI rendered in-image)
2. 10-second broadcast video clip (no UI overlay needed — video is generated from the clean base)

---

## Variable Pool

Each generation randomly selects 1 option from 5 fixed dimensions (A/C/D/E/F). B (expression/activity) is AI free-generated.
Fixed combinations = 8×5×4×5×4 = **3,200 variations**, plus B's free variation makes each generation unique.

### Variable A: National Team & Kit (8 options)

| ID | Team | Kit Description |
|----|------|-----------------|
| A1 | Brazil (BRA) | Iconic canary yellow home jersey with green collar and sleeve trim, CBF crest on left chest, Nike swoosh on right, green shorts |
| A2 | Argentina (ARG) | Light blue and white vertical striped jersey, AFA sun crest on chest, three gold stars above crest, Adidas three stripes on shoulders, black shorts |
| A3 | Germany (GER) | White home jersey with black angular accents, DFB eagle crest, Adidas three stripes, black shorts |
| A4 | France (FRA) | Navy blue home jersey with subtle tricolor detail at collar, gold FFF rooster crest, Nike swoosh, white shorts |
| A5 | England (ENG) | White home jersey with navy blue trim at collar and sleeves, Three Lions crest on left chest, Nike swoosh, white shorts |
| A6 | Spain (ESP) | Vibrant red home jersey with subtle tonal pattern, RFEF crest on chest, Adidas stripes, navy blue shorts |
| A7 | Italy (ITA) | Azzurri blue home jersey with Renaissance-inspired subtle pattern, FIGC shield crest with tricolor, Adidas stripes, white shorts |
| A8 | Netherlands (NED) | Bright orange home jersey with lion watermark pattern, KNVB lion crest, Nike swoosh, orange shorts |

Random selection, no default bias. If user specifies a team, use that team.

### Variable B: Expression & Activity (AI Free Generation)

No fixed option pool. AI generates a natural, candid expression and activity based on the selected variables (team A, composition C, lighting D, background E, match stage F) and the user photo's vibe.

Possible directions (inspiration only, not exhaustive):
- Goal celebration (jumping up, arms raised, hugging stranger next to them, screaming)
- Penalty shootout tension (hands covering face, peeking through fingers, biting nails, clutching scarf)
- Face paint in national colors
- Waving national flag or scarf
- Holding beer/hot dog/popcorn
- Blowing vuvuzela/horn
- Clapping along with crowd chant
- Checking phone replay
- Disappointment after conceding (head in hands, slumped in seat)
- Standing ovation
- Singing national anthem
- High-fiving nearby fan
- Clenched fists staring intensely at the pitch
- Holding hand-written support banner

KEY CONSTRAINTS on expression/activity:
- Must look CANDID and UNAWARE of camera
- Expression should be natural and slightly imperfect (NOT model-pose)
- Activity should match the lighting/atmosphere and match stage
- Keep facial expression natural — no exaggerated grimaces
- Hands should be doing something natural

### Variable C: Camera Composition (5 options)

| ID | Composition |
|----|-------------|
| C1 | Medium-wide shot, subject off-center to the left at the 1/3 line, densely packed crowd visible on right edge, some national flags in background |
| C2 | Medium-wide shot, subject slightly right of center, left edge partially obstructed by a fan in front row waving a scarf or flag |
| C3 | Wider shot, subject at center-left, 3-4 other fans visible in frame, some standing some sitting, chaotic crowd energy |
| C4 | Medium-wide framing, subject nearly centered but one side partially cropped by person standing with arms raised in celebration |
| C5 | Subject caught at the edge of frame as if the broadcast camera was panning across the crowd section and accidentally captured them mid-sweep |

### Variable D: Lighting (4 options)

| ID | Lighting |
|----|----------|
| D1 | Night match — powerful white LED stadium floodlights from above creating crisp defined shadows, dark sky beyond the stadium roof structure |
| D2 | Late afternoon kickoff — warm golden sunlight streaming across the stands at a low angle, long shadows across the seats, blue sky visible |
| D3 | Enclosed/roofed stadium — even artificial lighting from translucent retractable roof, no harsh shadows, neutral clean white balance |
| D4 | Dusk/evening start — deep blue sky transitioning to dark, stadium lights at full power, atmospheric purple-blue ambient mixed with white LED flood |

### Variable E: Background Detail (5 options)

| ID | Background |
|----|------------|
| E1 | Sea of national team flags and banners held aloft, large tifo display visible in upper tier, coordinated colored clothing creating a wall of team color |
| E2 | Green pitch partially visible in background blur, goal net at an angle, LED advertising boards glowing with sponsor logos |
| E3 | Dense crowd with face paint in national colors, vuvuzelas, scarves held overhead, confetti remnants floating in the air |
| E4 | Modern FIFA-standard stadium with distinctive architectural roof structure visible, multiple tiers packed with 60,000+ fans, LED ribbon boards between tiers |
| E5 | Giant stadium screen showing replay visible in distant background, crowd around subject reacting to the replay, mixed emotions and pointing at the screen |

### Variable F: Match Stage (4 options)

| ID | Stage |
|----|-------|
| F1 | GROUP (random A-H) |
| F2 | ROUND OF 16 |
| F3 | SEMI-FINAL |
| F4 | FINAL |

---

## Workflow

### Step 1: Read Photo (Zero Input)

Read the user's uploaded photo directly, ask no questions.
- 1+ photos → take the first one as identity reference, proceed to Step 2
- 0 photos → request a selfie upload

### Step 2: analyze_image — Analyze Photo

Call `analyze_image` to analyze the user's selfie:

**Extract:**
- Gender (for kit description wording)
- Facial features: face shape, hairstyle, hair color, skin tone, distinctive features
- Skin texture (maintain consistency in prompt)
- Overall vibe (for AI free-generation of expression/activity)

### Step 3: Random Variables + Single generate_image (WITH UI RENDERED)

Randomly select 1 option from each of A/C/D/E/F. B is AI free-generated. Also randomly generate match data:
- Opponent team: random from remaining 7 teams (excluding selected home team)
- Home score: random 0-4
- Away score: random 0-4
- Match minute: random 1-90 (or 90+1 to 90+5 for added time)

**Single call to `generate_image`:**

- **model**: openai
- **skill**: creative
- **useOriginalAsReference**: true
- **aspectRatio**: 16:9

**Prompt Template:**

```
Generate a realistic FIFA World Cup 2026 broadcast screenshot. This must look like a frame captured from a live international football broadcast — NOT a posed photo, NOT a studio portrait, NOT an influencer shot.

FRAMING — CRITICAL:
- MEDIUM-WIDE SHOT — the person must be visible from HEAD TO KNEES (show some lower body, they can be wearing shorts/pants)
- Eye-level perspective — camera is at the SAME HEIGHT as the spectators, NOT looking down from above, NOT looking up from below
- The person and the crowd behind them must share the SAME perspective and angle — no mismatched viewpoints

The person from the reference photo is sitting/standing in the spectator stands of a massive 60,000+ capacity FIFA World Cup stadium. They are wearing a {A: kit description}. They may have face paint in their team's national colors on their cheeks.

EXPRESSION & ACTIVITY — AI FREE GENERATION:
Based on the stadium atmosphere and match stage ({F: match stage}) described below, invent a natural, candid expression and activity for this person. They are a real spectator at a World Cup match — think about what real football fans actually do during a high-stakes international match.

KEY CONSTRAINTS on expression/activity:
- Must look CANDID and UNAWARE of camera
- Expression should be natural and slightly imperfect (NOT model-pose)
- Activity should match the lighting/atmosphere and match intensity
- Keep facial expression natural — no exaggerated grimaces or overly dramatic reactions
- Hands should be doing something natural (holding something, clapping, resting, raised in celebration, etc.)

IDENTITY PRESERVATION — HIGHEST PRIORITY:
The person's face must be IDENTICAL to the reference photo. Same facial structure, same eyes, same nose, same mouth, same jawline, same skin tone, same hair. Do NOT beautify, smooth, enlarge eyes, slim jaw, or alter any facial feature. Preserve exact facial identity including all natural imperfections — visible pores, uneven skin texture, slight redness, oily shine, flyaway hair.

CAMERA & LENS:
{C: composition description}. Shot with a telephoto broadcast lens (200-300mm equivalent). Strong background compression — the massive crowd behind is flattened into a dense wall of people. Shallow depth of field — subject reasonably in focus, background slightly soft. Camera positioned from the opposite stand or broadcast gantry at EYE LEVEL. Subtle micro-jitter feel from handheld broadcast camera on a long lens.

BROADCAST REALISM:
- High-definition international broadcast quality, slight compression from satellite transmission
- Color grading matches international football broadcast — slightly warm, vivid but natural tones
- The person looks ACCIDENTALLY caught on camera — candid, not posed, not looking at camera
- Natural facial asymmetry preserved, visible skin texture, imperfect posture
- The stadium is MASSIVE — 60,000+ seats, this is the World Cup not a local league

LIGHTING: {D: lighting description}
STADIUM ENVIRONMENT: {E: background description}

BROADCAST UI OVERLAY — MUST BE RENDERED IN THE IMAGE:
In the TOP-LEFT corner of the image, render a broadcast scoreboard graphic with this EXACT layout (three stacked layers):

Layer 1 (top, purple/violet background bar): White text reading exactly 'FIFA WORLD CUP 2026' with '{F: match stage}' on the right side of this bar.

Layer 2 (middle, dark gray/navy background bar, directly below layer 1): Shows the match score. On the left side a small {home team} flag, then '{home team code}', then the number '{home score}', then a small football icon in the center, then the number '{away score}', then '{away team code}', then a small {away team} flag on the right.

Layer 3 (bottom, small dark strip below layer 2): Shows the match time '{match minute}:{random seconds 00-59}' centered.

Additionally, in the TOP-RIGHT corner, render a small red rectangle badge with white text 'LIVE'.

The UI elements should look like professional broadcast graphics overlaid on the camera feed — clean, sharp, semi-transparent dark backgrounds, white text, properly sized (not too large, not too small — roughly 15-20% of image width for the scoreboard cluster).

WHAT THIS IS NOT:
- NOT a beauty photo, NOT retouched, NOT an influencer shot
- NOT a magazine photoshoot, NOT a posed portrait
- NOT a different person — must be recognizably the same person from reference
- Do NOT add beauty retouching, enlarged eyes, V-line jaw, porcelain skin
- Do NOT add any Chinese text anywhere — all text must be in English
- Do NOT add any date stamps or year numbers outside of the scoreboard UI

Only ONE main subject (the user). Background crowd are anonymous blurred spectators only. No extra prominent characters.
```

### Step 4: analyze_image — Face Check

After generation, call `analyze_image` to check:
- Face matches reference photo? (features, hairstyle, skin tone)
- Only one main subject? (background is only blurred spectators)
- Has broadcast screenshot feel? (telephoto compression, off-center composition)
- FIFA UI rendered correctly in top-left? (3-layer scoreboard visible)
- LIVE badge in top-right?
- Medium-wide framing showing head to knees?

Fail → regenerate (max 1 retry).

### Step 5: Display Image + Immediately Generate Video Script

**⚠️ CRITICAL: After displaying the image, do NOT stop and wait for user reply. Do NOT list option menus like "you can: 1. Keep 2. Regenerate...". You MUST in the same response, after showing the image, immediately say "Generating video script..." and then call mcp__makaron__makaron_write_video_script. This is one continuous action, not two separate steps.**

**Video Script Generation Flow:**

1. Call `analyze_image` on the generated image to observe the person's current expression, activity, held items, body orientation
2. Based on the image state, construct a storyboard as userRequest

**Storyboard Template (10 seconds):**

```
Storyboard for FIFA World Cup broadcast camera shot, 16:9, 10 seconds, single continuous shot with no cuts:

This is a live international football broadcast camera capturing a spectator in the crowd. Telephoto lens (200-300mm) positioned from the opposite stand or broadcast gantry at eye level, zoomed into one section of the 60,000+ capacity stadium. MEDIUM-WIDE framing showing the person from head to knees.

[0-3s]: {Describe initial state based on analyze_image results — pose, expression, what they're holding, body position}. Minimal movement — natural breathing, slight head micro-movements, maybe bobbing to a crowd chant. Camera has subtle broadcast-quality telephoto micro-shake (long lens handheld feel). Background crowd has ambient movement (people shifting, flags waving gently, scarves moving).

[3-6s]: A match event triggers a shift — {natural transition from the initial state. Example: if relaxed → leans forward with intense focus; if already tense → springs to feet in celebration}. The crowd around them reacts in sync. Keep the reaction natural and genuine, not exaggerated or theatrical.

[6-9s]: Peak reaction — {the emotional climax. Example: jumps up with fist pump, hugs stranger, arms raised in celebration}. Full body energy, crowd explodes around them.

[9-10s]: Settling — {brief wind-down. Example: throws arm around neighbor, settles back, still buzzing}. Camera begins a very subtle slow drift as if the broadcast director is about to cut away.

CRITICAL CAMERA RULES:
- This is a BROADCAST CAMERA, not a cinematic camera
- Subtle telephoto micro-jitter throughout (not smooth gimbal) — amplified by the long 200-300mm focal length
- NO dramatic camera movements, NO cinematic pans, NO dolly moves
- The camera is essentially static with natural handheld vibration
- Shallow depth of field — subject sharp, massive crowd background slightly soft
- EYE LEVEL — same height as spectators

CRITICAL PERSON RULES:
- Face IDENTICAL to the image throughout — no morphing, no beauty filter
- Natural skin texture visible — pores, slight oil, imperfections
- Movement should be NATURAL — this is a candid shot, not a performance
- The person should NOT look directly at camera (they don't know they're being filmed)
- Keep expressions natural and understated — real human reactions, not acting
- The motion must feel like a CONTINUATION of the still image — same pose, same props, same clothing
- If holding any item (beer, flag, scarf, phone), keep it in hand throughout — do NOT drop or throw it
- Show from head to knees — maintain medium-wide framing throughout
```

**Call `mcp__makaron__makaron_write_video_script`:**
- **images**: [Step 3 generated image URL]
- **userRequest**: storyboard filled in based on analyze_image results
- **language**: "en"

Wait 1-2 minutes for script generation, then display to user:

```
🎬 Video Script Preview

Based on your World Cup broadcast screenshot, here's the video script (16:9, ~10 seconds):

{script content}

---
Options:
1. ✅ Confirm → Start video generation (~3-5 minutes)
2. ✏️ Edit → Tell me what to adjust
3. ⏭️ Skip → Keep only the image
```

**Wait for user reply:**
- User confirms → proceed to Step 6
- User requests changes → edit script, re-display
- User skips → end, keep image result

### Step 6: Generate Video

After user confirms the script:

**Call `mcp__makaron__makaron_create_video`:**
- **script**: the confirmed script content
- **images**: [same image URL from Step 3]
- **aspectRatio**: "16:9"
- **duration**: 10
- **videoModel**: "seedance"

After receiving the Task ID, inform user: "Video generating, estimated 3-5 minutes..."

**Poll `mcp__makaron__makaron_get_video_status`:**
- Poll every 15 seconds
- When status becomes `completed`, extract videoUrl

Display the final video to the user. No additional post-processing needed — the video is the final output.

---

## Tips Directions

1. **Brazil Fan**: Upload your selfie and become a passionate Brazilian fan caught on the World Cup broadcast camera. Wearing the iconic yellow jersey in a sea of 60,000 fans, the camera captures your raw celebration as the Seleção scores. Full FIFA broadcast UI with score and match clock.
2. **Penalty Shootout**: Knockout stage penalty shootout — the broadcast camera finds you in the crowd, hands over your face, peeking through your fingers. The tension is unbearable. Complete with FIFA score overlay and match clock showing 120+.
3. **Goal Celebration**: The camera catches you at the exact moment your team scores — jumping out of your seat, arms raised, pure ecstasy on your face. Strangers hugging, flags waving, confetti in the air. Full FIFA World Cup broadcast UI.
4. **World Cup Atmosphere Video**: Generate a 10-second broadcast clip — the camera finds you in a sea of 60,000 fans, flags and scarves everywhere. A crucial match moment unfolds and your natural reaction is captured live on international TV. Complete with FIFA broadcast scoreboard.

---

## Rules

1. **Single person skill** — Only generate one person (the user) in the stadium. Background crowd are anonymous blurred spectators only, no extra prominent characters.
2. **Face identity is #1 priority** — Must match the uploaded photo. No beautification, no skin smoothing, no eye enlargement, no jaw slimming. Visible pores, skin texture, natural imperfections. If not matching → retry (max 1 time).
3. **Zero-input workflow** — Start as soon as photo is uploaded, don't ask about team/scene/expression, all decisions are automatic. Only interaction point: video script confirmation.
4. **UI rendered by OpenAI directly** — The FIFA broadcast scoreboard (3-layer stacked: purple FIFA bar / dark score bar with flags / clock strip) and LIVE badge are rendered directly by the image model in a single generation pass. No post-processing overlay.
5. **16:9 fixed** — Broadcast frame format, never generate portrait or square.
6. **useOriginalAsReference: true** — All generate_image calls must set this.
7. **Telephoto lens feel is mandatory** — 200-300mm, background compression, shallow DOF, soft background. This is a distant zoom, not a close portrait lens.
8. **Medium-wide framing** — Show the person from head to knees. Eye-level perspective matching the crowd.
9. **Teams are random** — Each time randomly selected from 8 traditional powerhouses. If user specifies a team, use that team.
10. **Video is 10 seconds** — Duration must be 10 seconds, using seedance model.
11. **Video script must be confirmed by user** — This is the only step requiring user confirmation in the entire workflow.
12. **All text in English** — No Chinese text in the generated image. All UI text (FIFA WORLD CUP 2026, team codes, LIVE, etc.) must be in English.
13. **No illegal, hateful, or explicit content** — Maintain positive sports culture.
