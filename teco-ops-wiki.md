# teco-ops-wiki

## 一、目录结构

```
teco-ops-wiki/
├── data/                schema、别名、标签定义（与 SDAAKernelWiki 共用同一份定义）
│   ├── schemas.yaml       页面类型的字段规范
│   ├── aliases.yaml       术语别名映射
│   └── tags.yaml          标签定义
├── sources/             原始证据层
│   └── docs/
│       ├── teco-ops-docs.md         Teco-Ops 项目文档集索引页
│       ├── teco-ops-docs/           9 个分卷页（按原始文件切分）
│       ├── raw-teco-ops/            Teco-Ops doc/ 目录 9 份原文（.txt，无 frontmatter）
│       ├── <4 份官方手册索引页>.md
│       ├── <4 份官方手册>/           分卷页目录
│       └── raw/                     4 份官方手册的原始 pdftotext 全文
├── wiki/                策展/加工知识层
│   ├── hardware/          硬件与编程模型速览（1 页）
│   ├── techniques/        算子开发技术（3 页）
│   ├── patterns/          精度问题诊断模式（1 页）
│   └── kernels/           flatten_rays 范例解析（1 页）
├── queries/              按主题预先整理的导航索引（by-document.md、by-technique.md 等，5 份）
├── references/           使用引导：primer.md（主题速查表）、schema.md（本知识库的 schema 说明）
├── scripts/              查询与校验脚本（与 SDAAKernelWiki 共用同一套脚本，路径自适应）
├── README.md             知识库说明（含范围边界与安全说明）
├── SKILL.md              Claude Code skill 定义（供 AI 直接加载查询）
└── requirements.txt      Python 依赖
```

与 `SDAAKernelWiki` 相比，本知识库省去了 `artifacts/`（厂商源码快照层）、`candidates/`（审计台账）、`sources/repos/`（内部代码仓索引）三个层次，因为这些层次对应的内容本身就不在收录范围内；`wiki/` 层也只保留了 `hardware`/`techniques`/`patterns`/`kernels` 四个子目录（省去 `runtime`/`languages`/`compiler`/`migration`/`examples`），因为现有 6 个策展页面尚不需要用到后面几类。

## 二、页面类型与 Schema

页面类型定义与 `SDAAKernelWiki` 完全一致（共用同一份 `data/schemas.yaml`），但本知识库实际只用到其中一部分类型：

| 类型 | id 前缀 | 必需字段 | 本知识库中的用途 |
|---|---|---|---|
| `source-doc` | `doc-` | id, title, type, source_category, product_version, published_at, captured_at | Teco-Ops 文档集索引页 + 4 份官方手册索引页 |
| `source-doc-part` | `doc-*-pNN` | id, title, type, parent_doc, product_version, raw_text, raw_line_range | 全部正文分卷页 |
| `wiki-hardware` | `hw-` | id, title, type, architectures, tags, confidence, sources | 硬件与编程模型速览 |
| `wiki-technique` | `technique-` | id, title, type, architectures, tags, confidence, reproducibility, sources | interface+ual 分层、PyTorch 绑定、Plugin 注册 |
| `wiki-pattern` | `pattern-` | id, title, type, symptoms, candidate_techniques, sources | 精度问题三类模式 |
| `wiki-kernel` | `kernel-` | id, title, type, architectures, kernel_types, confidence, sources | flatten_rays 范例解析 |

`wiki-language`/`wiki-runtime`/`wiki-compiler`/`wiki-migration`/`wiki-example`/`source-repo`/`source-op`/`source-local` 这几种类型在本知识库中未使用（对应内容不在收录范围内），完整定义见 `external/SDAAKernelWiki/references/schema.md`。

