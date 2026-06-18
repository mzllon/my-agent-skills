---
name: skill-template
description: |
  这是一个 Skill 模板。复制本目录并修改本节内容来创建你自己的 Skill。
  description 字段是 Agent 决定是否触发该 Skill 的关键依据，请清晰描述：
  1) 这个 Skill 能做什么；
  2) 在什么场景下应该被使用；
  3) 何时不应该使用。
source: original
---

# <Skill 名称>

> 一句话说明该 Skill 的用途。

## 适用场景

- 列出典型使用场景。
- 说明前置条件（如依赖、运行环境）。

## 使用步骤

1. 第一步……
2. 第二步……
3. 第三步……

## 输入 / 输出

- **输入**：……
- **输出**：……

## 注意事项

- 列出边界情况、常见错误与处理方式。

## 参考资料

- [链接](https://example.com)

---

## 如何使用本模板

### A. 原创 Skill

1. 复制 `skill-template/` → `skills/<your-skill-name>/`。
2. 改写上方 front matter 与正文。
3. front matter 保持 `source: original` 即可（无需 author/source_url/license）。

### B. 收集公开 Skill

1. 复制 `skill-template/` → `skills/<skill-name>/`。
2. front matter 改为：

   ```yaml
   ---
   name: <skill-name>
   description: <原描述，可保留原文>
   source: collected
   author: <原作者>
   source_url: <原始链接>
   license: <原许可证，如 MIT>
   ---
   ```

3. 用原 Skill 的内容替换正文。
4. 复制本目录下 `ATTRIBUTION.md` 模板，填写后放入新 Skill 目录。
5. 若原许可证 ≠ Apache-2.0，把原 `LICENSE` 全文一并放入新 Skill 目录。

详细规范见根目录 [CONTRIBUTING.md](../../CONTRIBUTING.md)。
