# 示例 2 ｜ 输入"单眼皮韩系小猫妆 + 参考图"

> 输入：明确风格 + 提供参考图。Skill 用参考图作人物锚（模式 1）。

## 用户输入
```
想法：想发一个单眼皮韩系小猫妆
参考图：H:\客户照片\阿茶_约妆后.jpg（25 岁单眼皮女生，长发刘海，左颊有小痣）
```

## Skill 输出

# 都匀桃九九 ｜ 单眼皮韩系小猫妆笔记 · 2026-05-13

## 📋 元信息
- 主题分类：A 妆面展示
- 风格主线：韩系亚裔 + 小猫感
- 受众细分：单眼皮 / 淡颜
- 钱钩子：无
- 节日 / 季节钩子：无（常规客返笔记）

## 👤 Persona Lock Card

```yaml
persona_id: P-001 (阿茶 ｜ 单眼皮淡颜韩系款)  # 基于用户参考图识别
age: 25
gender: female
ethnicity_visual: East Asian
face_shape: oval
face_length: medium
eye_shape: mono-lid                           # ← 从参考图确认
eye_distance: average
nose: straight, medium bridge
lip: thin, defined cupid-bow
chin: rounded
skin_tone: cool fair
skin_texture: smooth
hair_color: dark brown
hair_style: straight long with curtain bangs   # ← 从参考图确认
distinctive: 左颊小痣，笑起来眼睛弯弯           # ← 从参考图确认
reference_image: H:\客户照片\阿茶_约妆后.jpg
reference_strategy: Midjourney --cref <upload_url> --cw 100
seed: 49102
```

> 用户参考图作 cref 主锚。需先把本地参考图上传到图床获取 URL（如 imgbb/PicGo/腾讯云 COS）。

## 🖼️ 3 张图提示词

### 图 1 ｜ 主图 / 封面（45° 侧脸）

```
25-year-old East Asian female, oval face, medium length, mono-lid eyes, straight 
medium-bridge nose, thin defined cupid-bow lips, rounded chin, cool fair skin, 
dark brown straight long hair with curtain bangs, distinctive small mole on left 
cheek, gentle smile with eyes slightly crinkled.
45-degree side profile portrait.
Makeup focus: Korean "small cat" makeup — winged eyeliner slightly upturned, 
cool silver inner-corner shimmer, dark brown gradient shadow, milk-tea glossy 
lip, peachy side-cheek blush.
Lighting: studio softbox key light from above + soft fill, cool clean color grading.
Background: light gray gradient, blurred.
Composition: subject 80% of frame.
Style: editorial Korean magazine portrait, slight retouch, skin pores visible, 
NOT plastic.
Sticker: small Emoji 🐈 at top-right; tiny white Chinese caption "都匀约妆" at 
bottom-right corner.
Negative: no different face, no over-smoothed skin, no anime cartoon look.
--ar 2:3 --style raw --cref <USER_REF_IMAGE_URL> --cw 100 --seed 49102
```

### 图 2 ｜ 细节（眼妆 + 卧蚕银光）

```
SAME MODEL as Image 1, identical face structure, identical mono-lid eyes, 
identical 25-year-old features, same dark brown hair with curtain bangs.
Tight close-up on right eye area, mono-lid clearly visible.
Detail: winged eyeliner upturned at outer corner, cool silver inner-corner 
highlight (banana shape), dark brown gradient eyeshadow, mascara curl on 
upper lashes only.
Eyebrow: natural arch, slightly straight.
Gaze: looking up-right with slight smile.
Depth: shallow, surrounding face soft.
Lighting: same studio softbox.
Negative: no double-eyelid, no different eye shape, no extra makeup.
--ar 2:3 --style raw --cref <USER_REF_IMAGE_URL> --cw 100 --seed 49102
```

### 图 3 ｜ 妆前妆后对比

