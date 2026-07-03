# 按文档索引

## Teco-Ops 项目文档集（按原始文件切分）

索引页 `doc-teco-ops-docs` → 分卷页 `doc-teco-ops-docs-p*`（`source-doc-part`，完整正文）→ `sources/docs/raw-teco-ops/*.txt`（原文）。

| 原始文件 | 分卷页 | 原文 |
|---|---|---|
| `doc/PR.md` | `doc-teco-ops-docs-p01` | `sources/docs/raw-teco-ops/PR.txt` |
| `doc/QA.md` | `doc-teco-ops-docs-p02` | `sources/docs/raw-teco-ops/QA.txt` |
| `doc/README_DEBUG.md` | `doc-teco-ops-docs-p03` | `sources/docs/raw-teco-ops/README_DEBUG.txt` |
| `doc/README_OP.md` | `doc-teco-ops-docs-p04` | `sources/docs/raw-teco-ops/README_OP.txt` |
| `doc/README_PLUGIN.md` | `doc-teco-ops-docs-p05` | `sources/docs/raw-teco-ops/README_PLUGIN.txt` |
| `doc/README_PYTHON.md` | `doc-teco-ops-docs-p06` | `sources/docs/raw-teco-ops/README_PYTHON.txt` |
| `doc/teco-ops-hardware.md` | `doc-teco-ops-docs-p07` | `sources/docs/raw-teco-ops/teco-ops-hardware.txt` |
| `doc/op_docs/doc_template.md` | `doc-teco-ops-docs-p08` | `sources/docs/raw-teco-ops/op_docs/doc_template.txt` |
| `doc/op_docs/flatten_rays.md` | `doc-teco-ops-docs-p09` | `sources/docs/raw-teco-ops/op_docs/flatten_rays.txt` |

## 官方手册（4 份，完整结构化）

| 文档 | 索引页 | 分卷数 | 原文 |
|---|---|---|---|
| 性能优化手册 算子篇 v1.1.0 | `doc-perf-optimization-operator-v1-1-0` | 2 | `sources/docs/raw/性能优化手册-算子篇_v1.1.0.txt` |
| 性能优化手册 SDAA C 篇 v2.0.2 | `doc-perf-optimization-sdaa-c-v2-0-2` | 3 | `sources/docs/raw/性能优化手册-SDAA C篇_v2.0.2.txt` |
| SDAA C 零基础入门 v1.1.0 | `doc-sdaa-c-getting-started-v1-1-0` | 2 | `sources/docs/raw/SDAA C零基础入门_v1.1.0.txt` |
| SDAA C 编程指南 v3.1.0 | `doc-sdaa-c-programming-guide-v3-1-0` | 27 | `sources/docs/raw/SDAA C编程指南_v3.1.0.txt` |

## 直接检索示例

```bash
python3 scripts/query.py --type source-doc --compact
python3 scripts/query.py --tag proto --type source-doc-part --compact
python3 scripts/query.py "interface ual RUN_OP" --compact   # 正文全文检索
python3 scripts/get_page.py doc-teco-ops-docs               # 索引→分卷
python3 scripts/validate.py                                 # schema 完整性自检
```
