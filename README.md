# my-agent-skills

> 我常用的 Agent SKILLS 集合 —— 把重复的工作流沉淀为可复用技能，供 ZCode / Claude 等支持 Skills 机制的 Agent 直接调用。

## 📌 项目简介

本仓库用于**个人沉淀和版本管理**我在日常开发、文档处理、内部系统对接等场景下常用的 Agent Skills。每个 Skill 是一个独立目录，以 `SKILL.md` 为入口，配合必要的脚本与资源文件，可以被 Agent 运行时按需加载。

## 🗂️ 目录结构

```
my-agent-skills/
├── README.md              # 本说明文件
├── CONTRIBUTING.md        # 如何编写 / 新增一个 Skill
├── LICENSE                # Apache-2.0
├── .gitignore
└── skills/                # 所有 Skill 的根目录
    └── <skill-name>/      # 每个 Skill 一个独立目录
        ├── SKILL.md       # Skill 入口（必需）
        ├── scripts/       # 可选：辅助脚本
        ├── templates/     # 可选：模板文件
        └── assets/        # 可选：静态资源
```

## 📚 已收录 Skills

| Skill | 说明 | 状态 |
| ----- | ---- | ---- |
| _(待补充)_ | | |

> 新增 Skill 后，请同步更新本表格。

## 🚀 使用方式

### 方式一：克隆到本地 Skills 目录

```bash
# ZCode CLI 默认个人 skills 目录
git clone git@github.com:mzllon/my-agent-skills.git ~/.agents/my-agent-skills

# 或建立软链，将需要的 skill 链接到 ~/.agents/skills/
```

### 方式二：按需拷贝单个 Skill

每个 Skill 目录是自包含的，可直接把 `<skill-name>/` 拷贝到任意支持 Skills 的 Agent 加载路径下。

## 🛠️ 新增 Skill

详见 [CONTRIBUTING.md](./CONTRIBUTING.md)。简要步骤：

1. 在 `skills/` 下新建 `<skill-name>/` 目录（小写、连字符命名，如 `code-review`）。
2. 编写 `SKILL.md`（必须包含 `name`、`description`，参考模板）。
3. 按需放入 `scripts/`、`templates/` 等辅助文件。
4. 更新本 README 的「已收录 Skills」表格。
5. 提交 PR / 直接提交。

## 📄 许可证

[Apache License 2.0](./LICENSE)
