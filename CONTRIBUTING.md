# 贡献指南 / 如何编写或收集一个 Skill

本仓库用于归档**个人常用**的 Agent Skills。Skill 有两类来源，处理方式不同：

| source | 来源 | 适用场景 |
| --- | --- | --- |
| `original` | 本人原创 | 把自己重复执行的工作流沉淀成 Skill |
| `collected` | 公开收集 | 看到别人写得不错、自己在用、想归档方便查找的公开 Skill |

## 一、何时应该沉淀成一个 Skill

满足以下任一条件，就值得（原创或收集）放进本仓库：

- 一段会被**反复执行**的工作流（如代码评审、文档导出、内部系统对接）。
- 包含**固定步骤 + 判断分支**，单纯靠对话难以稳定复现。
- 需要**附加脚本 / 模板 / 资源文件**，不适合直接放在对话里。
- 发现一个**公开的优秀 Skill**，自己已在用，希望集中归档以便查找。

## 二、目录约定

```
skills/
└── <skill-name>/            # kebab-case，与 SKILL.md 的 name 字段一致
    ├── SKILL.md             # 必需，Skill 入口
    ├── scripts/             # 可选，辅助脚本
    ├── templates/           # 可选，模板文件
    ├── assets/              # 可选，静态资源
    ├── README.md            # 可选，给人类阅读的说明
    ├── ATTRIBUTION.md       # collected 类必需，署名与来源信息
    └── LICENSE              # collected 类必需（当原许可证 ≠ Apache-2.0 时）
```

> 推荐**复制** `skills/skill-template/` 作为起点，再按需修改。

## 三、SKILL.md 编写规范

`SKILL.md` 由两部分组成：YAML Front Matter + Markdown 正文。

### 1. Front Matter（必需）

| 字段          | 必需 | 说明                                                                       |
| ------------- | ---- | -------------------------------------------------------------------------- |
| `name`        | ✅   | Skill 唯一标识，需与目录名一致，kebab-case。                              |
| `description` | ✅   | **决定 Agent 是否触发本 Skill 的关键**。需写清楚：能做什么、何时用、何时不用。 |
| `source`      | ✅   | 来源类型：`original`（原创）或 `collected`（公开收集）。                  |
| `author`      | collected 必需 | 原作者署名（个人 / 团队 / 组织名）。                              |
| `source_url`  | collected 必需 | 原始来源 URL（仓库、博客、文档等）。                              |
| `license`     | collected 必需 | 原 Skill 的许可证（如 MIT、Apache-2.0、GPL-3.0）。                |

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

> ⚠️ 对于 `collected` 类 Skill：原则上**保留原 SKILL.md 正文内容不动**，仅补充 front matter 元数据。如确有本地化修改（如翻译、适配），在 ATTRIBUTION.md 中「本地改动」一节如实记录。

## 四、来源与许可证规范（重要）

### `original` 类（原创）

- 默认采用仓库的 [Apache License 2.0](./LICENSE)，**无需**额外文件。
- front matter 不需要 `author` / `source_url` / `license` 字段（但可自愿填 `author` 标注自己）。

### `collected` 类（公开收集）

**必须严格保留原作者权益**，这是合规底线：

1. **front matter 完整填写**：`source: collected` + `author` + `source_url` + `license`。
2. **新增 `ATTRIBUTION.md`**（见下方模板），记录：
   - 原作者、原仓库 / 来源链接
   - 原许可证类型与全文链接
   - 抓取 / 同步时的 commit / 版本号
   - 本地化改动说明（如有）
3. **许可证文件处理**：
   - 原许可证为 **Apache-2.0 / MIT / BSD** 等宽松许可 → 保留原 `LICENSE` 文件于 Skill 目录内即可。
   - 原许可证为 **GPL / LGPL / AGPL** 等 copyleft 许可 → 必须在 Skill 目录内保留原 `LICENSE` 全文。
   - 原许可证**不明或无** → **不要收录**。无法确认许可证的代码不应进入本仓库。
4. **不得删除或篡改**原作者署名、版权声明、许可证声明。
5. 如原 Skill 的 `SKILL.md` 中含版权声明，原样保留。

### ATTRIBUTION.md 模板

```markdown
# Attribution — <skill-name>

- **原作者 / 来源**：<author>
- **原始链接**：<source_url>
- **原许可证**：<license>
- **抓取版本 / commit**：<commit-sha 或 tag 或日期>
- **本地改动**：
  - 如实列出对原内容的修改，如"无"、"翻译为中文"、"适配本地路径"等
```

## 五、新增 Skill 的完整流程

### A. 原创 Skill（`source: original`）

1. 复制 `skills/skill-template/` → `skills/<your-skill-name>/`。
2. 修改 `SKILL.md`：填 `name`、`description`、`source: original`，写好正文步骤。
3. （可选）放入 `scripts/`、`templates/` 等辅助文件。
4. 自测：在一个新的 Agent 会话里用自然语言触发，确认能被正确识别和执行。
5. 更新根目录 `README.md` 的「已收录 Skills」表格。
6. 提交：

   ```bash
   git add skills/<your-skill-name> README.md
   git commit -m "feat(skills): add <your-skill-name>"
   ```

### B. 收集公开 Skill（`source: collected`）

1. **先确认许可证**：明确原 Skill 的许可证类型，许可证不明则放弃收录。
2. 复制 `skills/skill-template/` → `skills/<skill-name>/`（建议沿用原名，必要时加后缀）。
3. **原样拷贝**原 Skill 的 `SKILL.md` 正文与辅助文件到该目录。
4. 在 front matter 补充：`source: collected` + `author` + `source_url` + `license`。
5. 新增 `ATTRIBUTION.md`（按第四节模板）。
6. 按需放入原 `LICENSE` 文件（非 Apache-2.0 时必需）。
7. 更新根目录 `README.md` 的「已收录 Skills」表格。
8. 提交：

   ```bash
   git add skills/<skill-name> README.md
   git commit -m "feat(skills): collect <skill-name> from <author>"
   ```

## 六、维护已有 Skill

- 修改 `description` 时务必同步考虑触发可靠性，避免误触发或漏触发。
- 步骤有调整时，记得同步更新正文示例与「注意事项」。
- `collected` 类 Skill 如有上游更新，同步后**更新 ATTRIBUTION.md 的「抓取版本」字段**。
- 若 Skill 不再使用，建议直接删除目录而非保留过期内容。

## 七、命名与风格

- 目录名、`name` 字段：小写 + 连字符（kebab-case）。
- 文档使用中文为主，关键术语保留英文原词。
- 脚本需在文件头部注释说明用途、入参、依赖。
