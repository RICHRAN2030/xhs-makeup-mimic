# 图片提示词模板 ｜ 3 张图同人物 2:3

> 本文档配合 `persona-anchor.md` 使用。先在 persona-anchor 建好「Persona Lock Card」，再用本文件的 3 张图模板填充。

## 一、3 张图的角色分工（**严格遵守**）

| 图 | 角色 | 占比 | 必备元素 |
|---|---|---|---|
| **图 1 主图 / 封面** | 钩流量 | 70-80% 画面 | 模特 45° 侧脸特写 + 完整妆面氛围 + 工作室柔光 |
| **图 2 细节 / 局部** | 种草 | 浅景深局部 | 眼妆 OR 唇妆 OR 卧蚕 OR 美瞳特写 |
| **图 3 对比 / 上身** | 验证 | 双格 / 全身 | 妆前妆后双格 OR 模特半身出片场景 |

## 二、图 1 主图提示词模板

```text
====== IMAGE 1 / Cover / 主图 ======
{
  Persona: <从 Lock Card 复制 15 项特征，浓缩为 1-2 句>,
  Pose: 45-degree side profile portrait, looking slightly off-camera, gentle relaxed expression,
  Makeup Focus: {主妆容元素 — 眼妆 / 唇 / 腮红 / 妆面整体},
  Makeup Details: {具体色彩 — 如 deep brown shadow with cool silver inner-corner highlight + milk tea lip + peachy pink blush},
  Lighting: soft key light from above + soft fill, studio softbox, no harsh shadows,
  Color Grading: {冷调 cool clean / 暖调 warm cozy / 通透 translucent},
  Background: light gray gradient OR off-white blurred studio backdrop,
  Composition: subject occupies 70-80% of frame, subtle negative space upper-right,
  Style: realistic editorial portrait, soft retouch, magazine cover quality, NOT overly smoothed,
  Texture: skin pores visible but soft, no plastic look,
  Sticker/Text Overlay: small white thin-stroke Chinese caption "都匀约妆" at bottom-right corner; small Emoji {🌸/🩵/💖/🎀/🐈/✨} sticker at top-right,
  Negative: no over-saturated colors, no harsh shadows, no plastic skin, no asymmetric eyes, no extra fingers,
}
--ar 2:3 --style raw --seed {SEED}
```

## 三、图 2 细节提示词模板

```text
====== IMAGE 2 / Detail / 细节 ======
{
  Persona Lock: SAME MODEL as Image 1, identical face structure, identical features. Use Image 1 as character reference.
  Crop: tight close-up on {eye area / lip area / cheek area},
  Focus Detail: {具体细节 — 如 winged eyeliner with cool silver inner-corner highlight + slightly upturned lash extensions / glossy milk-tea lip with subtle plumping highlight},
  Eye Contact: {gaze direction — looking up-right / looking down / closed eyes},
  Depth: shallow depth of field, surrounding face slightly out of focus,
  Lighting: same studio softbox as Image 1, slightly more directional to emphasize detail texture,
  Color Continuity: 与图 1 同色调,
  Composition: tightly framed, 90% on the focal detail,
  Negative: no different face structure, no different eye shape, no extra makeup elements not in Image 1,
}
--ar 2:3 --style raw --cref <IMAGE_1_URL> --cw 100 --seed {SEED}
```

## 四、图 3 对比 / 场景提示词模板

### 3A 妆前妆后对比（推荐主题 D 客户改造）

```text
====== IMAGE 3 / Before-After / 对比 ======
{
  Persona Lock: SAME MODEL as Image 1, identical face structure. Reference Image 1.
  Layout: split-frame composition, left half = pre-makeup, right half = post-makeup,
  Left (pre-makeup): natural bare face, neutral daylight, plain expression, slightly tired, identical face structure,
  Right (post-makeup): full makeup as shown in Image 1, confident expression, studio softbox lighting,
  Middle Divider: thin vertical white line,
  Text Overlay: large Emoji "换头‼️" centered at the bottom, white thin-stroke,
  Lighting Continuity: both sides match in white balance,
  Composition: each half is half-body shot,
}
--ar 2:3 --style raw --cref <IMAGE_1_URL> --cw 90 --seed {SEED}
```

### 3B 上身 / 场景出片（推荐主题 A 妆面 + B vlog）

