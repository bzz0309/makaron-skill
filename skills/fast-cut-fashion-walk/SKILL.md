---
name: one-take-fashion-walk
description: >
  穿搭快切走秀：上传一张人物照片，生成15秒快节奏穿搭视频。
  6套韩系look × 6个城市场景，手遮镜头卡点切换+结尾快速闪回。
  Fast-cut fashion walk: upload a photo, get a 15s high-energy fashion video
  with 6 Korean streetwear looks, hand-swipe transitions, and rapid flash ending.
allowed-tools: analyze_image Bash mcp__makaron__makaron_edit_image mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status
metadata:
  makaron:
    icon: "🚶"
    color: "#1A1A2E"
    tags: [fashion, streetwear, kpop, outfit, seoul, match-cut, fast-cut, transition]
    defaultAspectRatio: "9:16"
    videoModel: seedance
---

# 穿搭快切走秀 — Fast-Cut Fashion Walk

**⚠️ 重要：用户在对话中附带的图片就是面孔/角色参考，直接使用。不要要求用户重新上传。**

生成一段**15秒快节奏穿搭走秀视频**：6套差异化韩系look × 6个不同城市场景，通过主角的手从下往上快速划过镜头实现卡点切换，结尾3秒快速闪回所有look。全程快节奏，无慢动作。

## 输入类型

- **图片**：人物面孔/角色参考图（用于锁定外貌）
- **文字描述**（可选）：风格偏好、季节、特定穿搭要求

## 输出

- 15秒 9:16 竖屏视频
- 6套look快切，手遮镜头转场
- 结尾快速闪回所有穿搭
- 全程快节奏，高能量

## 四步工作流

### Step 1: 生成角色身份板

基于用户上传的面孔参考，生成一张干净背景的正面肖像角色板（用于Seedance面孔锁定）。

调用 `mcp__makaron__makaron_edit_image`：
- image: 用户上传的图片
- editPrompt: "Same person, clean white background, headshot portrait, looking at camera, soft natural smile, high quality"
- aspectRatio: "1:1"

将生成的角色板上传获取公共URL：
```bash
makaron admin upload <local_file> "refs/onetake-<timestamp>.jpg"
```

### Step 2: 构建视频脚本

设计6套差异化look × 6个场景：

**默认配置：**
| # | 风格 | 穿搭 | 场景 |
|---|------|------|------|
| 1 | 学院绅士 | 格纹oversized西装+阔腿西裤+乐福鞋+眼镜 | 机场长廊 |
| 2 | 工装牛仔 | 做旧牛仔夹克套装+马丁靴+银链 | 红砖巷 |
| 3 | 运动复古 | 天蓝拼色运动夹克+深灰阔腿裤+厚底鞋 | 地铁站 |
| 4 | 慵懒文艺 | 大地色风衣+黑色高领+阔腿裤+围巾 | 梧桐树街 |
| 5 | 暗黑机车 | 黑色皮夹克+窄腿裤+尖头靴+墨镜 | 地下停车场 |
| 6 | 甜酷混搭 | 藏蓝针织+白衬衫叠穿+水洗牛仔+帆布包 | 咖啡街黄昏 |

**转场方式：**
- 主角的手从画面下方快速往上划过镜头（自然手势，不抓取任何物品）
- 手经过后场景和穿搭瞬间切换
- 不要做扯帽子/摘眼镜等容易出错的动作

**时间分配：**
- 0-12s：6套look，每套2秒
- 12-15s：快速闪回，0.5秒一个look循环加速

