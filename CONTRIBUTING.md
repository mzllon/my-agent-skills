# 贡献指南 / 如何编写一个 Skill

本仓库用于沉淀**个人常用**的 Agent Skills。欢迎按以下规范新增或维护 Skill。

## 一、何时应该沉淀成一个 Skill

满足以下任一条件，就值得抽象成 Skill：

- 一段会被**反复执行**的工作流（如代码评审、文档导出、内部系统对接）。
- 包含**固定步骤 + 判断分支**，单纯靠对话难以稳定复现。
- 需要**附加脚本 / 模板 / 资源文件**，不适合直接放在对话里。

## 二、目录约定

```
skills/
└── <skill-name>/            # kebab-case，与 SKILL.md 的 name 字段一致
    ├── SKILL.md             # 必需，Skill 入口
    ├── scripts/             # 可选，辅助脚本（Python / Node / Shell 等）
    ├── templates/           # 可选，模板文件
    ├── assets/              # 可选，静态资源
    └── README.md            # 可选，给人类阅读的说明（与 SKILL.md 互补）
```

> 推荐**复制** `skills/skill-template/` 作为起点，再按需修改。

## 三、SKILL.md 编写规范

`SKILL.md` 由两部分组成：YAML Front Matter + Markdown 正文。

### 1. Front Matter（必需）

| 字段          | 必需 | 说明                                                                       |
| ------------- | ---- | -------------------------------------------------------------------------- |
| `name`        | ✅   | Skill 唯一标识，需与目录名一致，kebab-case。                              |
| `description` | ✅   | **决定 Agent 是否触发本 Skill 的关键**。需写清楚：能做什么、何时用、何时不用。 |

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

## 四、新增 Skill 的完整流程

1. 复制 `skills/skill-template/` → `skills/<your-skill-name>/`。
2. 修改 `SKILL.md`：填写 `name`、`description`，写好正文步骤。
3. （可选）放入 `scripts/`、`templates/` 等辅助文件，并在 SKILL.md 中说明调用方式。
4. 自测：在一个新的 Agent 会话里用自然语言触发，确认能被正确识别和执行。
5. 更新根目录 `README.md` 的「已收录 Skills」表格。
6. 提交：

   ```bash
   git add skills/<your-skill-name> README.md
   git commit -m "feat(skills): add <your-skill-name>"
   ```

## 五、维护已有 Skill

- 修改 `description` 时务必同步考虑触发可靠性，避免误触发或漏触发。
- 步骤有调整时，记得同步更新正文示例与「注意事项」。
- 若 Skill 不再使用，建议直接删除目录而非保留过期内容。

## 六、命名与风格

- 目录名、`name` 字段：小写 + 连字符（kebab-case）。
- 文档使用中文为主，关键术语保留英文原词。
- 脚本需在文件头部注释说明用途、入参、依赖。
