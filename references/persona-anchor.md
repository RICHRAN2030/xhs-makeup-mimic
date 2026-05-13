# 人物一致性锚定 ｜ Persona Anchor

> **这是整个 skill 最重要的文件**。用户最在意的一件事就是"3 张图必须是同一个人物"——这文件解决这个问题。

## 一、为什么需要"人物锁卡"

AI 出图工具默认每次出图都是新人物。即使提示词写"25 岁单眼皮女生"，第一张可能是高鼻梁，第二张可能是低鼻梁，第三张眼距又变了——这对小红书化妆师笔记是致命的，因为读者一眼能看出"这不是同一个客户"，立刻失去信任感。

解决方法是建立一张「**Persona Lock Card 人物锁卡**」，把模特的 15 个特征用结构化语言固定下来，3 张图共享这同一张卡。

## 二、Persona Lock Card 的 15 项标准字段

```yaml
persona_id: <唯一编号或名字>      # 如 P-001 / 阿茶
age: <数字>                       # 22 / 25 / 28
gender: female | male             # 几乎都是 female
ethnicity_visual: <视觉族裔>      # East Asian / Northeast Asian
face_shape: <脸型>               # oval / round / square / oblong / heart / pear
face_length: short | medium | long
eye_shape: <眼型>                # mono-lid 单 / inner-double 内双 / outer-double 外双 / hooded 窄双
eye_distance: close | average | wide
nose: <鼻型>                     # straight, low bridge / high bridge / button / curved
lip: <唇型>                      # full / thin / cupid-bow / wide / heart
chin: <下巴>                     # rounded / pointed / squared / receded
skin_tone: <肤色>                # cool fair / warm fair / cool medium / warm medium / olive
skin_texture: smooth | freckled | slightly pored
hair_color: <发色>               # black / dark brown / chocolate / chestnut
hair_style: <发型>               # straight long / wavy long / shoulder bob / wolf cut / low ponytail
distinctive: <辨识度特征>        # 颊上小痣 / 微微婴儿肥 / 笑起来有酒窝
```

## 三、3 种使用模式

### 模式 1 ｜ 用户传了参考图（最优）

步骤：
1. 用 Read 工具读图
2. 按 15 项清单逐一识别填写
3. 输出锁卡
4. 锁卡末尾自动追加：`reference_image: <用户提供的图片路径>`
5. 图 1/2/3 全部用 `--cref <reference_image_url> --cw 100` 锚定（Midjourney 语法）

注意：如果用户给的图是化妆后的客户照片，需要在锁卡注明 `makeup_state: post-makeup` —— 后续图 2/3 不能复制妆容色彩当成人物特征。

### 模式 2 ｜ 用户没传图，从内置人物库选 1 个（次优）

按风格主线匹配（默认推荐）：

#### P-001 ｜ 阿茶 ｜ 单眼皮淡颜韩系款（推荐韩系亚裔妆）
```yaml
persona_id: P-001
age: 25
gender: female
ethnicity_visual: East Asian
face_shape: oval
face_length: medium
eye_shape: mono-lid
eye_distance: average
nose: straight, medium bridge
lip: thin, defined cupid-bow
chin: rounded
skin_tone: cool fair
skin_texture: smooth
hair_color: dark brown
hair_style: straight shoulder bob with curtain bangs
distinctive: 左颊小痣，笑起来眼睛弯弯
```

#### P-002 ｜ 圆圆 ｜ 方圆脸日杂款（推荐日杂 / 樱花妹妆）
```yaml
persona_id: P-002
age: 22
gender: female
ethnicity_visual: East Asian (Japanese aesthetic)
face_shape: round
face_length: short
eye_shape: inner-double
eye_distance: average
nose: low bridge, button tip
lip: full, slight heart shape
chin: rounded
skin_tone: warm fair
skin_texture: smooth with very light freckles
hair_color: chocolate brown
hair_style: shoulder length wavy with side parting
distinctive: 婴儿肥，下颌线柔和，有元气感
```

#### P-003 ｜ 黎黎 ｜ 长脸千金款（推荐泰式 / 千金 / 邝玲玲风）
```yaml
persona_id: P-003
age: 28
gender: female
ethnicity_visual: East Asian (Southeast Asian feel)
face_shape: oblong
face_length: long
eye_shape: outer-double, slightly upturned
eye_distance: average
nose: high bridge, narrow
lip: full, wide
chin: pointed
skin_tone: warm medium
skin_texture: smooth
hair_color: black
hair_style: long straight with low pony or middle parting
distinctive: 颧骨清晰，气场冷冽
```

