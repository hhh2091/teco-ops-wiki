---
name: teco-ops-wiki
description: 用于查询 Teco-Ops、Teco-AL（Tecorigin 开源 SDAA 算子仓库）的算子提交规范、interface+ual 分层开发流程、PyTorch/Plugin 绑定方式、调试手段、硬件编程模型、Teco-AL 公开的 GEMM/卷积/AddTensor 完整性能优化案例，以及 PICT_smoke 模型级 CUDA→SDAA 自动迁移模式。范围严格限定于三仓库的文档目录（Teco-Ops/PICT_smoke 为 doc/ 或根 README，Teco-AL 为 doc/+ 根 README.md）、4 份太初官方手册与 TecoLIBRT 用户手册，不含内部代码仓或其余官方手册内容。
argument-hint: "[natural-language-question] | [--tag proto --type technique] | [page-id]"
allowed-tools: "Bash Read Grep Glob"
---

# teco-ops-wiki

这是面向 Teco-Ops、Teco-AL、PICT_smoke 三个 Tecorigin 公开仓库文档的知识 skill，与更完整的 SDAAKernelWiki 相互独立、范围更窄。当问题涉及这些仓库本身的算子开发规范、interface+ual 架构、PyTorch/Plugin 绑定、调试方法、Teco-AL 公开的 GEMM/卷积/AddTensor 分支性能优化案例，或模型级 CUDA→SDAA 迁移模式时，优先使用这里的知识；涉及更广泛的 SDAA 硬件优化技术、内部代码仓（`tecoal`/`sdcops`/`tecocustom`/`tecolmk` gerrit 仓库，与本知识库收录的公开 Gitee 仓库 `teco-al` 是两个不同项目）算子索引时，改用 `external/SDAAKernelWiki`。

## 查询流程

在本 skill 根目录下运行：

