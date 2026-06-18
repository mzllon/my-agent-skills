# 工作流（常见任务指引）

## 一、新增 Skill

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

详细规范见 [coding-standards.md](./coding-standards.md) 与根目录 [../CONTRIBUTING.md](../CONTRIBUTING.md)。

## 二、修改已有 Skill

- 调整步骤时**同步更新正文示例与「注意事项」**。
- 修改 `description` 时务必重新评估触发可靠性（避免误触发或漏触发）。
- 若涉及行为变更，需在 commit message 中说明动机。

## 三、删除 Skill

- 直接删除对应目录，并从根目录 `README.md` 表格移除对应行。
- **不要保留过期内容**；如需历史，依靠 git 历史而非留在仓库里。

## 四、提交代码

用户要求提交 / commit / push 时：

- **必须使用 `git-commit` skill**，遵循其规范流程。
- 关键约束：
  - 禁止 `git add -A`，需明确指定文件。
  - 提交前以树形格式展示待提交文件清单（含未纳入文件）供用户确认。
  - 展示 commit message 供用户审阅。
  - 提交后自动推送到远端。

## 五、文档维护

任务完成后按 `CLAUDE.md` 的「Document Update Rules」检查：

1. 检查现有文档是否需要更新（新 Skill、新约定、新决策）。
2. 同一类错误犯了第二次 → 补充到 [lessons.md](./lessons.md)。
3. 新增了 `docs/` 文档 → 在 `CLAUDE.md` / `AGENTS.md` 索引表加一行。
4. `CLAUDE.md` / `AGENTS.md` 不放任何实质内容，所有内容在 `docs/` 对应文件中维护。