```
SAME MODEL as Image 1.
Split-frame layout, left = pre-makeup, right = post-makeup.
Left (pre-makeup): bare-face mono-lid, neutral daylight, plain expression, no 
makeup, slightly tired, identical 25-year-old face structure.
Right (post-makeup): full Korean small-cat makeup as in Image 1, confident 
smile with eyes slightly crinkled.
Middle: thin vertical white divider line.
Text overlay: large Emoji "换头‼️🐈" centered bottom, white thin-stroke.
Lighting: cool clean, balanced both sides.
Each half: half-body framing.
Negative: no different face structure on either side.
--ar 2:3 --style raw --cref <USER_REF_IMAGE_URL> --cw 90 --seed 49102
```

## 🏷️ 3 版标题

| 版本 | 公式 | 字数 | 标题 |
|---|---|---|---|
| **A 服务卡式** | A | 19 | 都匀约妆｜单眼皮神妆🐈韩系亚裔小猫感拉满‼️ |
| **C 反问型** | C | 14 | 这样化的单眼皮🩵真的不是韩国 vlogger 吗 |
| **E 体感动词** | E | 16 | 都匀约妆｜单眼皮化成这样真的换头‼️🐈 |

> 推荐：A 作主标题，E 备选（更口语化）。

## 📝 3 版正文

### 精简版 ｜ 95 字

```
客妹自己单眼皮 + 淡颜，化妆店从来不化她——这次用『冷调银光卧蚕 + 奶茶唇』反向救她。出门同事第一句"你是不是去韩国了"她当场笑哭。

都匀桃九九化妆室 ｜ 约妆 / 招学员私我宝～
#都匀化妆师 #都匀约妆 #单眼皮化妆 #韩系亚裔妆 #小猫妆教程
```

### 标准版 ｜ 124 字 ★ 推荐

```
客妹自己单眼皮 + 淡颜，化妆店从来不化她，第一次约我时一脸不抱期待。

我反过来跟她说：单眼皮才是韩系小猫感的天选——眼线尾上扬 + 卧蚕银光，整张脸瞬间野生中性。底妆 NARS 裸光叠 Visee 高光，眼影锁定米色 + 深棕过渡，腮红下手要轻打侧颊不打苹果肌。她出门同事第一句"你是不是去韩国了"。

都匀桃九九化妆室｜约妆 / 招学员私我宝～（黔南州内同城可上门）
#都匀化妆师 #都匀约妆 #单眼皮化妆 #韩系亚裔妆 #小猫妆教程
```

### 深度版 ｜ 152 字

```
客妹阿茶自己单眼皮 + 淡颜，化妆店从来不化她，第一次约我时一脸不抱期待。

单眼皮的韩系小猫公式我拆给她（也给所有同款姐妹）：

- 卧蚕银光：冷调银色香蕉型扫在眼下 0.5cm
- 眼线尾上扬 15°：不要全描，只描眼尾 1/3
- 眼影双色封顶：米色铺 + 深棕勾尾，不晕大面积
- 唇用奶茶豆沙 + 中央叠高光显嘟嘟
- 腮红打侧颊不打苹果肌

她出门同事第一句"你是不是去韩国了"——这就是单眼皮的福报。

都匀桃九九化妆室 ｜ 约妆 / 招学员私我宝～
#都匀化妆师 #都匀约妆 #单眼皮化妆 #韩系亚裔妆 #小猫妆教程
```

## ✅ 自检
- [x] 3 张图 2:3 + 用户参考图作 cref
- [x] 人物锁卡基于用户图识别填写
- [x] 标题 14-19 字含 🐈 / 🩵 Emoji
- [x] 正文均含具体产品（NARS / Visee）+ 客户故事 + 价格信号
- [x] 末尾跨州转化路径

## 工具适配
- **Midjourney**：把 `<USER_REF_IMAGE_URL>` 替换为参考图实际 URL（可先上传到 imgbb.com 获取）
- **即梦/可灵**：在工具里直接上传参考图，参考强度 90-100，3 张图都用同一参考图
- **本地参考图上传**：推荐 imgbb.com（免登录）或 GitHub Gist 存图
