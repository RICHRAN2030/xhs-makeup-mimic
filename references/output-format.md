# 输出格式 ｜ 最终交付物组装规范

> 8 步法走完后，按本文件格式组装最终输出给用户。**一次性输出全套**，不要分多次。

## 完整输出模板

```markdown
# 都匀桃九九｜{主题名}笔记 · {日期}

## 📋 元信息
- 主题分类：{A 妆面 / B vlog / C 招生 / D 改造 / E 情绪}
- 风格主线：{日杂 / 韩系亚裔 / ...}
- 受众细分：{单眼皮 / 方圆脸 / ...}
- 钱钩子：{月入1w+ / 399 周末班 / 无}
- 节日 / 季节钩子：{春日 / 演唱会季 / 母亲节 / 无}

## 👤 Persona Lock Card（人物锁卡）

```yaml
persona_id: <P-XXX 或自定义>
age: 25
gender: female
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
reference_strategy: Midjourney --cref --cw100
seed: 42
```

> 同一人物 3 张图共享上方锁卡。若用即梦/可灵，把图 1 输出后作为参考图传给图 2/图 3。

## 🖼️ 3 张图提示词

### 图 1 ｜ 主图 / 封面

```
<完整图 1 提示词（按 image-prompts.md 图 1 模板）>
--ar 2:3 --style raw --seed 42
```

### 图 2 ｜ 细节特写

```
<完整图 2 提示词（按 image-prompts.md 图 2 模板）>
--ar 2:3 --style raw --cref <PLACEHOLDER_IMG1_URL> --cw 100 --seed 42
```

### 图 3 ｜ 对比 / 上身

```
<完整图 3 提示词（按 image-prompts.md 图 3 模板）>
--ar 2:3 --style raw --cref <PLACEHOLDER_IMG1_URL> --cw 80 --seed 42
```

## 🏷️ 3 版标题

| 版本 | 公式 | 字数 | 标题 |
|---|---|---|---|
| **A 服务卡式** | A | XX | <标题 1> |
| **C 反问型** | C | XX | <标题 2> |
| **E 体感动词** | E | XX | <标题 3> |

> 推荐：发布时 A/E 二选一作主标题，C 作评论区置顶引互动。

## 📝 3 版正文

### 精简版 ｜ 80-100 字

```
<完整正文，含 hashtag>
```

### 标准版 ｜ 110-130 字 ★ 推荐

```
<完整正文，含 hashtag>
```

### 深度版 ｜ 140-160 字

```
<完整正文，含 hashtag>
```

## ✅ 发布前自检清单

- [ ] 3 张图全部 2:3 比例
- [ ] 3 张图人物锁卡一致（用 cref / seed / 同特征描述）
- [ ] 标题 12-22 字，含地域词 + 风格词 + Emoji
- [ ] 正文 80-160 字，含客户故事 + 技术解读 + 价格信号 + hashtag
- [ ] 至少 1 个具体产品名（增加种草价值）
- [ ] 末尾"都匀桃九九化妆室 ｜ 约妆 / 招学员私我宝～"
- [ ] 评论区前 30 分钟回复率目标 ≥50%
- [ ] 同一账号不能在网页端 + xiaohongshu-mcp 同时登录

## 🔧 出图工具适配 hint

| 工具 | 操作 |
|---|---|
| **Midjourney** | 直接复制提示词，先出图 1，再用图 1 URL 替换图 2/3 的 `<PLACEHOLDER_IMG1_URL>` |
| **即梦（字节）** | 复制 prompt 主体，删除 `--cref` 等 MJ 参数；图 1 出完后上传作为图 2/3 的参考图，强度 80-100 |
| **可灵** | 同即梦，开启"角色一致性" |
| **Stable Diffusion** | 复制 prompt 主体，启用 IP-Adapter + FaceID，权重 0.8-1.0，同 seed |
| **DALL-E (GPT)** | 复制 prompt，图 2/3 加一句"使用上面图片里的模特，相同脸" |

---

🎯 *若任何一项不满意，告诉我"图 X 换 Y" 或 "标题 N 再野一点"，我只改那一项不重做*
```

## 输出风格注意

1. **不要附加解释**——输出完三件套就停。用户要原理会单独问。
2. **不要过度道歉**——如果信息不全，直接用合理默认值产出，不要先连珠炮提问。
3. **必须包含"PLACEHOLDER"占位**——告诉用户图 1 出完后替换。否则用户会迷茫。
4. **Persona Lock Card 用 YAML 块**——便于复制到其他工具或保存。

## 异常处理

| 情况 | 处理 |
|---|---|
| 用户只给日期，无主题 | 默认 A 妆面 + 日杂 + 内置 P-002 人物 |
| 用户传了图但模糊 / 看不清 | 用图里能看清的特征 + 内置人物库补全缺失项 |
| 用户输入的妆容词不在风格矩阵 | 选最接近的主线，备注"建议改为 X 主线，黔南三线本地接受度更高" |
| 用户要求"5 张图" | 在 image-prompts 基础上加图 4（不同表情）+ 图 5（场景广角），全部用同一 cref + seed |
| 用户要求"只要一版" | 只给标准版正文 + A 公式标题 + 图 1 |
