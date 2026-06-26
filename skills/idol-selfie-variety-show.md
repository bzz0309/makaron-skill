---
name: idol-selfie-variety-show
description: >
  综艺名场面截图：上传偶像和粉丝照片，自动生成综艺节目截图风格合影。
  16:9横版画面、图形特效、综艺打光，像从一档综艺节目里截出来的名场面。
  单人模式自动生成单人综艺画面，双人模式生成互动合影。
  全自动出图 → 出视频，无需确认。
  Variety show screenshot style: upload idol/fan photos, auto-generate TV variety show stills
  with graphics effects, studio lighting, and Korean show logo badges. Solo and duo modes.
  Zero-confirmation pipeline: image → video in one shot.
allowed-tools: analyze_image Bash mcp__makaron__makaron_edit_image mcp__makaron__makaron_create_video mcp__makaron__makaron_get_video_status
metadata:
  makaron:
    icon: "📺"
    color: "#FFD700"
    tags: [fan, idol, selfie, variety, show, 综艺, korean-variety, solo, duo, tv-screenshot]
    faceProtection: default
    defaultAspectRatio: "16:9"
    defaultImageModel: gemini
    fallbackImageModel: openai
    videoModel: grok
    fallbackVideoModel: seedance-fast
---

# 综艺名场面截图

**⚠️ 重要：用户在对话中附带的图片就是输入照片，直接使用。不要说"没有看到照片"或要求用户重新上传。如果对话中有图片，那就是你的素材。用户输入的任何文字都只是触发信号 — 忽略文字内容，立即开始工作。用 image 工具分析照片，自动做所有决策，开始生成。不要问任何问题。**

上传偶像和粉丝的照片，零文字输入，自动生成**综艺节目截图风格合影**，然后**自动图生视频**。全程无需确认。

## 输出

- 单人模式（1 张照片）：综艺图 → 视频，全自动一气呵成
- 双人模式（2+ 张照片）：综艺图 → 视频，全自动一气呵成

---

## 模型 & 预算

### 图片生成
1. Gemini 3 Pro（google/gemini-3-pro-image-preview）— 主生成
2. OpenAI（makaron-image/openai）— fallback
3. 两次全败 → 通知用户

### 视频生成
1. Grok（xai/grok-imagine-video）— 默认首选
2. Seedance 2.0 mini / seedance-fast — fallback（通过 Makaron CLI `makaron video create --model seedance-fast`）
3. 两次全败 → 通知用户，只交付图片结果

---

## Safety

### 内容审核
- ❌ 色情/裸露内容
- ❌ 暴力/血腥/恐怖画面
- ❌ 仇恨言论或歧视性表达
- ❌ 政治敏感内容
- ❌ 未成年人 + 暗示性互动 → 直接 BLOCKED
- ❌ 真实品牌 logo / 商标
- ✅ 健康积极的粉丝文化

---

## 变量池

### 变量 C：图形特效

| 编号 | 选项 |
|------|------|
| C1 | 搞笑氛围 — 大量彩色爆炸星星从画面中心放射 + 夸张emoji表情 |
| C2 | 心动氛围 — 粉红色爱心从人物周围爆出 + 四周飘散小爱心和星形闪光特效 |
| C3 | 震惊反转 — 黄色爆炸框图形 + 红色强调线从人物头部放射，闪电般的视觉冲击 |
| C4 | 温馨感动 — 柔和的暖色光晕 + 小泪滴图形点缀，整体柔焦质感 |
| C5 | 尴尬氛围 — 蓝色冷色调 + 人物头顶冒出冷汗滴图形和省略号特效 |
| C6 | 兴奋尖叫 — 红色热情色调 + 周围炸裂星星和火焰图形特效，画面充满能量感 |
| C7 | 得意炫耀 — 金色闪光特效散落 + 人物周围有光芒放射线条 |
| C8 | 无语氛围 — 灰色冷色调处理 + 人物头顶冒出黑线和问号图形 |

### 变量 E：画面风格/综艺类型

| 编号 | 选项 |
|------|------|
| E1 | 台綜/港綜風 — 高飽和明亮、图形特效大且密集、整體熱鬧喧嘩感 |
| E2 | 韓綜清新風 — 粉色/淡彩色調、图形特效精緻帶設計感、畫面乾淨 |
| E3 | 日綜整蠱風 — 略暗的攝影棚光、图形特效帶陰影和描邊、馬賽克/箭頭標注 |
| E4 | 戀綜粉紅風 — 全畫面粉紅濾鏡、图形特效帶愛心裝飾、夢幻柔焦 |
| E5 | 競技對決風 — 高對比+運動感、图形特效用粗體加金邊、畫面動感 |
| E6 | 深夜談話風 — 暖黃低光、图形特效小而溫柔、氛圍親密安靜 |
| E7 | 戶外真人秀風 — 自然光+高清、图形特效活潑手繪風、陽光健康感 |