置信度（`confidence`）与可复现程度（`reproducibility`）分级与 `SDAAKernelWiki` 完全一致，见文档 05 第 3.1、3.2 节。本知识库中**全部页面**的置信度均为 `verified`——因为内容直接来自已发布的官方手册或公开仓库材料，不含未经验证的本地实验数据，这一点与 `SDAAKernelWiki`（存在 `source-reported`/`inferred`/`experimental` 页面）不同。

## 四、内容规模与覆盖范围

（以下数据经页面校验器 `validate.py` 实际核实）

**总页面数：54 个，全部通过 schema 校验，无重复 id。**

### 4.1 Teco-Ops 项目文档集（`sources/docs/teco-ops-docs*`）

Teco-Ops 仓库 `doc/` 目录下全部 9 份文档，逐文件切分为 1 个索引页 + 9 个分卷页（共 10 页）：

| 分卷页 | 原始文件 | 主题 |
|---|---|---|
| `doc-teco-ops-docs-p01` | `doc/PR.md` | 算子提交规范（commit 格式、PR 规范、代码风格、cpplint） |
| `doc-teco-ops-docs-p02` | `doc/QA.md` | 常见问题（proto 参数配置、Executor/Parser/MetaTensor 测试框架） |
| `doc-teco-ops-docs-p03` | `doc/README_DEBUG.md` | SDAA C 程序调试手册（printf、TecoGDB、abort、assert、精度问题） |
| `doc-teco-ops-docs-p04` | `doc/README_OP.md` | 算子开发指南（interface+ual 分层架构，添加新算子完整流程） |
| `doc-teco-ops-docs-p05` | `doc/README_PLUGIN.md` | Plugin 自定义算子接口（TVM Relay IR 注册） |
| `doc-teco-ops-docs-p06` | `doc/README_PYTHON.md` | PyTorch 扩展绑定 |
| `doc-teco-ops-docs-p07` | `doc/teco-ops-hardware.md` | 算子开发硬件相关知识 |
| `doc-teco-ops-docs-p08` | `doc/op_docs/doc_template.md` | 算子设计文档模板 |
| `doc-teco-ops-docs-p09` | `doc/op_docs/flatten_rays.md` | flatten_rays 算子设计文档范例 |

原始全文（未做任何切分/加工）保存于 `sources/docs/raw-teco-ops/`，共 9 份 `.txt`，采集自 commit `d90ddf51f09374ea082f8b4f9dbf96190384b1f6`（2026-06-29）。

### 4.2 官方手册（`sources/docs/<slug>*`）

4 份官方手册，与 `SDAAKernelWiki` 中的对应页面**逐字节一致**（同一份原始拷贝）：

| 文档 | 分卷数 | 索引 page id |
|---|---|---|
| SDAA C 编程指南 v3.1.0 | 27 | `doc-sdaa-c-programming-guide-v3-1-0` |
| SDAA C 零基础入门 v1.1.0 | 2 | `doc-sdaa-c-getting-started-v1-1-0` |
| 性能优化手册 SDAA C 篇 v2.0.2 | 3 | `doc-perf-optimization-sdaa-c-v2-0-2` |
| 性能优化手册 算子篇 v1.1.0 | 2 | `doc-perf-optimization-operator-v1-1-0` |

原始全文保存于 `sources/docs/raw/`，共 4 份 `.txt`（pdftotext 抽取全文）。索引页 + 分卷页合计 38 页。

### 4.3 策展 wiki 页面（`wiki/`）

6 个人工整理的桥接页面，把 Teco-Ops 文档与官方手册内容串联起来：