```bash
python3 scripts/query.py "算子提交规范 commit PR 格式" --compact
python3 scripts/query.py "interface ual RUN_OP 分支派发" --compact
python3 scripts/query.py "PyTorch 绑定 torch_ext" --compact
python3 scripts/query.py "Plugin TVM Relay 自定义算子" --compact
python3 scripts/query.py "half 精度 溢出 下溢" --compact
python3 scripts/query.py "gemm 分块 广播 双缓冲" --compact
python3 scripts/query.py "conv2gemm 卷积转矩阵乘" --compact
python3 scripts/query.py "TORCH_SDAA_AUTOLOAD cuda_migrate" --compact
python3 scripts/query.py --tag spmd --compact
python3 scripts/get_page.py doc-teco-ops-docs --follow-sources
python3 scripts/get_page.py doc-teco-al-docs --follow-sources
python3 scripts/get_page.py doc-pict-smoke-docs --follow-sources
python3 scripts/get_page.py kernel-teco-ops-flatten-rays --follow-sources
python3 scripts/get_page.py kernel-teco-al-gemm --follow-sources
python3 scripts/get_page.py technique-pict-smoke-cuda-sdaa-model-migration
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

## Teco-AL 项目文档集（完整结构化）

`doc/` 目录与根 `README.md` 已整理为 19 份分卷页：索引页 `sources/docs/teco-al-docs.md`（`doc-teco-al-docs`），正文在 `sources/docs/teco-al-docs/p*.md`（`doc-teco-al-docs-p*`），原文全文存于 `sources/docs/raw-teco-al/*.txt`。

| 主题 | 索引 page id |
|------|-------------|
| 仓库总览、目录结构、贡献指南（README.md） | `doc-teco-al-docs-p01` |
| 开发指南：核心概念（句柄/张量/描述符/工作空间） | `doc-teco-al-docs-p02` |
| 编程规范 | `doc-teco-al-docs-p03` |
| 算子设计文档模板 | `doc-teco-al-docs-p04` |
| **AddTensor**（完整讲解范例，含真实性能数据） | `doc-teco-al-docs-p05` |
| **Hgemm**（完整讲解范例，含真实性能数据） | `doc-teco-al-docs-p06` |
| **ConvolutionForward**（完整讲解范例，含真实性能数据） | `doc-teco-al-docs-p07` |
| ActivationForward / ActivationBackward | `doc-teco-al-docs-p08` / `p09` |
| Argmax / IndexPut / LogicalNotTensor | `doc-teco-al-docs-p10` / `p11` / `p12` |
| MaskedFill / MaskedSelect / ScaleTensor | `doc-teco-al-docs-p13` / `p14` / `p15` |
| ScatterNdAdd / ScatterOut / UnaryOps / Unique | `doc-teco-al-docs-p16` / `p17` / `p18` / `p19` |

## PICT_smoke 项目文档集

| 主题 | 索引 page id |
|------|-------------|
| SDAA 迁移与训练指南（README.md，中文） | `doc-pict-smoke-docs-p01` |
| 原始学术项目说明（readme_en.md，英文，SIGGRAPH 2024） | `doc-pict-smoke-docs-p02` |

## 官方手册（与 SDAAKernelWiki 内容一致）

| 文档 | 索引 page id |
|------|-------------|
| SDAA C 编程指南 v3.1.0 | `doc-sdaa-c-programming-guide-v3-1-0` |
| 性能优化手册 SDAA C 篇 v2.0.2 | `doc-perf-optimization-sdaa-c-v2-0-2` |
| 性能优化手册 算子篇 v1.1.0 | `doc-perf-optimization-operator-v1-1-0` |
| SDAA C 零基础入门 v1.1.0 | `doc-sdaa-c-getting-started-v1-1-0` |
| TecoLIBRT 用户手册 v1.2.0 | `doc-tecolibrt-user-manual-v1-2-0` |

## 策展 wiki 页面

| 主题 | Page ID |
|---|---|
| 硬件与编程模型速览（SPA/SPE/SPMD） | `hw-teco-ops-hardware-model` |
| interface+ual 分层算子开发 | `technique-teco-ops-interface-ual-layering` |
| PyTorch 扩展绑定 | `technique-teco-ops-python-torch-binding` |
| Plugin/TVM Relay IR 注册 | `technique-teco-ops-plugin-relay-registration` |
| 精度问题三类模式 | `pattern-teco-ops-precision-pitfalls` |
| flatten_rays 范例解析 | `kernel-teco-ops-flatten-rays` |
| Teco-AL 分支递进式性能优化方法论 | `technique-teco-al-algo-branch-benchmarking` |
| Hgemm 分块+广播+重排+双缓冲解析 | `kernel-teco-al-gemm` |
| ConvolutionForward conv2gemm 解析 | `kernel-teco-al-conv-forward` |
| AddTensor 分块+双缓冲入门案例 | `kernel-teco-al-add-tensor` |
| PICT_smoke 模型级 CUDA→SDAA 自动迁移模式 | `technique-pict-smoke-cuda-sdaa-model-migration` |

## 证据规则

1. 回答时引用 page id 和路径。
2. 沿 `sources:` 追溯到 `sources/docs/raw-teco-ops/`、`sources/docs/raw-teco-al/` 或 `sources/docs/raw/` 下的原始文本。
3. 官方手册与两仓库 `doc/` 目录内容均可按 `verified` 使用（均为已发布的官方/公开仓库材料）。
4. 若问题涉及本知识库范围外的内容（内部代码仓、其余官方手册、`teco/`/`cuda/`/`api/`/`test/`/`ual/`/`interface/` 等源码），应明确告知超出范围，改查 `external/SDAAKernelWiki` 或直接阅读上游仓库源码。

## KernelPilot 集成

Teco-Ops/Teco-AL 相关任务在 KernelPilot 中应遵循：

1. 恢复 `K`、`R`、`W`。
2. 若任务是"给 Teco-Ops/Teco-AL 仓库新增/移植算子"，先查本 skill 的 interface+ual 分层流程（`technique-teco-ops-interface-ual-layering`）；若任务是 GEMM/卷积/elementwise 性能优化，先查 `technique-teco-al-algo-branch-benchmarking` 与对应的 `kernel-teco-al-*` 案例页，再套用 SDAAKernelWiki 的硬件优化启发式。
3. 用页面证据选择一个可测量的下一步编辑。
4. 在 attempt ledger 中记录影响本轮决策的 page id。
