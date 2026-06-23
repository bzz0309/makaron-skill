---
name: ai-world-cup
description: >
  Create cinematic AI World Cup football/soccer sports-ad videos from a prompt,
  photo, or reference images. Use for night stadium action, macro ball shots,
  dribble breakthroughs, goal/net moments, aerial stadium shots, and epic
  football-world concept videos with Makaron-ready prompts.
allowed-tools: analyze_image generate_image generate_video generate_music
metadata:
  makaron:
    icon: "football"
    color: "#23C552"
    tags: [video, sports, football, world-cup, commercial, template]
    tipsEnabled: true
    tipsCount: 4
    modelPreference: [seedance, kling, gemini]
    defaultAspectRatio: "9:16"
---

# AI World Cup / AI 世界杯

把用户的一张图、几张参考图或一句主题,做成电影级足球世界杯感短视频:夜晚大型球场、强烈灯光、湿润草坪、运动员高速突破、足球飞行、门网震动、观众席虚化、广告大片质感。默认输出不是教程截图或提示词卡片,而是一支可发布的 9:16 竖屏体育商业短片。

## 默认输出

- 9:16 竖屏视频,建议 8-12 秒。
- 4-6 个镜头,每个 1-2.5 秒,节奏从国际大赛氛围到突破爆发。
- 风格:超写实、体育广告、电影级、高对比、冷蓝/青蓝/冷白球场灯、湿润草坪反光、薄雾、逆光轮廓光、轻微镜头眩光、动态抓拍。
- 可加低音量史诗/电子/鼓点 BGM;可加踢球、草屑、球网、观众低频欢呼等音效。
- 如果要标题,优先后期叠加 `AI WORLD CUP` 或用户指定标题;不要依赖视频模型生成准确文字。

## 重要原则

- 不要生成手机界面、绿色描边框、播放按钮、`输入图/成片/提示词` 字样,除非用户明确要复刻教程页面。
- 不要使用 FIFA、世界杯官方标志、真实国家队徽、真实球员肖像或受保护赞助商标,除非用户提供并明确授权。可以使用虚构队徽、抽象胸章和球衣号码来增强真实比赛感,但不能清晰复刻真实标志、品牌或赞助商。
- 默认使用「族裔自动匹配球队配色」:系统识别人脸族裔,自动分配主角国家队球衣配色,对手自动选对比色。族裔识别不确定时默认日本队 🇯🇵。主角和对手必须来自不同国家配色,不能同色同队。
- 如果出现球衣号码,先为主角选择一个固定号码,范围 1-99,默认可用 10 或 11。全片主角号码必须一致,不要在不同镜头从 0 变成 8、10、19 等;不要使用 0 号。对手也可有 1-99 号码,但不能和主角身份混淆。
- 足球必须是清晰球体,不能变形、融化或多出奇怪纹理;球员肢体必须合理,避免多腿、多手、断脚、错位球鞋。
- 画面焦点要明确:每个镜头只服务一个主体动作,例如球、脚、门将、突破者、球网或球场俯瞰。
- 运动感来自真实动线:球飞向镜头、球员向前突破、门将横向扑救、镜头低位跟拍、航拍快速俯冲。不要只做静态海报微动。
- 如果使用人像参考,参考图只影响主角的发型、气质和大致脸型;视频镜头仍必须服务比赛动作。除非用户明确要求,不要插入单独的人脸大特写、时尚硬照特写、凝视镜头或 MV 式肖像 cutaway。主角镜头应优先是半身/全身带球、低机位盘带、突破、射门、庆祝等动作镜头,足球或比赛动作要持续可见。
- 人像输入可以是男性、女性或非明确性别人物。默认保留上传人物的性别表达:女生照片生成女性足球运动员主角,男生照片生成男性足球运动员主角;不要把女性主角改成男性,也不要把女性角色做成性感摆拍、短裙、露肤写真或时尚 MV。所有主角都穿专业足球装备,镜头语言保持竞技、力量和比赛动作。
- 如果上传人物呈现为女性,默认生成女子足球比赛:主角、对手、防守者、门将和其他可见球员都应是女性足球运动员。除非用户明确要求混合性别比赛,不要让女性主角对抗男性球员。

## 工作流

### Step 0: 可选黑白 12 帧分镜预览

如果用户想先确认镜头逻辑,或任务涉及多镜头视频,先进入 Storyboard Mode:输出一张 12 帧黑白速写电影故事板,而不是直接生成成片。故事板用于确认节奏、动作和镜头衔接,不追求最终脸部精修。

Storyboard Mode 规则见 [references/storyboard-mode.md](references/storyboard-mode.md)。确认故事板后,再用同一 12 镜头结构进入 Makaron/Seedance/Kling 视频生成。

