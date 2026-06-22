---
name: bicycle-kick-hero
description: Create platform-neutral AI video prompts for a bicycle kick football highlight. Use when turning a portrait, lifestyle clip, or sports reference into a vertical World Cup-style overhead kick scene with identity preservation, ball cue, airborne contact, landing, and optional Makaron-ready output.
allowed-tools: analyze_image generate_image generate_video generate_music
metadata:
  makaron:
    icon: "football"
    color: "#16A34A"
    tags: [video, sports, football, soccer, bicycle-kick, world-cup, template]
    tipsEnabled: true
    tipsCount: 4
    modelPreference: [seedance, kling, gemini]
    defaultAspectRatio: "9:16"
---

# Bicycle Kick Hero

Use this skill to create a reusable AI video template for a football bicycle kick / overhead kick. The skill is platform-neutral and can output prompts for Makaron, Runway, Kling, Seedance, Gemini, Sora-style agents, other video agents, or a custom video pipeline.

## Core Motion

The action must be readable in five beats:

1. `setup_beat`: the person faces the camera or goal, takes two small steps, and shifts weight.
2. `ball_cue`: the football pops up from the ground, a pass, or a light juggle to chest height or above.
3. `action_ramp`: the person leans backward, jumps, twists, and opens the legs in a scissor shape.
4. `hero_contact`: the body is nearly horizontal in midair; the kicking foot strikes the ball above the head.
5. `result_beat`: the ball flies toward the top corner, the net ripples, and the person lands naturally or rolls sideways.

## Universal Prompt Template

```text
Use the uploaded image or video as the protagonist reference. Preserve the person's face, hairstyle, body proportions, clothing color, and overall attitude.

Create a {duration}-second 9:16 realistic sports commercial video in a dramatic football stadium. The scene has real turf, a visible goal, bright floodlights, and a World Cup final atmosphere.

Action: bicycle kick / overhead kick.
Beat 1: the protagonist faces the goal and takes two small adjustment steps.
Beat 2: the football pops up in front of the body to chest or head height.
Beat 3: the protagonist leans backward, jumps, and opens the legs in a scissor motion.
Beat 4: in short slow motion, the body is horizontal in the air and the kicking foot strikes the ball cleanly above the head.
Beat 5: the ball flies into the top corner of the goal, the net ripples, and the protagonist lands or rolls naturally.

Camera: low side-front tracking camera, slight push-in at contact, clear ball path. Keep one protagonist, one football, and one readable goal direction.

Avoid extra limbs, wrong head-foot direction, distorted face, floating body for too long, missing ball, ball not touching the foot, unreadable jersey text, real logos, subtitles, UI, and watermark.
```

## Makaron Marketplace

- Name: Bicycle Kick Hero
- Chinese name: 倒挂金钩
- Core promise: turn a portrait, lifestyle clip, or sports reference into a spectacular overhead kick goal.
- Default aspect ratio: 9:16
- Recommended duration: 5–8 seconds for image-to-video; 8–12 seconds for lifestyle-video conversion.
- Best cover moment: protagonist suspended horizontally in the air, foot striking the ball above the head.

## Makaron Chinese Prompt

```text
使用上传的素材作为主角参考。保持主角的脸部特征、发型、身材比例、服装主色和整体气质稳定，不要换人。

生成一段{duration}秒、9:16竖版、高清真实体育广告风格视频。场景转化为夜晚职业足球场：真实草坪、清楚球门、观众席、强烈球场灯光、世界杯决赛般的紧张氛围。不要出现真实赛事logo、真实队徽、赞助商文字或水印。

动作主题：倒挂金钩。
动作分为五段：
1. 主角面向球门或镜头前小跑，两步调整重心。
2. 足球从前方弹起或被主角轻轻挑起，升到胸口以上。
3. 主角后仰起跳，身体开始横向腾空，双腿剪刀式展开。
4. 触球瞬间短暂慢动作：主角身体横在空中，主力脚越过头顶击中足球，足球与脚接触清楚。
5. 足球飞向球门上角，球网震动，主角自然落地或侧身翻滚。

镜头：低机位侧前方跟拍，触球瞬间轻微推近，足球轨迹清晰，身体姿态有力量感。全程保持一个主角、一个足球和清楚的球门方向。

负面要求：不要头脚方向混乱、不要多余腿或手、不要人物悬空过久、不要足球不接触脚、不要畸形手脚、不要脸部漂移、不要球衣乱码文字、不要真实品牌logo、字幕、UI界面、水印。
```

## Stabilization Notes

- Use a defender-free shooting zone unless the user explicitly asks for defenders.
- Keep the ball visible before the jump; a sudden ball appearing at contact is unstable.
- Prefer low side-front camera over frontal camera, because the horizontal body shape is easier to read.

## Quality Checks

- The ball is visible before the kick.
- The body orientation is understandable: head lower, kicking foot above the head, torso horizontal.
- The contact moment clearly shows foot-to-ball contact.
- The result shows a physical payoff: ball path, goal, net ripple, landing.
- If the model struggles, simplify to no defenders and a low side-front camera.
