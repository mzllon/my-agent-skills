# AGENTS.md

> ⚠️ 本文件是入口指针，**不包含任何项目实质内容**。
> 本项目的所有上下文（项目性质、目录结构、开发规范、工作流、术语表）均维护在 [`./CLAUDE.md`](./CLAUDE.md) 中。

## 如何建立项目上下文

1. **首先**：打开并完整阅读 [`./CLAUDE.md`](./CLAUDE.md)。
2. **然后**：按 `CLAUDE.md`「详细文档」索引表，读取与当前任务相关的 `docs/*` 文件。
3. **执行任务时**：遵循 `CLAUDE.md` 中的「Document Update Rules」维护文档。

## 为什么不直接把内容写在本文件

为避免在 `AGENTS.md` 与 `CLAUDE.md` 之间重复维护两份内容、导致不一致，本仓库采用**单一信息源**策略：`CLAUDE.md` 为唯一权威，`AGENTS.md` 仅负责把通用 Agent 工具（Copilot、Cursor 等）引导过去。

> 因此：**不要在本文件中补充任何项目实质内容**；如有变更，统一改 `CLAUDE.md` 及其引用的 `docs/*`。
