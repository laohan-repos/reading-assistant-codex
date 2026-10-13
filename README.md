# 读书助手 · Reading Assistant for Codex

一个运行在 Codex 中的项目级 skill。输入书名，或让助手随机选书，即可整理中文阅读笔记，并生成可编辑的 Word 文档，保存到当前工作区。

适合梳理全书内容、制作读书笔记、准备阅读讨论和写读后感。

## 功能

- 根据书名整理作品，也支持随机选书。
- 按七个部分组织阅读笔记，覆盖书籍信息、作者、背景、情节、主题、章节和阅读思考。
- 核实重要事实，保留来源链接，区分史实、学术争议和阅读解读。
- 支持指定版本、受众、篇幅、逐章分析或无剧透要求。
- 将内容导出为 Word，并检查中文显示、表格和分页。
- 支持把同一对话中已有的阅读整理内容直接保存为 Word。

## 快速开始

### 1. 获取项目

从 GitHub 克隆：

```bash
git clone https://github.com/laohan-repos/reading-assistant-codex.git
cd reading-assistant-codex
```

也可以从 Gitee 克隆：

```bash
git clone https://gitee.com/laohan_repos/reading-assistant-codex.git
cd reading-assistant-codex
```

### 2. 在 Codex 中打开项目

将克隆后的目录作为当前工作区。skill 位于项目内的 `.agents/skills/reading-assistant/`，按 [Codex 的项目级 skill 发现规则](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)加载，无需复制到用户全局 skill 目录。

如果新 skill 未出现在列表中，可重启 Codex 后再打开项目。

### 3. 输入阅读请求

在项目聊天中输入：

```text
使用 $reading-assistant 整理《西游记》，生成七部分阅读笔记，并保存为 Word。
```

也可以直接使用自然语言：

```text
用读书助手整理《小王子》。
```

Word 导出依赖当前 Codex 环境中可用的 `documents:documents` 技能及其文档生成、渲染工具。本仓库包含阅读整理规则和导出参考，不内置独立的 Word 生成程序。

## 阅读笔记的七个部分

| 部分 | 内容 |
| --- | --- |
| 书籍基本信息 | 书名、作者、时代或出版时间、类型、版本范围与作品结构 |
| 作者介绍 | 作者身份、主要经历、代表作品及与本书相关的文学特点 |
| 创作背景 | 历史社会环境、作品形成或出版背景、文化思想环境 |
| 故事概括 | 起因、发展、转折与结局，以及主要人物和冲突 |
| 内容总结 | 主要主题、人物特点、核心观点和表达方式 |
| 章节分析 | 依据真实目录或回目覆盖全书，并分析代表性章节 |
| 阅读思考 | 结合原文的讨论问题、思考方向和读后感写作方法 |

非虚构作品以论述或叙事主线代替故事情节，着重整理核心论点、证据和适用条件；诗集、散文集按真实篇目、主题或分辑分析。

长篇作品默认可以按连续阶段合并章节，但须覆盖全书。需要逐章分析时，请在请求中明确说明。

## 使用示例

**随机选书**

```text
用读书助手随机选一本书，整理七个部分并保存为 Word。
```

**指定分析方式**

```text
使用 $reading-assistant 整理《红楼梦》，章节分析按全书阶段展开，重点分析人物关系。
```

**指定受众与剧透范围**

```text
用读书助手整理《小王子》，面向初中生，只要无剧透提纲，暂不生成 Word。
```

**导出已有内容**

```text
把上面整理好的《活着》阅读内容完整保存为 Word，保留表格和来源链接。
```

未指定版本时，采用通行完整版并说明版本范围；默认包含结局。需要指定译者、版本或避免剧透时，请在请求中注明。

## 文件命名与保存

Word 文件默认保存在当前工作区根目录，命名规则为：

```text
书名_阅读整理_YYYYMMDD.docx
```

例如，在 2026 年 10 月 13 日生成《西游记》的阅读整理：

```text
西游记_阅读整理_20261013.docx
```

日期采用生成时用户当地日期，书名不带外层《》。同名文件已存在且未授权覆盖时，使用 `_v2`、`_v3` 等后缀保留已有文件。也可以指定保存目录和文件名。

生成的 Word 文档可随项目提交到仓库；`.gitignore` 仅忽略 Word 临时锁文件和 macOS 的 `.DS_Store`。渲染预览和检查用文件默认放在临时目录。

## 示例文档

- [小王子 · 阅读整理](小王子_阅读整理_20261012.docx)
- [西游记 · 阅读整理](西游记_阅读整理_20261012.docx)

## 项目结构

```text
reading-assistant-codex/
├── .agents/
│   └── skills/
│       └── reading-assistant/
│           ├── SKILL.md                # 阅读整理规则与工作流程
│           ├── agents/
│           │   └── openai.yaml         # 界面名称和默认调用提示
│           └── references/
│               └── word-export.md      # Word 导出与检查参考
├── .gitignore
├── README.md
├── 小王子_阅读整理_20261012.docx
└── 西游记_阅读整理_20261012.docx
```

修改阅读整理流程时，编辑 [SKILL.md](.agents/skills/reading-assistant/SKILL.md)；修改 Word 导出约定时，编辑 [word-export.md](.agents/skills/reading-assistant/references/word-export.md)。

## 仓库地址

- [GitHub](https://github.com/laohan-repos/reading-assistant-codex)
- [Gitee](https://gitee.com/laohan_repos/reading-assistant-codex)