### Step 1: 判断输入

如果用户上传图片:
- 把图片作为风格/构图/主体参考,而不是直接照抄截图 UI。
- 如果是球员/球鞋/足球/球场图,保留主体颜色、机位和氛围。
- 如果是非足球图片,抽取色调、人物姿态或地点气质,再转换为足球大片场景。

如果用户只给主题:
- 默认做一支"AI 世界杯预告片":太空或城市球场开场 -> 国家队配色主角带球启动 -> 突破对抗 -> 射门/入网高潮 -> 结尾灯光、旗海和草坪粒子。

### Step 1.5: 选择国家队配色(族裔自动匹配)

首次用户不需要写 prompt,系统自动根据人脸族裔匹配主角球衣配色,对手自动选对比色。

**优先级:**
1. 用户明确指定球队 → 用指定球队
2. 用户未指定 → 识别图片中人脸族裔,按配色表自动匹配主角球衣
3. 族裔识别不确定 / 无图片参考 → **默认日本队 🇯🇵**

## 球队配色表

| 族裔 | 主角国家队 | 主角球衣 | 对手球衣(自动对比) |
|------|----------|----------|-------------------|
| 东亚脸 | 日本 🇯🇵(默认) | 深海军蓝 + 白边 | 白 + 红 |
| 东亚脸 | 韩国 🇰🇷 | 红 + 白 | 白 + 蓝 |
| 欧美脸 | 巴西 🇧🇷 | 黄 + 绿边 | 白 + 黑 |
| 欧美脸 | 阿根廷 🇦🇷 | 蓝白条纹 | 黑 + 白 |
| 欧美脸 | 英格兰 🏴 | 白 + 深蓝 | 红 + 蓝 |
| 欧美脸 | 法国 🇫🇷 | 深蓝 + 金边 | 白 + 黄 |
| 非洲脸 | 非洲 🌍 | 绿 + 黄 | 白 + 黑 |
| 中东/南亚 | 通用 | 白 + 绿 | 红 + 黑 |

可替换组合:Spain vs Germany、Brazil vs Spain、France vs England、Argentina vs Netherlands、Portugal vs Spain。

只使用颜色和球衣结构,不生成官方徽章、真实国旗细节、赞助商、品牌 logo、可读球衣文字或真实队标。允许虚构队徽、抽象盾牌胸章和固定球衣号码增强国家队氛围,但要避免可识别真实标志。观众席可出现抽象色块旗海,例如 yellow-green crowd waves、red-yellow crowd colors,但不要写清晰文字。

### Step 2: 选镜头结构

优先从下面结构中选 4-6 个镜头:

1. **Establishing**: 夜晚环形体育场航拍、球员通道入场、抽象国家色旗海、球场灯光从云层中亮起。不要默认出现奖杯。
2. **Build-up**: 主角穿国家队启发式球衣带球启动、赛前通道冲出、湿草坪与足球短特写。只允许快速 first touch 或球滚过脚边,不要重复"球鞋踩住球/压球"的画面。
3. **Acceleration**: POV 边路突破、侧面低机位盘带、两名防守者包夹。对抗必须是可读的一对二压迫,不要变成多人乱挤、摔跤、拉扯成团。
4. **Impact**: 足球被大力抽射、球在空中旋转靠近镜头、门将腾空扑救。
5. **Payoff**: 球撞入球网、网绳拉伸、草屑和水雾飞散、观众席成为虚化光海。
6. **Hero End**: 球入网后的网绳回弹、灯光爆发、主角在禁区外或远处减速庆祝,可后期加标题或品牌字。不要让主角突然瞬移到球门线、球门里面、网前正中央或门框旁;最后一幕的人物位置必须延续前面射门动线。不要用纯脸部大特写作为转场或结尾。

详细镜头配方见 [references/scene-recipes.md](references/scene-recipes.md)。需要 Makaron/CLI 交付时读 [references/makaron-agent.md](references/makaron-agent.md)。

### Step 3: 生成关键图或直接视频

若工具支持"图生视频",先生成每个镜头关键图,再做视频化,稳定性最高。关键图 prompt 使用:

```text
Cinematic sports commercial frame, night mega football stadium, [SHOT ACTION],
clear subject focus, wet green turf, cold blue and white floodlights, strong
rim light, shallow depth of field, subtle mist, grass particles, realistic
motion energy, ultra realistic, high contrast, premium football advertising,
8K detail. No text, no UI, no logos, no watermark.
```

若工具支持一次性长视频,使用:

