# 项目术语表（Context）

> 本文件定义本仓库的核心概念、模块职责和已知限制，供 Agent 和人类快速建立上下文。

## 核心概念

### Skill
一个可被 Agent 按需加载的能力单元。在本仓库中表现为 `skills/<name>/` 下的一个自包含目录，以 `SKILL.md` 为入口。Agent 依据 `SKILL.md` 中的 `description` 字段决定是否触发该 Skill。

### SKILL.md
Skill 的入口文件，由 YAML front matter（`name` + `description`）和 Markdown 正文组成。正文描述具体的执行步骤。

### description（触发描述）
`SKILL.md` front matter 中的关键字段，**直接决定 Skill 是否被 Agent 触发**。必须清晰描述「能做什么 / 何时用 / 何时不用」并覆盖典型触发词。

### kebab-case
本仓库采用的命名风格：全小写 + 连字符，如 `code-review`、`git-commit`。

## 模块职责

| 路径                | 职责                                                                 |
| ------------------- | -------------------------------------------------------------------- |
| `skills/`           | 所有 Skill 的根目录，每个子目录是一个自包含 Skill                    |
| `skills/skill-template/` | 新建 Skill 的起点模板，复制后修改即可                              |
| `docs/`             | 项目详细文档（架构、规范、工作流、教训记录）                         |
| `CONTRIBUTING.md`   | 面向贡献者的 Skill 编写 / 新增指南                                   |
| `CLAUDE.md`         | Claude Code 项目上下文（纯索引文件）                                 |
| `AGENTS.md`         | 通用 Agent 项目上下文（与 CLAUDE.md 内容保持一致）                   |
| `CONTEXT.md`        | 本文件，术语表                                                       |

## 已知限制

- 本仓库**仅用于个人沉淀 Agent Skills**，不是一个可运行的应用。
- 本仓库**与 Java / Maven 无关**；早期 `.gitignore` 中的 Maven 条目是创建仓库时的失误，已清理。
- Skills 的实际加载与运行依赖外部 Agent 运行时（ZCode / Claude Code 等），仓库本身只负责存放与版本管理。

## 外部依赖的 Skills（运行时）

本仓库的 Skill 在执行时可能调用以下外部 Skill（来自本地环境，不属于本仓库）：

| Skill 名称                  | 用途                                     |
| --------------------------- | ---------------------------------------- |
| `git-commit`                | 规范化 Git 提交流程                      |
| `skill-creator`             | 从零编写或迭代 SKILL.md                  |
| `docx` / `pdf`              | 文档生成与处理                           |

> 调用这些 Skill 时，遵循它们各自的 SKILL.md 约定。
