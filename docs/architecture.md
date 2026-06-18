# 项目架构

## 仓库性质

这是一个**个人 Agent Skills 仓库**，不是软件代码项目，**不是 Java / Maven 项目**（早期 `.gitignore` 中的 Maven 条目是仓库创建时的遗留失误，已清理）。

仓库的作用：沉淀作者日常常用的 Agent Skills，每个 Skill 是 `skills/` 下一个自包含的目录，以 `SKILL.md` 为入口，供 ZCode / Claude Code 等支持 Skills 机制的 Agent 按需加载调用。

## 目录结构

```
my-agent-skills/
├── README.md              # 项目说明 + Skills 索引表（新增 Skill 后需同步更新）
├── CONTRIBUTING.md        # 如何编写 / 新增 / 维护一个 Skill
├── CLAUDE.md              # Claude Code 上下文（纯索引，无实质内容）
├── AGENTS.md              # 通用 Agent 上下文（内容与 CLAUDE.md 保持一致）
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
        ├── SKILL.md       # Skill 入口（必需，含 YAML front matter）
        ├── scripts/       # 可选：辅助脚本
        ├── templates/     # 可选：模板文件
        └── assets/        # 可选：静态资源
```

`skills/skill-template/` 是新建 Skill 的起点模板。

## 关键约定

处理本仓库任务时请遵循以下约定：

1. **Skill 命名**：小写 + 连字符（kebab-case），目录名需与 `SKILL.md` 的 `name` 字段一致。
2. **SKILL.md 结构**：YAML front matter（`name`、`description` 必需）+ Markdown 正文。
   - `description` 是 Agent 决定是否触发该 Skill 的关键依据，需写清楚「能做什么 / 何时用 / 何时不用」并覆盖典型触发词。
3. **自包含**：每个 Skill 目录应可独立拷贝使用，避免跨 Skill 的硬编码路径依赖。
4. **新增 Skill 后必须同步更新**根目录 `README.md` 的「已收录 Skills」表格。
5. **文档以中文为主**，关键术语保留英文原词。
6. **本仓库不涉及任何 Java / Maven 构建**，不要引入 `pom.xml`、`target/` 等。

详细的编写规范见 [coding-standards.md](./coding-standards.md) 与根目录 [CONTRIBUTING.md](../CONTRIBUTING.md)。
