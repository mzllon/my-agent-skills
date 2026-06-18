# 项目架构

## 仓库性质

这是一个**个人 Agent Skills 仓库**，不是软件代码项目，**不是 Java / Maven 项目**（早期 `.gitignore` 中的 Maven 条目是仓库创建时的遗留失误，已清理）。

仓库的作用：归档日常常用的 Agent Skills。**Skill 有两类来源**：

| source | 含义 | 许可证要求 |
| --- | --- | --- |
| `original` | 本人原创编写 | 默认 Apache-2.0（沿用仓库 LICENSE） |
| `collected` | 公开收集、个人在用、觉得不错（非原创） | **必须严格保留**原作者署名、原许可证、来源链接；含 `ATTRIBUTION.md` |

每个 Skill 是 `skills/` 下一个自包含的目录，以 `SKILL.md` 为入口，供 ZCode / Claude Code 等支持 Skills 机制的 Agent 按需加载调用。

## 目录结构

```
my-agent-skills/
├── README.md              # 项目说明 + Skills 索引表（新增 Skill 后需同步更新）
├── CONTRIBUTING.md        # 如何编写 / 新增 / 维护一个 Skill
├── CLAUDE.md              # Claude Code 上下文（纯索引，无实质内容）
├── AGENTS.md              # 通用 Agent 上下文（引导读 CLAUDE.md）
├── CONTEXT.md             # 项目术语表
├── LICENSE                # Apache-2.0
├── .gitignore
├── docs/                  # 详细文档
│   ├── architecture.md    # 本文件
│   ├── coding-standards.md
│   ├── workflow.md
│   └── lessons.md
└── skills/                # 所有 Skill 的根目录
    ├── README.md
    └── <skill-name>/      # 每个 Skill 一个独立目录（kebab-case）
        ├── SKILL.md       # Skill 入口（必需，含 YAML front matter，含 source 字段）
        ├── scripts/       # 可选：辅助脚本
        ├── templates/     # 可选：模板文件
        ├── assets/        # 可选：静态资源
        ├── ATTRIBUTION.md # collected 类必需：原作者署名、来源链接、原许可证
        └── LICENSE        # collected 类必需（当原许可证 ≠ Apache-2.0 时）
```

`skills/skill-template/` 是新建 Skill 的起点模板。

## 关键约定

处理本仓库任务时请遵循以下约定：

1. **Skill 命名**：小写 + 连字符（kebab-case），目录名需与 `SKILL.md` 的 `name` 字段一致。
2. **SKILL.md 结构**：YAML front matter（`name`、`description`、`source` 必需）+ Markdown 正文。
   - `description` 是 Agent 决定是否触发该 Skill 的关键依据，需写清楚「能做什么 / 何时用 / 何时不用」并覆盖典型触发词。
   - `source` 必填，值为 `original`（原创）或 `collected`（公开收集）。
3. **来源合规**：`collected` 类 Skill 必须**严格保留**原作者署名、原许可证、来源链接，并附 `ATTRIBUTION.md`；许可证不明的代码不得收录。
4. **自包含**：每个 Skill 目录应可独立拷贝使用，避免跨 Skill 的硬编码路径依赖。
5. **新增 Skill 后必须同步更新**根目录 `README.md` 的「已收录 Skills」表格（含 `source` 列）。
6. **文档以中文为主**，关键术语保留英文原词。
7. **本仓库不涉及任何 Java / Maven 构建**，不要引入 `pom.xml`、`target/` 等。

详细的编写规范见 [coding-standards.md](./coding-standards.md) 与根目录 [CONTRIBUTING.md](../CONTRIBUTING.md)。