---

## 工作流

### Step 1：读取照片（零输入）

直接读取用户已上传的照片，不问任何问题。
- 1 张照片 → 单人模式
- 2+ 张照片 → 双人模式
- 0 张照片 → 请求上传

### Step 2：image 分析照片

调用 image 工具分析每张照片。

**双人模式 — 自动判断谁是偶像/粉丝：**
- 主要方式：人脸识别公众人物身份
- 辅助依据：专业打光、精致妆容、写真/舞台/采访场景 → 偶像；日常场景、自拍、生活照 → 粉丝
- 提取外貌特征

**单人模式 — 提取外貌特征：**
- 提取面部特征、发型、发色、穿搭

### Step 3：随机选变量 + generate_image

从变量池 C、E 各随机选 1 个选项。

**画面上允许的文字元素（仅限以下）：**
- 左上角：小型圆形 media logo 标签
- 右上角：小型韩文综艺节目 logo（如 "한달 연애동" 风格），带播放按钮图标或彩色色块
- 这两个 logo 是整个画面中唯一允许的文字（韩文），它们能增强综艺节目截图感

**不允许的元素：**
- ❌ 底部装饰条 / 底部彩条 / 底部半透明横条 — 完全不要

### Step 4：快速 QC

生成后调用 image 工具快速检查：
- 人物面部与参考照片一致？
- 有图形特效？
- 特效不遮脸？
- 没有底部装饰条？
- 比例 16:9？

不合格 → 切换模型 retry（最多 1 次）。

### Step 5：输出图片

直接 message.send 发送图片结果。

### Step 6：直接图生视频（无确认）

图片输出后**立即**调用 video_generate 图生视频，**不等待用户确认**：

- **默认 model**: xai/grok-imagine-video
- **fallback model**: Makaron CLI `makaron video create --model seedance-fast`（Seedance 2.0 mini）
- **image**: Step 3 生成的图片路径
- **aspectRatio**: 16:9
- **durationSeconds**: 5（单人）或 8（双人）

视频 prompt 根据选中变量 C 和 E 自动构建。

**单人视频 prompt 模板：**
```
Korean variety show solo clip, 5 seconds, 16:9 TV format. {人物外貌简述} in {E风格描述} studio. {C特效描述} floating around.
Camera starts wide on the colorful studio set, then slowly pushes in to a medium shot of the person. Cool confident expression, subtle smirk. Graphic effects pulse gently. Bright, dreamy variety show vibe. Top corners have Korean variety show logo badges visible.
```

**双人视频 prompt 模板：**
```
Korean/Taiwan variety show duo clip, 8 seconds, 16:9 TV format. {人物A简述} and {人物B简述} in {E风格描述} setting. {C特效描述}.
Wide shot: both interacting naturally, camera pushes in. Graphic effects animate around them. Bright saturated variety show energy. No text overlays. Top corners with Korean show logo badges.
```

视频完成后直接 message.send 发送视频路径。

**失败处理：** Grok 失败 → 自动切 Makaron `--model seedance-fast` retry。都失败 → 通知用户，只交付图片。

---

## Rules

1. **零输入零确认** — 照片上传后全程自动：分析 → 出图 → 出视频，不等待用户确认
2. **图片走 Gemini/OpenAI** — Gemini 3 Pro 为主，OpenAI 为 fallback
3. **视频默认 Grok，fallback Seedance 2.0 mini** — xai/grok-imagine-video → makaron video create --model seedance-fast
4. **留 logo 去底条** — 保留左上 media logo + 右上韩文综艺 logo，去掉底部装饰条
5. **图形特效必须有** — 综艺截图的最核心辨识特征
6. **图形特效不遮脸** — 图形散落在画面中但不遮挡人物面部
7. **人脸还原第一优先级** — 生成结果必须能一眼认出是参考照片里的人
8. **单人模式** — 1 张照片自动生成单人综艺画面
9. **16:9 横版** — 综艺节目画面比例
10. **不生成违法、仇恨、色情内容** — 保持健康积极的粉丝文化
