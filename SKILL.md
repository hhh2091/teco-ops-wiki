---
name: teco-ops-wiki
description: 用于查询 Teco-Ops（Tecorigin 开源 SDAA 算子仓库）的算子提交规范、interface+ual 分层开发流程、PyTorch/Plugin 绑定方式、调试手段与硬件编程模型。范围严格限定于 teco-ops 仓库 doc/ 目录与 4 份太初官方手册，不含内部代码仓或其余官方手册内容。
argument-hint: "[natural-language-question] | [--tag proto --type technique] | [page-id]"
allowed-tools: "Bash Read Grep Glob"
---

# teco-ops-wiki

这是面向 Teco-Ops 开源算子仓库开发者文档的知识 skill，与更完整的 SDAAKernelWiki 相互独立、范围更窄。当问题涉及 Teco-Ops 仓库本身的算子开发规范、interface+ual 架构、PyTorch/Plugin 绑定或调试方法时，优先使用这里的知识；涉及更广泛的 SDAA 硬件优化技术、内部代码仓算子索引时，改用 `external/SDAAKernelWiki`。

## 查询流程

在本 skill 根目录下运行：

```bash
python3 scripts/query.py "算子提交规范 commit PR 格式" --compact
python3 scripts/query.py "interface ual RUN_OP 分支派发" --compact
python3 scripts/query.py "PyTorch 绑定 torch_ext" --compact
python3 scripts/query.py "Plugin TVM Relay 自定义算子" --compact
python3 scripts/query.py "half 精度 溢出 下溢" --compact
python3 scripts/query.py --tag spmd --compact
python3 scripts/get_page.py doc-teco-ops-docs --follow-sources
python3 scripts/get_page.py kernel-teco-ops-flatten-rays --follow-sources
```

问题较宽泛时先读 `references/primer.md`。新增页面或判断证据质量时读 `references/schema.md`。

## Teco-Ops 项目文档集（完整结构化）

`doc/` 目录下 9 份文档已整理为完整、无损、可逐文件追溯的结构化页面：索引页 `sources/docs/teco-ops-docs.md`（`doc-teco-ops-docs`），正文按原始文件切分在 `sources/docs/teco-ops-docs/p*.md`（`doc-teco-ops-docs-p*`，`source-doc-part`），原文全文存于 `sources/docs/raw-teco-ops/*.txt`。

| 主题 | 索引 page id |
|------|-------------|
| 算子提交规范（PR.md） | `doc-teco-ops-docs-p01` |
| 常见问题（QA.md） | `doc-teco-ops-docs-p02` |
| SDAA C 程序调试手册（README_DEBUG.md） | `doc-teco-ops-docs-p03` |
| 算子开发指南（README_OP.md） | `doc-teco-ops-docs-p04` |
| Plugin 自定义算子接口（README_PLUGIN.md） | `doc-teco-ops-docs-p05` |
| PyTorch 扩展绑定（README_PYTHON.md） | `doc-teco-ops-docs-p06` |
| 算子开发硬件相关知识（teco-ops-hardware.md） | `doc-teco-ops-docs-p07` |
| 算子设计文档模板（op_docs/doc_template.md） | `doc-teco-ops-docs-p08` |
| flatten_rays 设计文档范例（op_docs/flatten_rays.md） | `doc-teco-ops-docs-p09` |

## 4 份官方手册（与 SDAAKernelWiki 内容一致）

| 文档 | 索引 page id |
|------|-------------|
| SDAA C 编程指南 v3.1.0 | `doc-sdaa-c-programming-guide-v3-1-0` |
| 性能优化手册 SDAA C 篇 v2.0.2 | `doc-perf-optimization-sdaa-c-v2-0-2` |
| 性能优化手册 算子篇 v1.1.0 | `doc-perf-optimization-operator-v1-1-0` |
| SDAA C 零基础入门 v1.1.0 | `doc-sdaa-c-getting-started-v1-1-0` |

## 策展 wiki 页面

| 主题 | Page ID |
|---|---|
| 硬件与编程模型速览（SPA/SPE/SPMD） | `hw-teco-ops-hardware-model` |
| interface+ual 分层算子开发 | `technique-teco-ops-interface-ual-layering` |
| PyTorch 扩展绑定 | `technique-teco-ops-python-torch-binding` |
| Plugin/TVM Relay IR 注册 | `technique-teco-ops-plugin-relay-registration` |
| 精度问题三类模式 | `pattern-teco-ops-precision-pitfalls` |
| flatten_rays 范例解析 | `kernel-teco-ops-flatten-rays` |

## 证据规则

1. 回答时引用 page id 和路径。
2. 沿 `sources:` 追溯到 `sources/docs/raw-teco-ops/` 或 `sources/docs/raw/` 下的原始文本。
3. 官方手册与 Teco-Ops 仓库 `doc/` 目录内容均可按 `verified` 使用（均为已发布的官方/公开仓库材料）。
4. 若问题涉及本知识库范围外的内容（内部代码仓、其余官方手册、`teco/`/`cuda/`/`api/`/`test/` 源码），应明确告知超出范围，改查 `external/SDAAKernelWiki` 或直接阅读源码。

## KernelPilot 集成

Teco-Ops 相关任务在 KernelPilot 中应遵循：

1. 恢复 `K`、`R`、`W`。
2. 若任务是"给 Teco-Ops 仓库新增/移植算子"，先查本 skill 的 interface+ual 分层流程（`technique-teco-ops-interface-ual-layering`），再套用 SDAAKernelWiki 的硬件优化启发式。
3. 用页面证据选择一个可测量的下一步编辑。
4. 在 attempt ledger 中记录影响本轮决策的 page id。
