---
name: patent-disclosure
description: "中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文。"
user-invocable: false
---

# 交底书编写

分步指令在 **`prompts/`**（本包内）。发明 / 实用新型 / 外观是**包内三个目录**，不是三个可触发技能。

## 产出形态与红线

- **产出形态确认（开工先做）**：先用 ask 类交互向用户确认本次产出形态——(a) 交底稿（给内部评审，**默认**）；(b) 跳过评审、直接出给代理人的申请文件（转 `skills/patent-application` 的门禁规则）。用户未明确时按交底稿处理，并在开工提示中说明「本次按交底稿（默认）产出」。
- **交底稿红线（禁止写入）**：权利要求项（权项）、FTO（自由实施）分析、上位化/概括策略分析。这些是代理人阶段的工作，交底稿写了反而污染评审。
- **交底稿必备要素**：
  1. **方案内容**：核心技术方案写完整，不含糊；
  2. **创新点**：逐条列出，能回指方案内容；
  3. **差异点**：与现有方案、与专利族关联方案的差异写清楚；
  4. **数据与图示备注**：实验数据标口径（样本/构建号/日期/环境）；图示编号与图题一致、图内文字不超框、风格统一、图像清晰。

| 步骤 | 文件 |
|------|------|
| Step 1 | `prompts/intake.md` |
| Step 2 | `prompts/project_scan.md` |
| Step 3–4 | `prompts/invention/` · `utility_model/` · `design/` 挖点 |
| 填表 / 线稿 | `prompts/fill_*`、`image_gen.md`、`*_lineart_*.md`；外观视图口径 `references/design_view_cnipa.md` |
| Step 5 | `prompts/prior_art_search.md`（轻量查新，一词一页） |
| Step 6 | `prompts/disclosure_preview.md` |
| Step 7 | 对应类型 `disclosure_builder.md` + `template_reference.md` |
| Step 8 | `prompts/disclosure_self_check.md`；终审/批注落实前再过 `references/review_checklist.md`（代理人视角八查） |
| 迭代 | `iteration_context.md` / `merger.md` / `correction_handler.md` |

查新工具：`tools/crawl/cnipa_epub_search.py`。整仓安装时路径为 `skills/patent-disclosure/tools/crawl/cnipa_epub_search.py`。著录检索不在本包，**禁止**当查新引擎调用。  
交底交付后**不要**自动进入申请文件；用户点名并给出本目录后，再走 `skills/patent-application/SKILL.md`。  
`--type` 与 intake 一致；两段式：关键词 → `EPUB_CLASS_HINT` / IPC·LOC → `--class`；不足 4 条则同分类号回补第一轮。

线稿、CAD、公式、Word 出图用本包 `tools/`（`browser.py`、`mermaid_render.py`、`md_to_docx.py` 等）。