| 主题 | Page ID | 说明 |
|---|---|---|
| 硬件与编程模型速览 | `hw-teco-ops-hardware-model` | SPA/SPE/SU/SREG/VPU/VREG/FU/SPM 速查表 + SPMD 切分公式 |
| interface+ual 分层算子开发 | `technique-teco-ops-interface-ual-layering` | 新增算子的完整九步流程，`RUN_OP`/`find()`/`.scpp` kernel 调用链路 |
| PyTorch 扩展绑定 | `technique-teco-ops-python-torch-binding` | `torch_ext.cpp` 包装 + `PYBIND11_MODULE` 注册 |
| Plugin/TVM Relay IR 注册 | `technique-teco-ops-plugin-relay-registration` | `AbstractPluginOp` 子类 + ONNX/Relay 转换，接入 Teco-Inference 推理管线 |
| 精度问题三类模式 | `pattern-teco-ops-precision-pitfalls` | half 截断、整型溢出、超越函数下溢，各附错误/正确写法对照 |
| flatten_rays 范例解析 | `kernel-teco-ops-flatten-rays` | 完整 tiling 策略 + 三种暴露方式（interface/PyTorch/Plugin）的对照分析 |

## 五、查询工具

`teco-ops-wiki/scripts/` 下的脚本与 `SDAAKernelWiki` 共用同一套代码（`_wiki_root.py` 按脚本所在目录自动定位仓库根，无需修改即可在不同知识库根目录下工作），用法完全一致。

### 5.1 `query.py`：自由文本 / 条件检索

```
usage: query.py [-h] [--type TYPE] [--tag TAG] [--architecture ARCHITECTURE]
                [--symptom SYMPTOM] [--confidence CONFIDENCE] [--limit LIMIT]
                [--compact] [--paths-only]
                [query ...]
```

参数含义与文档 05 第 5.1 节一致。示例（真实查询结果，在 `teco-ops-wiki` 根目录执行）：

```bash
$ python3 scripts/query.py "flatten_rays tiling SPMD" --compact
# 10 result(s)

  [wiki-kernel] kernel-teco-ops-flatten-rays: flatten_rays：Teco-Ops 算子设计文档范例解析
  [wiki-hardware] hw-teco-ops-hardware-model: Teco-Ops 硬件与编程模型速览（SPA/SPE/SPMD）
  [wiki-source-doc-part] doc-teco-ops-docs-p09: Teco-Ops 项目文档集 — 第p09部分 (op_docs/flatten_rays.md)
  [wiki-source-doc-part] doc-teco-ops-docs-p07: Teco-Ops 项目文档集 — 第p07部分 (teco-ops-hardware.md)
  [wiki-source-doc] doc-teco-ops-docs: Teco-Ops 项目文档集
  ...（另有 5 条命中官方手册正文分卷页）
```

结果同时命中策展的 `wiki-*` 页与文档原文的 `source-doc(-part)` 页，按相关性排序。与文档 05 的建议一致：不应过度使用 `--type` 限定，省略 `--type` 能同时拿到技术结论与文档原文。

按类型列出全部索引页：

```bash
$ python3 scripts/query.py --type source-doc --compact
# 5 result(s)

  [wiki-source-doc] doc-perf-optimization-operator-v1-1-0: 性能优化手册 算子篇 v1.1.0
  [wiki-source-doc] doc-perf-optimization-sdaa-c-v2-0-2: 性能优化手册 SDAA C 篇 v2.0.2
  [wiki-source-doc] doc-sdaa-c-getting-started-v1-1-0: SDAA C 零基础入门 v1.1.0
  [wiki-source-doc] doc-sdaa-c-programming-guide-v3-1-0: SDAA C 编程指南 v3.1.0
  [wiki-source-doc] doc-teco-ops-docs: Teco-Ops 项目文档集
```

### 5.2 `get_page.py`：按 id 精确获取

```
usage: get_page.py [-h] [--body-only] [--frontmatter-only] [--follow-sources] selector
```

参数含义与文档 05 第 5.2 节一致。示例：

```bash
python3 scripts/get_page.py doc-teco-ops-docs                   # 索引页：9 份文档的分卷表 + 目录
python3 scripts/get_page.py doc-teco-ops-docs-p04                # 算子开发指南分卷正文
python3 scripts/get_page.py kernel-teco-ops-flatten-rays --follow-sources   # 展开其引用的全部来源页
```

