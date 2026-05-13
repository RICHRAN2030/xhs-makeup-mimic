# xhs-makeup-mimic

> 小红书化妆师笔记生成器 ｜ Claude Agent Skill

一个把"日期 / 妆容想法 / 参考图"自动转换为可发布的小红书笔记三件套的 Claude Skill。**人物一致性优先**：3 张图必须看起来是同一个客户。

## 特性

- **3 张 2:3 比例图片提示词**——主图 / 细节 / 对比，全部锁定同一人物
- **3 个版本的标题**——A 服务卡 / C 反问 / E 体感，覆盖不同投放策略
- **3 个版本的正文**——精简 80 字 / 标准 120 字 / 深度 150 字
- **5 个内置虚拟人物库**——单眼皮韩系 / 方圆脸日杂 / 长脸千金 / 圆脸甜心 / 高颅顶通勤
- **支持用户自带参考图**——Midjourney `--cref` / 即梦参考图模式 / SD IP-Adapter
- **基于 4245 赞爆款 DNA**——292 条原博主笔记 + 4 篇头部爆款的统计提炼
- **本地化适配**——默认地域 `都匀`，可扩 `黔南/贵阳/独山/三都/龙里/罗甸/贵定/平塘/惠水`

## 安装

### 方式 1：克隆到 Claude Code 全局 skills 目录

```bash
# Windows
git clone https://github.com/<YOUR_USERNAME>/xhs-makeup-mimic.git \
  "%USERPROFILE%\.claude\skills\xhs-makeup-mimic"

# macOS / Linux
git clone https://github.com/<YOUR_USERNAME>/xhs-makeup-mimic.git \
  ~/.claude/skills/xhs-makeup-mimic
```

### 方式 2：作为项目级 skill

```bash
cd <你的项目目录>
mkdir -p .claude/skills
git clone https://github.com/<YOUR_USERNAME>/xhs-makeup-mimic.git \
  .claude/skills/xhs-makeup-mimic
```

### 方式 3：手动复制

下载本仓库 zip，解压到 `~/.claude/skills/xhs-makeup-mimic/`。

## 使用

在 Claude Code 里随便说一句以下变体之一，skill 自动激活：

```
"今天发什么笔记好"
"我有这张妆容图想发"
"帮我想个韩系单眼皮笔记"
"周末出 3 张小猫妆图"
"都匀桃九九今天的客返发什么"
```

输入分 3 种：

### 仅日期
```
"明天发条小红书"
"母亲节发什么妆"
```

### 仅想法
```
"想发一个春日通透日杂"
"美式甜心妆出图"
```

### 想法 + 参考图
```
"按这张图发个客返：H:\客户照片\阿茶.jpg"
```

## 输出格式

```markdown
# 都匀桃九九 ｜ {主题} · {日期}

## 📋 元信息
## 👤 Persona Lock Card (15 项人物锁卡)

## 🖼️ 3 张图提示词
  ### 图 1 主图 / 封面
  ### 图 2 细节 / 局部
  ### 图 3 对比 / 上身

## 🏷️ 3 版标题 (A/C/E 三个公式)
## 📝 3 版正文 (精简/标准/深度)
## ✅ 发布前自检
```

完整示例见 [`examples/`](./examples/) 目录。

## 文件结构

```
xhs-makeup-mimic/
├── SKILL.md                         # skill 主文件（含 YAML frontmatter）
├── README.md                        # 本文件
├── LICENSE                          # MIT
├── references/
│   ├── style-dna.md                 # 博主风格 DNA 与 5 个主题子模板
│   ├── persona-anchor.md            # ⭐ 人物一致性核心：15 字段锁卡 + 5 内置人物库
│   ├── image-prompts.md             # 3 张图提示词模板（含 cref/seed 一致性语法）
│   ├── title-formulas.md            # 5 个标题公式 ABCDE
│   ├── body-templates.md            # 3 个正文字数版本
│   └── output-format.md             # 最终输出格式规范
├── examples/
│   ├── example-01-spring-jzip.md    # 仅日期输入示例
│   └── example-02-mono-lid-korean.md # 想法 + 参考图输入示例
└── assets/
    └── custom-personas/             # 用户自带人物库放这里（gitignore）
```

## 人物一致性如何实现

3 层方案（按用户输入自动选）：

### L1 ｜ 用户提供参考图
- Claude 读图 → 提取 15 项特征 → 生成 Persona Lock Card
- 3 张图都用 `--cref <参考图URL>` + 同 seed

### L2 ｜ 用户没图，从内置 5 人物库选 1 个
- P-001 阿茶 单眼皮韩系（推荐韩系亚裔妆）
- P-002 圆圆 方圆脸日杂（推荐日杂 / 樱花妹妆）
- P-003 黎黎 长脸千金（推荐泰式 / 千金 / 邝玲玲风）
- P-004 桃桃 圆脸甜心（推荐美式甜心 / 芭比 / 洋娃娃）
- P-005 安安 高颅顶通勤（推荐 clean 通透 / 通勤）

### L3 ｜ 用户自建人物库
- 把图放在 `assets/custom-personas/`
- 在请求里说"用我的小桃模特"

## 兼容的出图工具

| 工具 | 一致性参数 | 支持度 |
|---|---|---|
| Midjourney v6+ | `--cref + --cw 100 + --seed` | ⭐⭐⭐⭐⭐ |
| 即梦（字节） | 参考图功能 + 强度 80-100 | ⭐⭐⭐⭐ |
| 可灵 | 角色一致性选项 | ⭐⭐⭐⭐ |
| Stable Diffusion | IP-Adapter + FaceID + 同 seed | ⭐⭐⭐⭐ |
| DALL-E 3 / Sora | 引用前一张图 + 详细人物描述 | ⭐⭐⭐ |
| 文心 / 通义 | 同 seed + 详细人物描述 | ⭐⭐ |

## 风格 DNA 来源

本 skill 基于对 [小红书博主"花里胡哨的小搓澡巾（招学员）"](https://www.xiaohongshu.com/user/profile/5a197cb511be10033b395947) 的 292 条笔记统计分析：

- **关键词矩阵**：226 次"南京" / 143 次"约妆" / 27 次"韩系" / 23 次"亚裔" / 15 次"日杂"
- **句式模板**：55% 用 ｜ 分隔，52% 套"南京X｜"开头
- **Emoji 偏好**：‼️ × 56 / ✨ × 21 / 💕 × 17 / 🌸 × 4
- **爆款公式**：人设 vlog + 钱钩子（4245 赞）/ 妆面 + 反问（2210 赞）/ vlog（1176 赞）/ 风格融合（1082 赞）

模仿账号特化为「都匀桃九九化妆室」+ 修复原博主"零正文"短板（强制 80-160 字真实化叙事）。

## License

MIT

## 致谢

- 原博主"花里胡哨的小搓澡巾（招学员）"提供风格样本（公开数据，仅作风格分析参考）
- Claude Agent Skill 标准
- [xpzouying/xiaohongshu-mcp](https://github.com/xpzouying/xiaohongshu-mcp) — 可与本 skill 配合实现"生成 + 发布"端到端闭环
