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
视频模型单次生成，不逐帧拼接。Agent 读本 SKILL.md 即可执行。

## Core Concept

```
Location A: environment A + outfit A + action A → beat cut → food A in hold_mode A
Location B: environment B + outfit B + action B → beat cut → food B in hold_mode B
```

每 stop ~2s。3–5 地点 = 6–10s。节拍感 match-cut。

## Input — Per Location Schema

```json
{ "location_name": "...", "food_item": "...", "outfit": "...", "action": "...", "hold_mode": "..." }
```

`hold_mode`: `palm` | `two_hands_bowl` | `plate` | `cup` | `wrap`

## Safety

### 食物白名单
| 类别 | 示例 |
|------|------|
| 热食 | 拉面/乌冬/米饭/饺子/寿司/咖喱/汉堡/披萨/烤肉 |
| 小食 | 鲷鱼烧/可丽饼/章鱼烧/薯条/炸鸡/甜甜圈/铜锣烧 |
| 甜点 | 冰淇淋/蛋糕/布丁/马卡龙/棉花糖/刨冰 |
| 水果 | 西瓜/草莓/橘子/苹果/芒果/葡萄/菠萝 |
| 饮品 | 奶茶/果汁/咖啡/汽水/奶昔/冰沙 |

### 拒绝
❌ 武器/危险品/人体部位/性暗示手势
❌ 真实品牌logo（KFC/McDonald's/Starbucks）/ 地图UI / 评分 / 店招牌
❌ 未成年人 + 暗示性手势 → 直接 BLOCKED

## Budget

1. seedance / seedance-fast（主生成）
2. kling（reroll 1）
3. grok（reroll 2）

主生成 1 + reroll 2 = 最多 3 次。三轮全败 → BLOCKED。

## Prompt 模板

（Agent 填入 `{变量}`，其余文字不可删减）

```
Vertical 9:16 video, single video generation with rhythmic beat-sync match-cuts between locations. No manual stitching.

Character identity: <<<ref>>> — [face描述], [build描述]. Same person throughout, but outfit changes per location.

[LOCATION 1 – 2s] Full scene change, new environment: {location_name}. Character wears {outfit}. {action}. Hold mode: {hold_mode}. At beat cut (white flash), {food_item} materializes into hand(s). Cut to next.

[LOCATION 2 – 2s] New environment: {location_name}. Same character identity. Character now wears {outfit}. {action}. Hold mode: {hold_mode}. Beat cut white flash — {food_item} materializes. Cut to next.

…（重复 N 个 location，上限 5）…

Style: Vertical 9:16, city natural light, vibrant saturation, rhythmic cuts. No real brand logos, no map UI, no store signage, no ratings. Character identity (face) consistent. Hands natural, 5 fingers. Food makes plausible contact with hand(s). Each location visually distinct — different environment, outfit, action, food.
```

## QC

| Outcome | 条件 | 动作 |
|---------|------|------|
| PASS | identity一致 / 手自然 / 食物接触合理 / 地点可区分 | 交付 |
| REROLL | 脸漂移 / 手变形 / 食物浮空 | 下一模型 retry |
| BLOCKED | 3次全败 / identity丢失 / 违禁 | 通知 human |

## 输出

- `location_food_popin.mp4`（视频，9:16）
- `prompt_used.md`（实际使用的 prompt 全文）
- `qc_report.md`（QC 结果）
