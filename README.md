# docx-editor-cn 优化版 · 编号可维护，格式有依据

面向需要反复修改的中文 Word 论文与报告，重点完善标题层级、章节题注和参考格式保留流程，为增删章节、调整图表和沿用模板提供明确的处理规则与检查步骤。

## 原版来源

基于 **[Gostyan 的 docx-skill-4-cn-paper](https://github.com/Gostyan/docx-skill-4-cn-paper)**，沿用其 Word 排版与转换基础能力，由 **belvme** 优化维护，保留原作者署名及 [MIT 许可证](LICENSE.txt)。

## 本版本重点调整

| 处理场景 | 本版本的调整 |
| --- | --- |
| 增删章节后维护编号 | 模板与转换脚本使用 Word 原生标题编号，并按章节组织下级计数；转换时移除识别到的手写编号前缀。 |
| 按已有文档继续编辑 | 技能说明明确以用户要求和参考文档为准，检查字体、字号、编号字形、缩进及段落间距。 |
| 图表题注跟随章节 | 补充原生 Caption、SEQ 字段、章号关联与分章重置的处理要求，并要求更新字段后核对结果。 |
| 选择标题编号方案 | 区分“一、→（一）→1、”和“1→1.1→1.1.1”两类规则，根据参考文档选择。 |
| 交付前检查 | 同时核对标题层级、编号关系和渲染外观。 |

其中，格式保留和题注检查包含对 AI Agent 的工作流程要求；具体文档仍需按参考样式调整并验证。配套脚本是起点，不代表所有模板都已自动适配。

## 使用方法

将本仓库下载到所用 AI 工具的技能目录，将文件夹命名为 `docx-editor-cn`，确保目录下直接包含 `SKILL.md` 和 `scripts/`。

可以这样向 Agent 提出任务：

> 使用 docx-editor-cn，把这份 Markdown 转成 Word。以我提供的 Word 为格式参考，保留各级标题的字体和间距，使用原生多级编号；图表题注按章节编号，完成后检查编号与排版。

或处理现有文档：

> 使用 docx-editor-cn，为这份 Word 整理 Heading 1/2/3 和图表题注。先识别实际章节层级，再设置编号，保持原有外观。

详细规则见 [SKILL.md](SKILL.md)。

## 脚本与依赖

在技能目录安装 JavaScript 依赖：

```bash
npm ci
```

新建文档可复制并调整 `scripts/new_doc.js` 的内容区、样式及输出路径，再运行：

```bash
node scripts/new_doc.js
```

| 文件或目录 | 用途 |
| --- | --- |
| `scripts/new_doc.js` | 新文档模板及排版辅助函数 |
| `scripts/convert_paper.js` | Markdown 论文转换脚本，使用前检查输入输出配置 |
| `scripts/mathml-to-docx.js` | 将 MathML 转为 Word 公式组件 |
| `scripts/table.py`、`scripts/formula.py` | 向文档 XML 插入表格和公式 |
| `scripts/comment.py`、`scripts/accept_changes.py` | 批注与修订处理 |
| `scripts/office/` | 解包、打包、校验及 LibreOffice 调用工具 |

编辑和检查现有文档时，按所用流程准备 Python 及相关依赖；格式转换或渲染可能需要 LibreOffice、Pandoc、Poppler。各命令的用途与前置条件见 `SKILL.md`。

## 许可证与署名

沿用原项目 MIT 许可证，原版权归属为 `Copyright (c) 2025-2026 Gostyan`。分发时请保留 [LICENSE.txt](LICENSE.txt) 及原作者声明。