#### P-004 ｜ 桃桃 ｜ 圆脸甜心款（推荐美式甜心 / 芭比 / 洋娃娃）
```yaml
persona_id: P-004
age: 20
gender: female
ethnicity_visual: East Asian
face_shape: round to heart
face_length: short
eye_shape: outer-double, round
eye_distance: close
nose: low bridge, slightly upturned tip
lip: full, heart-shape
chin: rounded
skin_tone: warm fair
skin_texture: smooth
hair_color: chestnut
hair_style: long wavy with bangs
distinctive: 苹果肌饱满，笑容糯
```

#### P-005 ｜ 安安 ｜ 高颅顶通勤款（推荐 clean 通透 / 通勤）
```yaml
persona_id: P-005
age: 26
gender: female
ethnicity_visual: East Asian
face_shape: heart
face_length: medium
eye_shape: outer-double
eye_distance: wide
nose: straight, medium-high bridge
lip: medium full, defined
chin: pointed
skin_tone: cool medium
skin_texture: smooth
hair_color: dark brown
hair_style: high pony or low bun with face-framing layers
distinctive: 高颅顶，五官立体，通勤感强
```

### 模式 3 ｜ 用户已建自己的 custom 库

用户在 `assets/custom-personas/` 下放图，并在请求里说"用我的小桃模特"。
- 读取该图 + 用户额外的口头描述
- 生成锁卡
- 用 `--cref` 引用该本地图（Midjourney 必须是 URL，可上传到图床后用 URL）

## 四、3 张图如何复用锁卡（**关键执行细节**）

### Midjourney v6+ 语法

```
[图 1 - 主图]
<完整提示词> --ar 2:3 --style raw --seed 42

[图 2 - 细节]
<完整提示词> --ar 2:3 --style raw --cref <图1输出的URL> --cw 100 --seed 42

[图 3 - 对比 / 场景]
<完整提示词> --ar 2:3 --style raw --cref <图1输出的URL> --cw 80 --seed 42
```

参数说明：
- `--ar 2:3`：小红书最佳显示比例
- `--cref <URL>`：以指定图为人物参照
- `--cw 100`：人物权重 100，完全锁定脸（图 2 用 100，图 3 用 80 留一点姿态发挥空间）
- `--seed`：3 张图用同一个 seed 进一步稳定特征
- `--style raw`：减少 MJ 默认美化，更接近真人质感

### 即梦 / 可灵 / Sora 适配

| 工具 | 一致性参数 |
|---|---|
| **即梦（字节）** | "参考图"功能：图 1 输出后保存，图 2/3 上传图 1 作参考图，"参考强度"拉到 70-100 |
| **可灵** | "角色一致性"功能，类似即梦 |
| **Stable Diffusion** | ComfyUI IP-Adapter + FaceID + 同 seed |
| **DALL-E 3 / Sora** | 详细 prompt 描述 + ChatGPT 内引用上一张图"使用上面图片中的人物" |

### 通用降级方案（无 cref 工具）

如果用户用的工具不支持参考图（如纯文字模型），把锁卡的全部 15 项详细描述塞进每张图的 prompt，再加：

```
EXACTLY the same model, identical face structure, identical features as previous image.
DO NOT change face shape, eye shape, nose, lip, or hair.
```

## 五、人物锁卡的输出格式

每次生成笔记时，必须先单独输出一张锁卡（**作为 3 张图提示词的前置**），格式：

```
======== PERSONA LOCK CARD ========
persona_id: P-001
age: 25
face_shape: oval
eye_shape: mono-lid
... (15 项全列)
distinctive: 左颊小痣，笑起来眼睛弯弯
reference_strategy: cref-cw100 (Midjourney)
seed: 42
===================================
```

后续 3 张图的提示词里直接 reference 这张卡，不重复写 15 项。

## 六、常见出图人物失真的根因（避坑）

1. **提示词只写了"25 岁女生"，没写脸型 / 眼型** → AI 每次随机生成。**必须写满 15 项。**
2. **图 2/3 不带 --cref** → 工具默认重新随机。**必须每张图都带。**
3. **3 张图用不同 seed** → 即使加了 cref 也可能漂移。**3 张图同 seed。**
4. **图 2 妆容描述太复杂淹没了人物描述** → AI 倾向于优先满足妆容。**人物描述放在 prompt 最前 30%。**
5. **服装变化太大** → 即使同一个脸也会被读者误读为不同人。**3 张图服装色系尽量相近（如全部白色高领 / 全部米色衬衫）。**
