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

同一个角色在 exactly 3 个城市打卡，每地点换装+不同食物+不同动作，节拍切换。
视频模型单次生成。Agent 不得改写 prompt 模板。

## Core Concept

3 城街头打卡。环境切换→角色摆 pose→食物弹出→表情反应。节拍 match-cut。每处 3s，共 9s。

## Input Schema（Agent 严格按此读取）

### 用户必传

| 输入 | 说明 |
|------|------|
| 人物图 | 1 张 reference image |
| locations | exactly 3 个地点，JSON 数组；用户给 4–5 个时先让用户选 3 个再继续 |

### 每 location 字段（全部必填）

```json
{
  "location_name": "Shinjuku ramen alley at night, red lanterns, steam",
  "food_item": "steaming tonkotsu ramen in a black bowl, chopsticks",
  "outfit": "black zip-up jacket, black tee, AirPods",
  "action": "holds the ramen bowl with both hands, lifts it toward camera, grins",
  "hold_mode": "with both hands holding a steaming bowl"
}
```

| 字段 | 必填 | 说明 |
|------|:--:|------|
| `location_name` | ✅ | 城市+地点+氛围描述 |
| `food_item` | ✅ | 食物外观描述（需通过安全白名单） |
| `outfit` | ✅ | 本地点穿着，每地点独立 |
| `action` | ✅ | 拿取/接住/捧起/咬食物的具体动作描述 |
| `hold_mode` | ✅ | 全自然语言，如：with one open hand / with both hands holding a steaming bowl / holding a plate in one hand / holding a cup with fingers wrapped / cradling wrapped food in both hands |

### 完整 JSON 示例（Agent 可直接参考）

```json
{
  "locations": [
    {
      "location_name": "Shinjuku ramen alley at night, red lanterns, steam",
      "food_item": "steaming tonkotsu ramen in a black bowl, chopsticks",
      "outfit": "black bomber jacket over white tee, AirPods",
      "action": "presents the bowl to camera with both hands, grins, then takes a small bite",
      "hold_mode": "with both hands holding a steaming bowl"
    },
    {
      "location_name": "Myeongdong street, Seoul, neon signs, busy crowd",
      "food_item": "golden hotteok sweet pancake, steam rising",
      "outfit": "cream knit cardigan over a striped tee",
      "action": "catches the hotteok in one open hand, takes a bite, grins with surprise",
      "hold_mode": "with one open hand"
    },
    {
      "location_name": "Khao San Road night market, Bangkok, string lights, food stalls",
      "food_item": "fresh mango sticky rice on a banana leaf plate",
      "outfit": "relaxed linen camp shirt with floral print",
      "action": "scoops a bite with a spoon, grins wide at camera, peace sign",
      "hold_mode": "holding a plate in one hand"
    }
  ]
}
```

## Safety（Agent 强制执行）

食物白名单（仅以下类别可通过）：
- 热食：拉面/乌冬/炒面/米饭/饺子/寿司/咖喱/汉堡/披萨/烤肉/火锅
- 小食：鲷鱼烧/可丽饼/章鱼烧/薯条/炸鸡/甜甜圈/铜锣烧/煎饼/热狗
- 甜点：冰淇淋/蛋糕/布丁/马卡龙/棉花糖/刨冰/巧克力
- 水果：西瓜/草莓/橘子/苹果/芒果/葡萄/菠萝
- 饮品：奶茶/果汁/咖啡/汽水/奶昔/冰沙

禁止（自动 BLOCKED）：
- ❌ 武器/危险品/易燃物
- ❌ 人体部位/血液/器官
- ❌ 性暗示手势或姿势
- ❌ 真实品牌 logo（KFC/McDonald's/Starbucks 等）
- ❌ 真实店招牌/地图 UI/Google/Apple Maps/评分星星/推荐文案
- ❌ 未成年人 + 暗示性手势 → 直接 BLOCKED