**脚本模板：**
```
<<<media_1>>> Fast-paced fashion video with 6 outfit changes, 9:16 vertical. Same young man with [发型描述]. ALL fast tempo, NO slow motion. Transitions: his own hand quickly swipes up past the camera from below (natural gesture, no grabbing anything). 6 looks in 12 seconds then 3 seconds of rapid flash cuts. High energy editorial fashion film.

0-2s: [场景1 + Look 1穿搭细节]. Fast stride. His hand swipes up past camera —

2-4s: [场景2 + Look 2穿搭细节]. Walking fast. His hand swipes up past camera —

4-6s: [场景3 + Look 3穿搭细节]. Quick walk. His hand swipes up past camera —

6-8s: [场景4 + Look 4穿搭细节]. Elegant stride. His hand swipes up past camera —

8-10s: [场景5 + Look 5穿搭细节]. Edgy cool walk. His hand swipes up past camera —

10-12s: [场景6 + Look 6穿搭细节]. Relaxed but quick walk toward camera.

12-15s: RAPID FLASH CUTS — all 6 looks cycling in 0.5-second bursts getting faster: [look1], [look2], [look3], [look4], [look5], [look6] — faster faster. Final frame: faces camera, quick confident smile. Freeze.
```

展示脚本给用户确认。

### Step 3: 生成视频

用户确认后，调用 `mcp__makaron__makaron_create_video`：
- script: 确认的脚本
- images: [角色板URL]
- duration: 15
- aspectRatio: "9:16"
- videoModel: "seedance"

轮询 `mcp__makaron__makaron_get_video_status` 直到完成（约5-8分钟）。

### Step 4: 交付

展示视频结果，提供调整选项：
- 重新生成（换穿搭/换场景/换转场节奏）
- 增减look数量
- 换季节/风格方向

## Prompt 工程知识库

### 穿搭描述要点

- 必须有**具体服装单品名称**（不说"穿着时尚的衣服"）
- 必须有**材质/颜色/版型**（oversized、wide-leg、distressed wash）
- 必须有**配饰细节**（链条包、银链项链、圆框眼镜、围巾）
- 必须有**鞋子**（chunky boots、loafers、pointed boots）
- 6套look之间**差异最大化**（颜色/廓形/风格/配饰全部不同）

### 转场关键规则

| 规则 | 说明 |
|------|------|
| 手从下往上划 | 自然手势，不从画面外伸入 |
| 不抓取物品 | 不做摘帽/摘眼镜/拿东西等动作（容易出错） |
| 不出现多余的手 | 必须是主角自己的手 |
| 快速通过 | 手划过镜头的时间要短（<0.5秒） |

### 场景差异化

6个场景应在以下维度拉开差异：
- **光线色温**：冷白/暖黄/荧光/金色/暗光/霓虹
- **空间类型**：室内/室外/地下/街道/建筑
- **材质背景**：玻璃/红砖/水泥/绿植/金属/霓虹

### 韩系Streetwear风格词库

| 风格方向 | 关键单品 | 配色 |
|----------|----------|------|
| 学院绅士 | 格纹西装+阔腿西裤+乐福鞋+眼镜 | 米棕+灰 |
| 工装牛仔 | 做旧牛仔夹克+阔腿牛仔+马丁靴 | 卡其+黑 |
| 运动复古 | 拼色运动夹克+阔腿裤+厚底鞋 | 天蓝+奶白 |
| 慵懒文艺 | 风衣/大衣+高领+阔腿裤+围巾 | 驼色+黑 |
| 暗黑机车 | 皮夹克+窄腿裤+尖头靴+墨镜 | 全黑+银 |
| 甜酷混搭 | 针织+衬衫叠穿+水洗牛仔+帆布包 | 藏蓝+白 |
| 机能户外 | 冲锋衣+束脚裤+厚底靴+胸包 | 黑+荧光点缀 |
| 复古preppy | 毛衣背心+衬衫+百褶裤+乐福鞋 | 酒红+奶白 |

## Rules

1. **季节统一** — 6套look必须是同一季节（全长袖或全短袖），不能混搭
2. **全程快节奏** — 不用慢动作，保持高能量
3. **手遮镜头切** — 转场统一用手从下往上划过，不要其他花哨动作
4. **差异最大化** — 6套look的颜色/廓形/风格/配饰必须全部不同
5. **结尾快速闪回** — 最后3秒做所有look的快速循环，越来越快，定格微笑
6. **英文脚本** — 提交给Seedance的脚本用英文，效果更好
7. **角色板必须AI生成** — 不直接用用户原图提交视频（避免版权检测），先通过edit_image生成角色板
8. **不做危险动作** — 不写摘帽/摘眼镜/抓物品等容易渲染出错的动作
