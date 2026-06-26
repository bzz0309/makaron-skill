---
name: cinema-short-drama-trailer-diverse
description: >
  Generate diverse TikTok-style vertical short-drama trailers from character photos.
  Use this when the user wants a Makaron/Seedance short-drama concept, storyboard,
  or 15-second trailer that adapts to each uploaded photo instead of reusing one plot.
allowed-tools: analyze_image Bash mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status
metadata:
  makaron:
    icon: "📺"
    color: "#FF2222"
    tags: [trailer, short-drama, tiktok, diverse, storyboard, seedance]
    defaultAspectRatio: "9:16"
    videoModel: seedance
---

# Diverse Cinema Short Drama Trailer

Create a premium **15-second vertical TikTok short-drama trailer** from the user's photo. Do **not** reuse one fixed story structure. Every new photo should drive a different genre, hook, setting, and twist.

If the user provides a photo, treat it as the main character reference. Do not ask them to re-upload.

## Non-Negotiable Rules

- Default video: `15s`, `9:16`, `seedance`.
- No Chinese visible text, subtitles, or dialogue unless the user explicitly asks for Chinese.
- All visible text, titles, and spoken lines should be English by default.
- Avoid small readable text in generated video: phone screens, contract text, document labels, neon signs, UI, subtitles, and long title cards often misspell.
- Do not force every story into billionaire revenge, courtroom reveal, gala betrayal, or missing-heiress logic.
- If the previous generated concept is known, avoid repeating its genre, key scene set, core betrayal, and final reveal.
- Keep the character adult when the reference appears adult; do not sexualize minors or uncertain-age subjects.
- Every video must be understandable on first watch. Visual style is secondary to clear cause-and-effect.
- Do not overpack 15 seconds with too many plot points. Prefer 5-7 clear beats over 10-12 confusing beats.
- The trailer must clearly answer: who is in danger, why they are in danger, what deal/secret changes the situation, and what the final cliffhanger is.
- Include one strong English hook line that explains the premise, not just mood.
- Before generating video, self-check the script for clarity and excitement. If clarity is below 7/10, simplify before rendering.

## Workflow

### Step 1: Photo-Driven Character Read

Analyze the photo for:

1. apparent age category: adult / uncertain
2. face energy: innocent, cold, fierce, soft, mysterious, comic, elite, wounded, rebellious
3. styling: casual, luxury, office, school-like, street, gothic, bridal, athletic, vintage
4. implied world: city, mansion, campus, small town, nightlife, hospital, police, fantasy, workplace
5. strongest usable hook: secret identity, betrayal, forbidden love, danger, comeback, accusation, rescue, supernatural bond

Write a one-line character archetype from the analysis before choosing the story.

### Step 2: Choose a Different Genre Lane

Pick the lane that best fits the photo and avoids repeating the previous concept.

Use this diversity rule:

- Do not reuse the same lane twice in a row.
- Do not reuse more than one major set piece from the last concept.
- Change at least two of these every time: relationship dynamic, secret, main location, threat type, final reveal.

Genre lanes:

1. **Missing Heiress Revenge**  
   Fits cold luxury looks. A real heiress was erased; an impostor takes her place; she returns with proof.

2. **Mafia Contract Romance**  
   Fits intense gaze, nightlife styling, black outfits, dangerous glamour. A witness signs a fake marriage or protection deal with a mafia heir.

3. **Bodyguard Forbidden Love**  
   Fits soft but guarded faces, celebrity/influencer styling, vulnerable energy. A bodyguard protects the lead while hiding the threat.

4. **Campus Power Reversal**  
   Fits youthful adult college styling. A scholarship girl is humiliated, then revealed as powerful. Use only if clearly adult.

5. **Small-Town Secret Return**  
   Fits candid, natural, nostalgic looks. The lead returns to a small town and exposes an old crime or hidden child.

6. **Crime Witness Thriller**  
   Fits serious urban realism. The lead witnesses a crime, but the detective/lover/fiance may be involved.

7. **Vampire / Werewolf Romance**  
   Fits gothic, dramatic, fantasy energy. The lead discovers a supernatural bond or bloodline.

8. **Medical Secret Baby Drama**  
   Fits gentle mature romantic looks. A child, diagnosis, or pregnancy secret collides with a powerful ex.

