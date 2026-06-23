---
name: makaron-location-food-popin
allowed-tools:
  - generate_video
  - analyze_image
metadata:
  makaron:
    icon: "📍"
    color: "#F97316"
    tags:
      - food
      - location
      - reveal
      - popin
      - checkin
      - transition
    faceProtection: default
    defaultAspectRatio: "9:16"
    models:
      - seedance
      - seedance-fast
      - kling
      - grok
---

# Location Food Pop-in — 地点打卡 + 食物弹出

同一个角色在不同城市打卡，每地点换装+不同食物+不同动作，节拍切换。
**视频模型单次生成**。Agent 不得改写 prompt 模板。

## Core Concept

多城街头打卡，每处 2–3s。环境切换→角色摆 pose→食物弹出→表情反应。不是滑动转场，是节拍 match-cut。**所有角色在画面上进行的是"拿取/接住/捧起/咬"食物这个行为——食物不是凭空浮在手上的。**

## Input

### 用户必传

| 输入 | 说明 |
|------|------|
| 人物图 | 1 张 reference image |
| locations | 2–5 个地点，JSON 数组 |

### 每 location schema（用户/Agent 填入具体值）

```json
{
  "location_name": "Shinjuku ramen alley at night, red lanterns, steam",
  "food_item": "steaming tonkotsu ramen in a black bowl, chopsticks",
  "outfit": "black zip-up jacket, black tee, AirPods",
  "action": "holds the ramen bowl with both hands, lifts it toward camera, grins",
  "hold_mode": "two_hands_bowl",
  "duration_s": 2
}
```

| 字段 | 必填 | 说明 |
|------|:--:|------|
| `location_name` | ✅ | 城市+地点+氛围 |
| `food_item` | ✅ | 食物描述 |
| `outfit` | ✅ | 本地点穿什么 |
| `action` | ✅ | 拿取/接住/捧起/咬食物的具体动作（不是微笑/比耶） |
| `hold_mode` | ✅ | palm / two_hands_bowl / plate / cup / wrap |
| `duration_s` | ✅ | 2 或 3，总时长 6–12s |

## Safety

- ✅ 食物：拉面、甜点、小食、水果、饮料、街头小吃
- ❌ 武器、危险品、人体部位、性暗示、品牌logo、地图UI、店招牌、评分

## Budget

| 轮次 | 模型 |
|:--:|------|
| 1 | seedance / seedance-fast |
| 2 | kling |
| 3 | grok |

三轮全败 → BLOCKED。总次数 ≤ 3。

## Workflow

### Step 1 — 验证

- 人物图 + locations 完整
- 所有 location 六字段不缺
- food_item 通过安全白名单
- 总 duration = 各位置 duration_s 之和

### Step 2 — 分析人物

`analyze_image` → face + build 描述。Agent 从结果中仅提取外貌特征用于 prompt（如：发型/肤色/五官），不提取具体品牌标签。

### Step 3 — 组装 prompt（❌ 禁止修改模板）

Agent 读取下方 prompt 模板并逐位填入变量。**不得翻译成中文、不得改写句式、不得增删段落。**

```
Vertical 9:16 video, single SeeDance generation, no manual stitching. Vibrant colors, city natural light, beat-sync match-cuts between locations.

Character: same person throughout — [FACE], [BUILD]. Outfit changes per location.

[SCENE 1 — {dur}s] Mid-shot. Environment: {location_name}. Character wears {outfit}. {action}. Hold mode: {hold_mode}. {food_item}. Beat cut white flash. Transition to next.

[SCENE 2 — {dur}s] Mid-shot. New environment: {location_name}. Same character identity. Character now wears {outfit}. {action}. Hold mode: {hold_mode}. {food_item}. Beat cut white flash. Transition to next.

[SCENE 3 — {dur}s] Mid-shot. New environment: {location_name}. Same character identity. Character now wears {outfit}. {action}. Hold mode: {hold_mode}. {food_item}. Beat cut white flash. End.

Style rules: 9:16 vertical. Natural hands with 5 fingers, no deformation. Face identity consistent across all locations — same person. Food makes realistic contact with hands — gripping, holding, lifting, not floating. Each location visually distinct: different city, different outfit, different food, different action. No brand logos, no map UI, no store signage, no ratings, no text overlay.
```

**赋值规则**：
- [FACE]: from analyze_image output, concise keywords only
- [BUILD]: from analyze_image output, concise keywords only
- {dur}: location 的 duration_s 值 + "s"
- 其余 {变量}: 从 locations JSON 里逐字段填入
- 3 locations = 拼 3 个 SCENE 段落；5 locations = 拼 5 个
- **不得修改模板的任何固定文字，不得翻译成其他语言，不得添加 Sound/音乐描述**

### Step 4 — 单次视频生成

`generate_video(model, prompt, reference_image, 9:16, total_duration)`

### Step 5 — QC

| Outcome | 条件 | 动作 |
|---------|------|------|
| PASS | identity一致、手自然、食物接触合理、地点可区分、动作不重复 | 交付 |
| REROLL | 脸漂移、手变形、食物浮空、地点太像（max 2 次，按 budget 表换模型） | Retry |
| BLOCKED | 3 轮全败、identity 丢失、违禁内容 | 通知 human |

## 输出

- `location_food_popin.mp4`（9:16）
- `prompt_used.md`
- `qc_report.md`