Identity 规则：脸部一致（同一个人），每地点 outfit 独立可变。

## Budget

| 轮次 | 模型 | 说明 |
|:--:|------|------|
| 1 | seedance / seedance-fast | 主生成 |
| 2 | kling | reroll 1 |
| 3 | grok | reroll 2 |

三轮全败 → BLOCKED。通知 human。总次数 ≤ 3。

## Workflow

### Step 1 — 验证输入

- 人物图 ≥ 1 张
- locations exactly 3 个
- 每个 location 五字段完整（location_name / food_item / outfit / action / hold_mode）
- 所有 food_item 在安全白名单 → 否则拒绝并提示缺什么

### Step 2 — 分析人物

`analyze_image` → face + build 描述。仅提取外貌特征（发型/肤色/五官），不提取品牌标签。
将结果写入 `location_plan.json` 的 `character` 字段。

### Step 3 — 组装 prompt（❌ 禁止修改模板）

Agent 填入 `{变量}`，其余文字不动。**不得翻译、改写、增删。** 将组装结果写入 `prompt_used.md`。

```
Vertical 9:16 video, single video-model generation (prefer SeeDance when available), no manual stitching. 9 seconds total, 3 scenes × 3 seconds. Vibrant colors, city natural light, rhythmic beat-sync match-cuts between locations.

Character: same person throughout — [FACE], [BUILD]. Outfit changes per location.

[SCENE 1 — 3s] Mid-shot, push-in. Environment: {location_name}. Character wears {outfit}. At the beat, {food_item} visibly appears {hold_mode}; {action}. Beat cut white flash. Transition to next.

[SCENE 2 — 3s] Mid-shot, slow push-in. New environment: {location_name}. Same character identity. Character now wears {outfit}. At the beat, {food_item} visibly appears {hold_mode}; {action}. Beat cut white flash. Transition to next.

[SCENE 3 — 3s] Mid-shot, gentle dolly forward. New environment: {location_name}. Same character identity. Character now wears {outfit}. At the beat, {food_item} visibly appears {hold_mode}; {action}. Beat cut white flash. End.

Style rules: 9:16 vertical. Natural hands with 5 fingers, no deformation. Face identity consistent across all locations — same person. Food makes realistic contact with hands — gripping, holding, lifting, not floating. Each location visually distinct: different city, different outfit, different food, different action. No brand logos, no map UI, no store signage, no ratings, no text overlay.
```

**赋值规则**：
- [FACE] / [BUILD]: from analyze_image output, concise keywords
- {hold_mode}: 使用 location 中 hold_mode 的完整自然语言值
- 其余 {变量}: 从 locations JSON 逐字段填入
- **不得修改模板的任何固定文字，不得翻译成其他语言，不得添加 Sound/音乐描述**
- **必须保留 3s 硬编码（3 scenes × 3s = 9s），不要改成动态 dur**

### Step 4 — 单次视频生成

`generate_video(model, prompt, reference_image, 9:16, 9)`

### Step 5 — QC

QC 时检查 **prompt_used.md 是否严格按模板填空**（逐行比对模板，不能自由发挥）。

| Outcome | 条件 | 动作 |
|---------|------|------|
| PASS | identity 一致、手自然/5手指不变形、食物真实接触手部、地点可区分、prompt_used 严格匹配模板 | 交付 |
| REROLL | 脸漂移、手变形、食物浮空、地点太像（max 2 次，按 budget 表换模型） | Retry |
| BLOCKED | 3 轮全败、identity 丢失、违禁内容、prompt_used 明显偏离模板 | 通知 human |

## 交付物（全部必输出）

- `location_food_popin.mp4`（9:16，9s）
- `location_plan.json`（character 描述 + 3 个 location 完整数据）
- `prompt_used.md`（Step 3 组装后的完整 prompt，QC 逐行比对模板）
- `qc_report.md`（逐项 PASS/REROLL/BLOCKED 结论 + prompt_used 模板匹配检查）