`--follow-sources` 是"从 wiki 结论跳回文档原文核实"的标准操作路径，例如从 `kernel-teco-ops-flatten-rays` 展开到 `doc-teco-ops-docs-p07`/`p08`/`p09` 的完整原文。

## 六、维护与校验工具

| 脚本 | 用法 | 作用 | 本知识库实测输出 |
|---|---|---|---|
| `validate.py` | `python3 scripts/validate.py` | 校验全部页面的 schema 合法性、id 唯一性、`sources`/`parent_doc` 引用完整性 | `OK: 54 pages, 54 ids` |
| `check_doc_coverage.py` | `--worklist WORKLIST --details --threshold THRESHOLD` | 检查某份文档的原文标识符在结构化页面中的覆盖率 | 需要 `SDAAKernelWiki` PDF 抽取流程生成的 worklist 文件，本知识库暂未生成对应 worklist，脚本本身随基础设施一并复制但当前未使用 |

本知识库没有复制 `SDAAKernelWiki` 中面向内部代码仓维护的脚本（`import_repo.py`、`list_ops.py`、`snapshot_repo_files.py`、`check_provenance.py`、`convert_office_docs.py`），因为这些脚本对应的 `sources/repos/`、`artifacts/`、`.docx/.xlsx` 转换流程在本知识库范围内均不存在。

## 七、常用页面速查

改编自知识库自带的 `references/primer.md`。

### 我想... 先查

| 目标 | 先查页面 |
|---|---|
| 给 Teco-Ops 添加一个新算子 | `technique-teco-ops-interface-ual-layering` → `doc-teco-ops-docs-p04` |
| 写算子设计文档 | `kernel-teco-ops-flatten-rays`（完整范例）+ `doc-teco-ops-docs-p08`（空白模板） |
| 让算子能被 PyTorch 直接调用 | `technique-teco-ops-python-torch-binding` |
| 让算子能在推理引擎里跑 | `technique-teco-ops-plugin-relay-registration` |
| 排查结果偏差但不崩溃的 bug | `pattern-teco-ops-precision-pitfalls` |
| 补充测试用例的 proto 参数 | `doc-teco-ops-docs-p02` |
| 提交 PR 前自查 | `doc-teco-ops-docs-p01` |
| 理解 SPA/SPE/SPMD 基础概念 | `hw-teco-ops-hardware-model` |

### 硬件页面

| 主题 | Page ID |
|---|---|
| SPA/SPE 拓扑、SU/SREG/VPU/VREG/FU/SPM、SPMD 编程模型 | `hw-teco-ops-hardware-model` |

若需要更完整的 SDAA 硬件页面（DMA 引擎模型、RMA mesh、ACE 矩阵单元、HBM channel-bank-row、pipe0/pipe1），需改查 `external/SDAAKernelWiki`（本知识库范围外，详见文档 05）。

## 八、使用规范

- 本知识库的边界是硬性的：任何时候不应从本知识库的页面中引用或推断出 `tecoal`/`sdcops`/`tecocustom`/`tecolmk` 内部代码仓的内容，也不应引用本知识库未收录的其余官方手册内容——如需这些内容，应明确改用 `external/SDAAKernelWiki`，而不是试图从 `teco-ops-wiki` 拼凑。
- 涉及具体 API 参数取值、边界条件、代码示例时，须使用 `--follow-sources` 跳转至 `doc-teco-ops-docs-p*` 或官方手册的分卷页核实原文，而非仅采信 `wiki/` 层的精炼结论。
- 新增页面时须遵守 `references/schema.md` 中定义的范围契约（来源仅限 Teco-Ops `doc/` 目录与 4 份已授权手册、不引用内部仓库、不收录图片资源、`sources` 字段引用必须能在本知识库内部解析），新增后运行 `python3 scripts/validate.py` 确认无 schema 错误。