9. **Workplace Double Identity**  
   Fits polished office styling. The lead enters as an assistant/intern while secretly owning, auditing, or investigating the company.

10. **Royal / Noble Impostor**  
   Fits elegant, bridal, formal, fantasy-luxury styling. The lead is mistaken for a servant/impostor but is the lost royal heir.

### Step 3: Build a Clear Trailer Logic

Every trailer needs a causal chain, not just vibes:

```text
incident -> immediate danger -> deal/secret -> proof/twist -> emotional reversal -> cliffhanger
```

If the chain cannot be explained in one sentence, the story is too complex for a 15-second trailer.

Recommended 15-second structure:

1. **0-3s**: immediate incident.
2. **3-6s**: danger and protective/deal hook line.
3. **6-10s**: one location shift proving the stakes.
4. **10-13s**: twist or attack.
5. **13-15s**: emotional reversal and title/no-title ending.

### Step 4: Pre-Render Quality Gate

Before generating final video, rate the trailer:

- **Clarity**: Can a first-time viewer understand the basic plot without reading a description?
- **Hook strength**: Is there one memorable line or situation in the first 4 seconds?
- **Causal logic**: Does each beat cause the next?
- **Emotional turn**: Does the protagonist's feeling visibly change?
- **Text risk**: Are there any small words that may become misspelled?

Automatic rejection rules before rendering:

- **Unreadable text risk**: reject phone screens, contracts, neon signs, documents, or UI with small/long readable text. Use blank pages, abstract seals, props, or spoken dialogue instead.
- **Face visibility risk**: reject any key character shot where the face is backlit, silhouetted, hidden, or too far away.
- **Over-obvious villain risk**: if the twist is "the killer is inside the family/group," do not use a masked attacker. Use an elegant unmasked insider whose face is visible.
- **Unrealistic clue risk**: clues should not be cartoonishly obvious. A bloody cufflink should have only a tiny dark red stain in an edge groove, not a large visible blood smear.
- **Vehicle motion risk**: avoid complex car chase or exterior driving shots unless necessary. Generated video may reverse direction or make cars move strangely. Prefer a parked car interior on a rainy street for dialogue/deal scenes.
- **Contract clarity risk**: if a contract matters, show the action through props and dialogue: ring + blank sealed page + hook line. Do not rely on readable contract text.
- **Too-many-beats risk**: reject any 15-second script with more than 7 major story beats unless the user explicitly wants a montage.

When a prior generation has user-reported issues, carry those fixes forward as hard constraints in the next prompt.

### Step 5: Pre-Video Assets

If the user asks for pre-production assets, create:

- character turnaround: front / side / back / close-up
- scene bible: 3-4 key locations with visual tone
- 12-panel storyboard: clear panels with motion/camera arrows

For storyboard planning:

- P01 immediate hook
- P02 confrontation
- P03 hook line close-up
- P04 secret clue
- P05 public pressure or chase
- P06 antagonist move
- P07 protagonist action
- P08 message/object reveal
- P09 location shift
- P10 proof exposed
- P11 protagonist reversal
- P12 title/no-title ending

Important: a storyboard can contain 12 panels for planning, but the final 15-second video should usually merge them into fewer, clearer moments.

### Step 6: Seedance Prompt Format

Build the final prompt as one paragraph or compact beat list:

```text
Premium vertical TikTok short-drama trailer. High saturation, cinematic color grading, fast-cut but readable suspense editing. No Chinese text. No Chinese subtitles. No Chinese dialogue. English dialogue only. Avoid small readable in-scene text. Use <<<image_1>>> as the visual reference for [character]. 0-3s: [incident]. 3-6s: [danger + hook line]. 6-10s: [stakes location]. 10-13s: [twist/attack]. 13-15s: [emotional reversal + title/no-title ending].
```

## Output Order

When user gives a new photo and asks for a trailer:

1. Character archetype
2. Chosen genre lane and why it fits
3. Core logic chain
4. English title and 2-3 hook lines
5. If requested: Makaron image prompts for character/scene/storyboard
6. Pre-render quality self-check
7. Final Seedance video prompt

If the user asks to generate immediately, use Makaron tools/CLI directly after constructing and self-checking the prompt.
