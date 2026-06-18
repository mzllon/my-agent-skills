# 开发规范

## 一、Skill 命名

- 全小写 + 连字符（kebab-case），如 `code-review`、`docx-export`。
- 目录名必须与 `SKILL.md` front matter 中的 `name` 字段一致。
- 名称应能体现用途，避免过短或含义模糊（如 `util`）。

## 二、SKILL.md 结构

由两部分组成：YAML Front Matter + Markdown 正文。

### 1. Front Matter（必需）

| 字段          | 必需 | 说明                                                                       |
| ------------- | ---- | -------------------------------------------------------------------------- |
| `name`        | ✅   | Skill 唯一标识，需与目录名一致，kebab-case。                              |
| `description` | ✅   | **决定 Agent 是否触发本 Skill 的关键**。需写清楚：能做什么、何时用、何时不用。 |
| `source`      | ✅   | 来源类型：`original`（原创）或 `collected`（公开收集）。                  |
| `author`      | collected 必需 | 原作者署名（个人 / 团队 / 组织名）。                              |
| `source_url`  | collected 必需 | 原始来源 URL（仓库、博客、文档等）。                              |
| `license`     | collected 必需 | 原 Skill 的许可证（如 MIT、Apache-2.0、GPL-3.0）。                |

#### Front Matter 示例

原创：

```yaml
---
name: code-review
description: 当用户要求评审代码……（覆盖触发词与适用场景）
source: original
---
```

收集：

```yaml
---
name: git-commit
description: 规范化 Git 提交流程……
source: collected
author: zcode-plugins-official
source_url: https://github.com/.../git-commit
license: Apache-2.0
---
```

### 2. description 撰写要点

Agent 仅依据 `description` 判断是否调用本 Skill，因此：

- **明确触发词**：把用户最可能提到的关键词写进去（如"提交代码""commit""push"）。
- **覆盖场景**：列出典型适用与不适用情形。
- **避免空泛**：不要写"一个有用的工具"这类无法匹配的描述。

✅ 好的例子：

> 规范化 Git 提交流程。当用户要求提交代码、commit、push，或者提到"提交"、"commit"时必须使用此 skill。无论请求看起来多简单，都必须严格遵循此流程。

❌ 不好的例子：

> 一个帮助处理 Git 的工具。

### 3. 正文结构（建议）

```
# <Skill 名称>
## 何时使用 / 何时不使用
## 前置条件
## 执行步骤           ← 核心部分，要可被 Agent 严格遵循
## 输入 / 输出
## 异常处理
## 参考资料
```

步骤应当**具体、可执行、有顺序**；遇到分支要明确给出判断条件。

## 三、目录组织

```
skills/<skill-name>/
├── SKILL.md             # 必需
├── scripts/             # 可选，辅助脚本（Python / Node / Shell 等）
├── templates/           # 可选，模板文件
├── assets/              # 可选，静态资源
├── README.md            # 可选，给人类阅读的说明（与 SKILL.md 互补）
├── ATTRIBUTION.md       # collected 类必需：原作者署名、来源链接、原许可证
└── LICENSE              # collected 类必需（当原许可证 ≠ Apache-2.0 时）
```

- 每个 Skill 目录应**自包含**，可独立拷贝使用。
- 避免跨 Skill 的硬编码路径依赖。

## 三-补、来源与许可证规范

| source | 必需 front matter | 必需文件 |
| --- | --- | --- |
| `original` | `name`、`description`、`source` | 无（默认 Apache-2.0） |
| `collected` | `name`、`description`、`source`、`author`、`source_url`、`license` | `ATTRIBUTION.md`；`LICENSE`（原许可证 ≠ Apache-2.0 时） |

**`collected` 类硬性规则**：

1. 不得删除 / 篡改原作者署名、版权声明、许可证声明。
2. 原则上**保留原 SKILL.md 正文不动**，仅补充 front matter。如有本地化改动（翻译、适配），在 `ATTRIBUTION.md`「本地改动」一节如实记录。
3. 原许可证**不明或无** → 不得收录。
4. 上游更新同步后，更新 `ATTRIBUTION.md` 的「抓取版本」字段。

`ATTRIBUTION.md` 模板见 [../CONTRIBUTING.md](../CONTRIBUTING.md) 第四节。

## 四、脚本规范

- 脚本文件头部需注释说明：用途、入参、依赖。
- Python 脚本使用 Python 3，需在文档中声明依赖（`requirements.txt` 或注释）。
- Node 脚本需在 `package.json` 中声明依赖。
- 默认不提交 `node_modules/`、`__pycache__/` 等产物（已被 `.gitignore` 忽略）。

## 五、提交信息规范

使用 **Conventional Commits** 风格：

| 场景               | 示例                                       |
| ------------------ | ------------------------------------------ |
| 新增 Skill          | `feat(skills): add <skill-name>`           |
| 修改 Skill          | `fix(<skill-name>): correct step ordering` |
| 更新文档           | `docs: update README skill index`          |
| 工程化 / 配置调整  | `chore: refine .gitignore`                 |

## 六、语言与风格

- 文档以中文为主，关键术语保留英文原词（如 `description`、`commit`、`kebab-case`）。
- 代码注释使用中文。
