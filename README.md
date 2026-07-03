# teco-ops-wiki

teco-ops-wiki 是面向 Tecorigin **Teco-Ops** 开源算子仓库（`https://github.com/Tecorigin/teco-ops`）的本地结构化知识库。它复用了 SDAAKernelWiki 的组织方式（`data/`/`sources/`/`wiki/`/`queries/`/`references/` 分层、页面 schema、`query.py`/`get_page.py` 查询工具），但内容范围被刻意收窄，仅覆盖以下**公开、非敏感**来源：

- Teco-Ops 仓库 `doc/` 目录下的全部开发者文档（不含 `teco/`、`cuda/`、`api/`、`test/` 等算子源码目录）。
- SDAAKernelWiki 中已有的 4 份太初官方手册：《SDAA C 编程指南 v3.1.0》《性能优化手册-算子篇 v1.1.0》《性能优化手册-SDAA C 篇 v2.0.2》《SDAA C 零基础入门手册 v1.1.0》。

**不包含**：SDAAKernelWiki 中其余全部官方手册、内部代码仓（`tecoal`/`sdcops`/`tecocustom`/`tecolmk`）的算子索引与代码快照、任何 `wiki/` curated 页面、以及 Teco-Ops 仓库中 `doc/` 之外的任何目录。这是有意的范围收窄，用于避免内部/敏感材料随知识库扩散。

## 内容范围

- Teco-Ops 项目文档集（`doc-teco-ops-docs`，索引页 + 9 个分卷页）：算子提交规范（PR.md）、常见问题（QA.md）、SDAA C 程序调试手册（README_DEBUG.md）、算子开发指南（README_OP.md）、Plugin 自定义算子接口（README_PLUGIN.md）、PyTorch 扩展绑定（README_PYTHON.md）、算子开发硬件相关知识（teco-ops-hardware.md）、算子设计文档模板与 flatten_rays 范例（op_docs/）。
- 4 份太初官方手册的完整结构化来源页（索引页 + 分卷页 + 原文 `raw/*.txt`），与 SDAAKernelWiki 中的对应页面逐字节一致。
- 6 个策展 `wiki/` 页面，桥接 Teco-Ops 文档与官方手册内容：硬件模型速览、interface+ual 分层开发、PyTorch 绑定、Plugin/Relay 注册、精度问题三类模式、flatten_rays 范例解析。

## 快速命令

```bash
python3 scripts/query.py "flatten_rays tiling SPMD" --compact
python3 scripts/query.py "interface ual RUN_OP 分支派发" --compact
python3 scripts/query.py --type source-doc --compact
python3 scripts/query.py --tag precision --compact
python3 scripts/get_page.py doc-teco-ops-docs --follow-sources
python3 scripts/get_page.py doc-teco-ops-docs-p04 --follow-sources
python3 scripts/get_page.py kernel-teco-ops-flatten-rays --follow-sources
python3 scripts/get_page.py hw-teco-ops-hardware-model
python3 scripts/validate.py
```

## 范围边界与安全说明

本知识库按用户明确要求（"不使用其他内容，防止重要信息泄漏"）构建，内容来源严格限定为上述公开仓库的 `doc/` 目录与 4 份已获授权收录的官方手册。若需要更完整的 SDAA / 太初 T1 优化知识（含内部代码仓索引、全部官方手册、性能诊断模式库），请使用 `external/SDAAKernelWiki`；两者相互独立，不共享 `wiki/` curated 页面。

## License

仓库基础设施（scripts、schema、queries、references）与源自 `Tecorigin/teco-ops` `doc/` 目录的页面遵循 `LICENSE`（BSD-3-Clause，与 teco-ops 仓库一致）。4 份太初官方手册的结构化页面版权归 Tecorigin Co., Ltd. 所有，不属于 BSD-3-Clause 授权范围，仅作参考与开发者教育用途收录。详见 `NOTICE.md`。