```text
====== IMAGE 3 / Lifestyle / 上身 ======
{
  Persona Lock: SAME MODEL as Image 1.
  Shot Type: half-body or three-quarter body,
  Pose: standing or sitting casually in a {curated scene — café window seat / studio mirror / city street softly blurred},
  Outfit: {与图 1 服装色系相近，如同样白色高领 / 同样米色针织衫},
  Makeup: identical to Image 1 close-up,
  Background: contextual but blurred, light soft-focus bokeh,
  Lighting: natural soft daylight OR cinematic golden hour,
  Atmosphere: {风格氛围 — 原生通透感 / 樱花妹日杂 / 微醺野性},
  Negative: no different face, no different outfit color, no body proportion issues,
}
--ar 2:3 --style raw --cref <IMAGE_1_URL> --cw 80 --seed {SEED}
```

## 五、风格 → 视觉参数对照表

| 风格主线 | 色调 | 灯光 | 背景 | Emoji 装饰 |
|---|---|---|---|---|
| **韩系亚裔** | cool clean | studio softbox | gray gradient | 🩵 🐈 |
| **日杂 / 樱花妹** | warm translucent | soft daylight | off-white / wood grain bokeh | 🌸 🫧 |
| **美式甜心** | warm saturated | golden hour | dusty pink / cream | 🎀 💖 |
| **泰式千金** | warm cinematic | low contrast moody | dark teal / amber | 💐 🤎 |
| **clean 通透** | cool neutral | flat lighting | pure white | 🤍 🫧 |
| **厌世 / 演唱会烟熏** | desaturated cool | hard rim light | dark navy / black bokeh | 🔥 |

## 六、Negative Prompt 通用清单（防 AI 翻车）

每张图都建议加 negative prompt（部分工具如 Midjourney 用 `--no` 参数，部分工具如 SD 用独立 negative）：

```
NEGATIVE: plastic skin, over-smoothed, asymmetric eyes, extra fingers, deformed hands,
distorted face, mutated features, harsh shadows, blown highlights, watermark, signature,
text artifacts, ugly, blurry low-quality, anime cartoon look, doll-like, fake jewelry,
inconsistent makeup between images
```

## 七、输出 3 张图提示词的完整模板（**直接复制改填**）

```
====== PERSONA LOCK CARD ======
<引用 persona-anchor 锁卡，15 项>
seed: <8XXXX>
reference_strategy: Midjourney --cref --cw

====== IMAGE 1 / Cover ======
<填入图 1 模板>
--ar 2:3 --style raw --seed <SEED>

====== IMAGE 2 / Detail ======
<填入图 2 模板>
--ar 2:3 --style raw --cref <PLACEHOLDER_IMAGE_1_URL> --cw 100 --seed <SEED>

====== IMAGE 3 / Before-After or Lifestyle ======
<填入图 3 模板>
--ar 2:3 --style raw --cref <PLACEHOLDER_IMAGE_1_URL> --cw 80 --seed <SEED>

====== 使用说明 ======
1. 先生成 IMAGE 1，把它的输出 URL 复制
2. 把 IMAGE 2 / IMAGE 3 提示词里的 <PLACEHOLDER_IMAGE_1_URL> 替换为该 URL
3. 3 张图共用同一个 SEED，强化人物一致性
4. 若用即梦/可灵：把 IMAGE 1 上传为参考图，IMAGE 2/3 在工具里选"参考图模式"，强度 80-100
```

## 八、出图工具特别提示

### Midjourney
- 一致性最强组合：`--cref + --cw 100 + --seed`
- 启用 `--style raw` 减少 MJ 默认美化滤镜
- 若 cref 不稳，加 `--sref random` 锁定艺术风格

### 即梦（字节 Doubao）
- 在"图像生成"里点击「+参考图」上传图 1
- 参考强度建议 80-100（人物锁）
- 风格可选"日漫 / 写实 / 摄影"等

### 可灵
- "角色一致性"选项打勾
- 上传图 1 后在描述里强调"基于上图人物"

### Stable Diffusion (ComfyUI/A1111)
- 装 IP-Adapter + InstantID + FaceID 三件套
- 同 seed + 同 prompt 前 30% + IP-Adapter 权重 0.8-1.0

### Sora / DALL-E（GPT 内）
- 第一张生成后，第二张说"使用上面图片里那位模特，相同的脸"
- 详细描述 15 项特征
- 一致性效果中等，建议导入 MJ 再处理

## 九、为什么默认 2:3（小红书规范）

- 1:1 方图在小红书 feed 显示为方块，封面占比小
- 3:4 是手机竖屏标准，但小红书首页 feed 会上下裁切
- **2:3 / 3:4** 是小红书算法推荐的最佳封面比例（占据 feed 最大视觉空间，提升点击率约 15-25%）
- 视频笔记同理（9:16 竖屏，单帧 2:3 也可）
