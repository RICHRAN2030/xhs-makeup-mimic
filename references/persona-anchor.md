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

## 三、3 种使用模式（**模式 0 是默认**）

### 模式 0 ｜ 用户素颜库（**默认 / 首选**）

用户已在 `H:\【项目】\小红书0\素颜库\` 下放好 17 张素颜参考图，已注册为 8 个 Persona（P-A 至 P-H）。

**实操**：
1. 读 `assets/custom-personas/library-index.md` 看 8 个 Persona 的 14 项锁卡
2. 按用户的"风格主线"匹配速查表自动选号（如韩系亚裔 → P-A 阿茶；泰式千金 → P-H 黎黎）
3. 用户也可以明确指定（"用 P-D 桃桃"）
4. 把对应 Persona 的参考图绝对路径上传给 Nano Banana 2 / GPT-image-2 作 cref
5. JSON 的"人物锁"字段直接从 library-index.md 复制 14 项

**注**：用户素颜库**优先级高于**下面的模式 1/2/3。仅当用户明确说"不用素颜库" / "新模特" / "我传新参考图" 时才走其他模式。

### 模式 1 ｜ 用户传了参考图（非素颜库内的）

步骤：
1. 用 Read 工具读图
2. 按 15 项清单逐一识别填写
3. 输出锁卡
4. 锁卡末尾自动追加：`reference_image: <用户提供的图片路径>`
5. 图 1/2/3 全部用 `--cref <reference_image_url> --cw 100` 锚定（Midjourney 语法）

注意：如果用户给的图是化妆后的客户照片，需要在锁卡注明 `makeup_state: post-makeup` —— 后续图 2/3 不能复制妆容色彩当成人物特征。

### 模式 2 ｜ 用户没传图且没用素颜库——从内置 5 人物库选（**仅作兜底**）

> 优先级低于上面的"模式 0 用户素颜库"。仅当用户明确说"不要用素颜库"或库里没合适风格时才用。


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

### 模式 3 ｜ 用户运行时上传新参考图（临时）

用户在某次请求里说"按这张图：H:\xxx\xxx.png"。
- Read 该图
- 提取 14 项特征 → 生成临时锁卡
- 用作本次生成的 cref（不入库）

如果用户希望长期复用，引导他："要不要把这张加进 `H:\【项目】\小红书0\素颜库\`？我帮你建索引"。

## 四、3 张图如何复用锁卡（GPT-image-2 / Nano Banana 2）

> 旧版用 Midjourney 的 `--cref` `--cw` `--seed` 参数。**这套语法 GPT-image-2 / Nano Banana 2 都不识别**，强行加进去会被当成噪声忽略或拉低输出质量。本节是针对新平台的正确做法。

### Nano Banana 2 (Gemini 3 Pro Image) — **强烈推荐**

Nano Banana 2 是 2026 年 Q1 发布的多模态图像模型，**原生内建多图角色一致性能力**，是目前对"同一人物多张图"最友好的工具。

**操作方式**：

```
一次性 prompt 多图生成（推荐）：

在前置 prompt 里写：
"请生成 3 张图片，全部使用同一位模特。模特的面部结构、五官、肤色、发型
14 项特征必须严格一致。第一张为主图，后两张以第一张为视觉参考。"

然后依次粘入 IMG-01 / IMG-02 / IMG-03 的 JSON。
```

**降级方案 — 分步生成 + 参考图**：

```
1. 单独喂 IMG-01 JSON → 得到图 1
2. 把图 1 上传作为参考图 + 喂 IMG-02 JSON，开头加：
   "以上传图片中的模特为基准，保持完全相同的脸生成下一张"
3. 同理生成图 3
```

### GPT-image-2 (ChatGPT 4o Image 升级版)

GPT-image-2 没有原生 multi-image consistency 机制，靠 **对话上下文 + 详细描述** 维持一致性。

**操作方式**：

```
方式 1 — 对话连续生成：

在 ChatGPT 同一对话里按顺序粘：
- 第一条消息：粘 IMG-01 JSON → ChatGPT 生成图 1
- 第二条消息：开头加 "使用上方图片中的同一位模特" + 粘 IMG-02 JSON
- 第三条消息：开头加 "使用图 1 中的同一位模特" + 粘 IMG-03 JSON

方式 2 — 参考图上传：
- 保存图 1 → 在新对话上传图 1
- "基于参考图中的模特，按以下 JSON 生成新图"
- 粘 IMG-02 JSON
```

### 其他平台备选（如果你切换工具）

| 工具 | 一致性机制 |
|---|---|
| **Midjourney v6.1+** | `--cref <URL> --cw 100 --seed 42`（详见旧版本文件） |
| **即梦（字节）** | "参考图"功能 + 强度 80-100 |
| **可灵** | "角色一致性"开关 |
| **Stable Diffusion / ComfyUI** | IP-Adapter + InstantID + FaceID + 同 seed |

### 通用降级方案 — 任何模型都管用

把锁卡的全部 14 项详细描述**完整粘进每张图的 JSON**，不要只写"同图 1"省略。然后在 IMG-02 / IMG-03 的 JSON 末尾加一段：

```text
"硬约束": "必须与图 1 是同一位模特，完全相同的 14 项面部特征。
如果输出中出现与图 1 不同的人物，视为生成失败。"
```

## 五、人物锁卡的输出格式

每次生成笔记时，必须先单独输出一张锁卡（**作为 3 张图提示词的前置**），格式：

```json
{
  "锁卡编号": "P-001",
  "锁卡名": "阿茶 ｜ 单眼皮淡颜韩系款",
  "14项特征": {
    "年龄": 25,
    "性别": "女",
    "族裔感": "东亚",
    "脸型": "椭圆脸 / 中等长度",
    "眼型": "单眼皮",
    "眼距": "适中",
    "鼻型": "笔挺中等鼻梁",
    "唇型": "薄唇饱满唇珠",
    "下巴": "圆润",
    "肤色": "冷调白皙",
    "肤质": "光滑细腻",
    "发型": "深棕长直发 + 空气刘海",
    "辨识度": "左颊小痣，笑起来眼睛弯弯"
  },
  "推荐工具": "Nano Banana 2 一次多图模式 / GPT-image-2 对话连续模式",
  "参考图路径": "<如果用户提供>"
}
```

后续 3 张图的 JSON 里直接复制 `14项特征` 到"人物锁"字段，不要省略写"同图 1"——模型对省略不稳定。

## 六、常见出图人物失真的根因（避坑）

1. **JSON 里只写了"25 岁女生"，没写脸型 / 眼型** → AI 每次随机生成。**必须写满 14 项。**
2. **图 2/3 用"同图 1"省略** → 模型不知道图 1 的具体特征，会重新随机。**必须每张图都把 14 项完整粘进去。**
3. **图 2 妆容描述太复杂淹没了人物描述** → AI 倾向于优先满足妆容。**JSON 里"人物锁"字段放在最前面，"妆容"放后面。**
4. **服装变化太大** → 即使同一个脸也会被读者误读为不同人。**3 张图服装色系尽量相近（如全部白色高领 / 全部米色针织）。**
5. **没用参考图机制** → 单靠文字描述，14 项再细也会漂移。**有条件就用"参考图上传"+"硬约束"双保险。**
6. **混入 Midjourney 参数** → GPT-image-2 / Nano Banana 2 不识别 `--ar` `--cref`，会被当噪声处理，反而干扰生成。**这两个平台 prompt 不要带任何 `--XX` 参数。**
