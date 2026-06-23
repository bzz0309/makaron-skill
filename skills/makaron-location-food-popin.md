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

# Location Food Pop-in — 地点打卡 + 伸手 + 食物弹出

同一个角色在不同地点打卡，每地点独立 outfit + action + food + hold_mode，节拍切换，食物弹出。
**视频模型单次生成**，不逐帧拼接。Agent 读本 SKILL.md 即可执行。

## Core Concept

```
Location A: environment A + outfit A + action A → beat cut → food A in hold_mode A
Location B: environment B + outfit B + action B → beat cut → food B in hold_mode B
Location C: environment C + outfit C + action C → beat cut → food C in hold_mode C
```

每 stop ~2s。3–5 地点 = 6–10s。节拍感 match-cut。

## Input — Per Location Schema

```json
{
  "location_name": "Shinjuku ramen alley at night, red lanterns",
  "food_item": "steaming tonkotsu ramen in a black bowl, chopsticks on top",
  "outfit": "black bomber jacket over white tee, silver chain",
  "action": "reaches both hands toward camera, ramen bowl materializes into both hands, lifts it toward lens with a grin",
  "hold_mode": "two_hands_bowl"
}
```

| 字段 | 必填 | 说明 |
|------|:--:|------|
| `location_name` | ✅ | 地点+氛围描述 |
| `food_item` | ✅ | 食物外观描述（需通过安全白名单） |
| `outfit` | ✅ | 本地点穿着（可与前面不同） |
| `action` | ✅ | 本地点动作+反应，每地点不同避免模板 |
| `hold_mode` | ✅ | palm \| two_hands_bowl \| plate \| cup \| wrap |

2–5 个 location，推荐 3–4。

## Safety（Agent 强制执行）

食物白名单 — 仅以下类别可通过：
- 热食：拉面/乌冬/米饭/炒面/饺子/寿司/天妇罗/咖喱/汉堡/披萨/烤肉/火锅
- 小食：鲷鱼烧/可丽饼/章鱼烧/铜锣烧/薯条/炸鸡/甜甜圈/饼干
- 甜点：冰淇淋/圣代/蛋糕/布丁/马卡龙/棉花糖/刨冰/巧克力
- 水果：西瓜/菠萝/草莓/橘子/苹果/香蕉/芒果/葡萄
- 饮品：奶茶/果汁/咖啡/汽水/奶昔/冰沙

拒绝区（自动 BLOCKED）：
- ❌ 武器（刀枪棍棒）、危险品、易燃物
- ❌ 人体部位、血液、器官
- ❌ 性暗示手势或姿势
- ❌ 真实品牌 logo / 品牌包装（KFC / McDonald's / Starbucks 等）
- ❌ 真实店招牌、Google/Apple Maps UI、评分星星、推荐文案
- ❌ 未成年人 + 任何暗示性手势 → 直接 BLOCKED

Identity：face 一致，outfit 每地点独立可变。

## Budget（写死）

| 轮次 | 模型 | 说明 |
|:--:|------|------|
| 1 | seedance / seedance-fast | 主生成 |
| 2 | kling | reroll 1 |
| 3 | grok | reroll 2 |

主生成 1 次 + reroll 2 次 = 最多 3 次尝试。三轮全败 → BLOCKED，通知 human。

## Workflow（Agent 自动化）

### Step 1 — 验证输入
- 人物参考图 ≥ 1 张（必填）
- locations ≥ 2，≤ 5
- 每个 location 六字段完整（location_name / food_item / outfit / action / hold_mode）
- 所有 food_item 通过食物白名单 → 否则拒绝并提示

### Step 2 — 分析人物参考

`analyze_image(person_reference)` → 提取：

```
Face: [性别 / 发型 / 五官特征]
Build: [体型 / 身高比例]
```

（outfit 不在人物常量里 — 每 location 独立指定）

### Step 3 — 组装视频 Prompt 模板

Agent 填入 `{变量}`，其余文字不动，**不可删减**：

```
Vertical 9:16 video, single video generation with rhythmic beat-sync match-cuts between locations. No manual stitching.

Character identity: <<<ref>>> — [face描述], [build描述]. Same person throughout, but outfit changes per location.

[LOCATION 1 – 2s] Full scene change, new environment: {location_name}. Character wears {outfit}. {action}. Hold mode: {hold_mode}. At beat cut (white flash), {food_item} materializes into hand(s). Cut to next.

[LOCATION 2 – 2s] New environment: {location_name}. Same character identity. Character now wears {outfit}. {action}. Hold mode: {hold_mode}. Beat cut white flash — {food_item} materializes. Cut to next.

[LOCATION 3 – 2s] New environment: {location_name}. Same character identity. Character now wears {outfit}. {action}. Hold mode: {hold_mode}. Beat cut white flash — {food_item} materializes. Cut to next.

[LOCATION 4 – 2s] New environment: {location_name}. Same character identity. Character now wears {outfit}. {action}. Hold mode: {hold_mode}. Beat cut white flash — {food_item} materializes. Cut to next.

[LOCATION 5 – 2s] New environment: {location_name}. Same character identity. Character now wears {outfit}. {action}. Hold mode: {hold_mode}. Beat cut white flash — {food_item} materializes. Cut to end.

Style: Vertical 9:16, city natural light, vibrant saturation, rhythmic cuts. No real brand logos, no map UI, no store signage, no ratings. Character identity (face) consistent throughout. Hands natural, 5 fingers, no deformation. Food makes plausible contact with hand(s), not floating. Each location visually distinct — different environment, outfit, action, food.
```

### Step 4 — 单次视频生成

`generate_video(model, prompt, reference_image, aspect_ratio, duration)`

### Step 5 — QC

| Outcome | 条件 | 动作 |
|---------|------|------|
| PASS | identity一致、手自然、食物接触合理、地点可区分、节奏到位 | 交付 |
| REROLL | 脸漂移、手变形、食物浮空、地点太像 | Retry（下一模型） |
| BLOCKED | 超 budget（3 次全败）、identity 完全丢失、违禁内容 | 通知 human |

## 输出

- `location_food_popin.mp4`（9:16）
- `prompt_used.md`
- `qc_report.md`