```text
Create a 9:16 cinematic AI World Cup football commercial video, 8-12 seconds,
made of 4-6 fast connected shots. Use clear international tournament signals:
abstract country-color crowd waves, generic national-team-inspired kits, a
grand night stadium, confetti, floodlights, player tunnel entrance, and wet
turf. Do not place any trophy in the sky or floating above the stadium. If a
trophy is requested, it must be physically grounded on a pedestal, held by
players, or shown only after the match celebration. Preserve the uploaded
person's gender expression. Choose one fixed jersey number for the protagonist
from 1-99, preferably 10 or 11, and keep that same number across the whole video;
never use jersey number 0 or change the protagonist number between shots. The
protagonist wears a Brazil-inspired yellow jersey with blue shorts and green
trim; opponents wear Germany-inspired white kits with black trim. Fictional
crest shapes and jersey numbers are allowed, but do not use official crests,
real flags, brand logos, sponsors, readable jersey text, or protected marks.
Start with an epic stadium or football-earth establishing shot, cut to the
protagonist already sprinting with the ball in national colors, then a low-angle
dribble breakthrough between differently colored defenders, then a powerful shot
toward goal, ending with the ball hitting the net, the net rippling, and the
protagonist remaining outside the goal area or slowing in the distance along the
same attack path. Do not place the protagonist suddenly in front of the goal,
inside the goal, or next to the net in the final shot.
Ultra realistic sports advertising style, dynamic camera movement, strong speed
and pressure. Keep the ball and football action visible through the middle of
the video. No isolated face close-up, no beauty portrait cutaway, no fashion
editorial stare shot. No phone UI, no prompt cards, no readable logos, no
watermark, no subtitles.
```

### Step 4: 视频运动指令

给视频模型的动作描述要写清楚"相机怎么动、球怎么动、球员怎么动":

- 低机位跟拍:camera tracks beside the player at knee height, fast forward motion, turf streaks past lens.
- POV 突破:first-person sideline dribble, hands and legs in foreground, defender closing in, ball kept tight under foot.
- 门后入网:behind-the-goal camera through the net, ball strikes net, net stretches toward camera, goalkeeper dives too late.
- 航拍俯冲:aerial camera dives from clouds toward a glowing stadium, city lights streak outward.
- 足球短触球:quick first touch or rolling ball insert, water droplets and grass blades visible, shallow focus. Use only as a very short insert. Avoid repeated cleat-pressing-on-ball shots; at the shot-preparation moment, show the plant foot landing beside the ball and the kicking leg swinging back, not the foot stepping on the ball.

### Step 5: 音乐和剪辑

- BGM:cinematic sports trailer drums, stadium bass, electronic pulse, no vocals.
- SFX:kick thump, boot scrape, net snap, crowd swell, whoosh transitions.
- 剪辑节奏:前 2 秒铺垫,3-7 秒加速,最后 1-2 秒入网/灯光爆发。
- 如需品牌/标题,后期加干净无衬线白字;不要让生成模型直接写复杂中文。

## 质检

交付前检查:
- 视频没有手机 UI、提示词卡片、播放按钮、绿色边框。
- 球、脚、门、网、草坪线条合理;没有畸形肢体和多个球混乱。
- 至少一个镜头有明确高速运动,至少一个镜头有足球近景,至少一个镜头有进攻/进球高潮。
- 主角和对手的球衣颜色必须明显不同，并且看起来像国际大赛国家队配色。族裔识别不确定时默认日本队 🇯🇵 主角配色。
- 球衣可以有虚构队徽和号码,但不能有真实官方标志、真实队徽、品牌 logo、赞助商或可读版权文字。主角号码如出现,必须固定为 1-99 的同一个数字;不要出现 0 号或跨镜头换号。
- 进球后的结尾必须延续射门动线:球在网里、门将扑救落地、主角在禁区外或远处庆祝。不要让主角突然站在球门前、球门内、网前或门线附近。
- 中段 3-7 秒不能突然切到纯人脸大特写;如果出现主角脸,必须仍能看出他在带球、突破、射门或庆祝的比赛语境。
- 上传女生照片时,主角必须保持女性足球运动员表达,穿专业球衣球裤和球袜;禁止性感化、写真化或变成非竞技服装。
- 上传女生照片时,所有可见对手、防守者和门将也应是女性足球运动员;禁止默认生成男足球员作为对手。
- 多人对抗应是 controlled physical pressure:一名防守者封路线,一名从侧后方追防,主角带球从夹防中突破。不要 scramble、pile-up、wrestling 或无序拉扯。
- 色调统一:夜晚球场、冷色灯、湿草坪、高反差。不要变成卡通、低清新闻画面或普通训练场。
- 若使用参考图,只继承构图/气氛/颜色;不要复刻截图里的 app 页面。
