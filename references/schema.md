# teco-ops-wiki Schema

## 页面类型

| 类型 | ID 前缀 | 用途 |
|---|---|---|
| `source-doc` | `doc-*` | 官方/外部文档的来源**索引页**：元信息、章节目录、分卷链接、`raw_text` 原文链接。 |
| `source-doc-part` | `doc-*-pNN` | 官方文档的**完整结构化分卷页**：正文按文件/章节切分，无损保留原文内容，经 `raw_text` 逐行可追溯。 |
| `wiki-hardware` | `hw-*` | 硬件与编程模型速览页面。 |
| `wiki-technique` | `technique-*` | 算子开发技术与流程（interface+ual、绑定、注册）。 |
| `wiki-pattern` | `pattern-*` | 症状 -> 诊断 -> 处理办法。 |
| `wiki-kernel` | `kernel-*` | 带证据的算子案例研究/范例解析。 |

本知识库范围内不使用 `wiki-language`/`wiki-runtime`/`wiki-compiler`/`wiki-migration`/`wiki-example`/`source-repo`/`source-op`/`source-local` 类型（这些类型用于 SDAAKernelWiki 更完整的内容范围，见 `external/SDAAKernelWiki/references/schema.md`）。完整 schema 定义见 `data/schemas.yaml`（与 SDAAKernelWiki 共用同一份 schema 文件，未做裁剪，仅在本知识库中未使用到全部类型）。

## 置信度

- `verified`：官方文档 + 实现或 profiler 证据共同支持。
- `source-reported`：由本地笔记、经验表或分析报告支持。
- `inferred`：从多个来源综合得出，但没有直接验证。
- `experimental`：合理但仍需复测、官方确认或更多 shape 覆盖。

本知识库中的全部页面（Teco-Ops 文档、官方手册、策展 wiki 页面）均标注为 `verified`，因为内容直接来自已发布的官方文档或公开仓库材料，未包含未经验证的本地实验数据。

## 范围契约

一个页面若要新增到本知识库，必须满足：

1. 内容来源仅限于 `https://github.com/Tecorigin/teco-ops` 的 `doc/` 目录，或已获授权收录的 4 份官方手册（SDAA C 编程指南、性能优化手册-算子篇、性能优化手册-SDAA C 篇、SDAA C 零基础入门手册）。
2. 不引用内部代码仓（`tecoal`/`sdcops`/`tecocustom`/`tecolmk`）或其余官方手册的内容。
3. 不收录图片资源，仅保留文字/公式/代码说明。
4. `sources:` 字段中的 id 必须能在本知识库内部解析（不指向 SDAAKernelWiki 独有的页面）。
