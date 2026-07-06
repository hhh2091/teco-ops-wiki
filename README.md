# teco-ops-wiki

teco-ops-wiki 是面向 Tecorigin 公开算子/模型生态（**Teco-Ops**：`https://github.com/Tecorigin/teco-ops`；**Teco-AL**：`https://gitee.com/tecorigin/teco-al`；**PICT_smoke**：`https://github.com/Tecorigin/PICT_smoke`）的本地结构化知识库。它复用了 SDAAKernelWiki 的组织方式（`data/`/`sources/`/`wiki/`/`queries/`/`references/` 分层、页面 schema、`query.py`/`get_page.py` 查询工具），但内容范围被刻意收窄，仅覆盖以下**公开、非敏感**来源：

- Teco-Ops 仓库 `doc/` 目录下的全部开发者文档（不含 `teco/`、`cuda/`、`api/`、`test/` 等算子源码目录）。
- Teco-AL 仓库（`develop` 分支）`doc/` 目录与根 `README.md`（不含 `interface/`、`ual/`、`custom_ops/`、`test/`、`samples/`、`SDAAC_examples/` 等算子源码/测试目录）。
- PICT_smoke 仓库（`main` 分支）根目录的两份 README（不含 `raymarching/`、`src/`、`configs/` 等模型实现与 CUDA→SDAA 迁移源码）。
- SDAAKernelWiki 中已有的 4 份太初官方手册：《SDAA C 编程指南 v3.1.0》《性能优化手册-算子篇 v1.1.0》《性能优化手册-SDAA C 篇 v2.0.2》《SDAA C 零基础入门手册 v1.1.0》。
- SDAAKernelWiki 中已有的 TecoLIBRT 用户手册 v1.2.0（索引页 + 7 个分卷页）。

**不包含**：SDAAKernelWiki 中其余全部官方手册、内部代码仓（`tecoal`/`sdcops`/`tecocustom`/`tecolmk`，这里的 `tecoal` 指内部 gerrit 仓库，与本知识库收录的公开 Gitee 仓库 `teco-al` 是两个不同的仓库）的算子索引与代码快照，以及上述三个公开仓库中文档之外的任何源码/测试/配置目录（Teco-Ops 的 `teco/`/`cuda/`/`api/`/`test/`、Teco-AL 的 `interface/`/`ual/`/`custom_ops/`/`test/`/`samples/`/`SDAAC_examples/`、PICT_smoke 的 `raymarching/`/`src/`/`configs/`）。这是有意的范围收窄，用于避免内部/敏感材料随知识库扩散，也避免知识库膨胀为源码镜像。

## 内容范围

- Teco-Ops 项目文档集（`doc-teco-ops-docs`，索引页 + 9 个分卷页）：算子提交规范（PR.md）、常见问题（QA.md）、SDAA C 程序调试手册（README_DEBUG.md）、算子开发指南（README_OP.md）、Plugin 自定义算子接口（README_PLUGIN.md）、PyTorch 扩展绑定（README_PYTHON.md）、算子开发硬件相关知识（teco-ops-hardware.md）、算子设计文档模板与 flatten_rays 范例（op_docs/）。
- Teco-AL 项目文档集（`doc-teco-al-docs`，索引页 + 19 个分卷页）：仓库总览与贡献指南（README.md）、开发指南（核心概念：句柄/张量/描述符/工作空间）、编程规范、16 个算子设计文档（其中 add_tensor/gemm/conv_forward 为含真实性能数据的完整讲解范例，其余 12 个为接口已定稿、性能优化留空的赛题参考文档）。
- PICT_smoke 项目文档集（`doc-pict-smoke-docs`，索引页 + 2 个分卷页）：SDAA 迁移版训练指南（中文）与原始 SIGGRAPH 2024 学术项目说明（英文），记录了一次真实的模型级 CUDA→SDAA 迁移案例（`TORCH_SDAA_AUTOLOAD`/`USE_SDAA` 两个接入点）。
- 4 份太初官方手册 + TecoLIBRT 用户手册的完整结构化来源页（索引页 + 分卷页 + 原文 `raw/*.txt`），与 SDAAKernelWiki 中的对应页面逐字节一致。
- 11 个策展 `wiki/` 页面：Teco-Ops 侧 6 个（硬件模型速览、interface+ual 分层开发、PyTorch 绑定、Plugin/Relay 注册、精度问题三类模式、flatten_rays 范例解析），Teco-AL 侧 4 个（分支递进式性能优化方法论、Hgemm/ConvolutionForward/AddTensor 三个真实性能数据案例解析），PICT_smoke 侧 1 个（模型级 CUDA→SDAA 自动迁移模式）。

## 快速命令

```bash
python3 scripts/query.py "flatten_rays tiling SPMD" --compact
python3 scripts/query.py "interface ual RUN_OP 分支派发" --compact
python3 scripts/query.py "gemm 分块 广播 双缓冲" --compact
python3 scripts/query.py "TORCH_SDAA_AUTOLOAD cuda_migrate" --compact
python3 scripts/query.py --type source-doc --compact
python3 scripts/query.py --tag precision --compact
python3 scripts/get_page.py doc-teco-ops-docs --follow-sources
python3 scripts/get_page.py doc-teco-al-docs --follow-sources
python3 scripts/get_page.py doc-pict-smoke-docs --follow-sources
python3 scripts/get_page.py kernel-teco-ops-flatten-rays --follow-sources
python3 scripts/get_page.py kernel-teco-al-gemm --follow-sources
python3 scripts/get_page.py technique-teco-al-algo-branch-benchmarking
python3 scripts/get_page.py technique-pict-smoke-cuda-sdaa-model-migration
python3 scripts/get_page.py hw-teco-ops-hardware-model
python3 scripts/validate.py
```

## 范围边界与安全说明

本知识库按用户明确要求（"不使用其他内容，防止重要信息泄漏"）构建，内容来源严格限定为上述公开仓库的文档目录（Teco-Ops/PICT_smoke 为 `doc/`或根 README，Teco-AL 为 `doc/`+ 根 `README.md`）与已获授权收录的官方手册。每个仓库在收录前均已通过官方 API 核实为公开仓库（GitHub `private: false` / Gitee `private: false`），Teco-AL 与 SDAAKernelWiki 中排除在外的内部 `tecoal` gerrit 仓库是两个独立项目，不构成内部材料泄漏。若需要更完整的 SDAA / 太初 T1 优化知识（含内部代码仓索引、全部官方手册、性能诊断模式库），请使用 `external/SDAAKernelWiki`；两者相互独立，不共享 `wiki/` curated 页面。

## License

仓库基础设施（scripts、schema、queries、references）与源自 `Tecorigin/teco-ops`、`tecorigin/teco-al`（Gitee）`doc/` 目录的页面遵循 `LICENSE`（BSD-3-Clause，与两仓库一致）。4 份太初官方手册与 TecoLIBRT 用户手册的结构化页面版权归 Tecorigin Co., Ltd. 所有，不属于 BSD-3-Clause 授权范围，仅作参考与开发者教育用途收录。PICT_smoke 项目文档集情况更特殊：该仓库本身未附带 LICENSE 文件，且英文 README 实质是原始 SIGGRAPH 2024 学术项目（Wang/Tang/Chu）的 README，版权归原作者所有，非 Tecorigin 授权范围，同样仅作参考与引用用途收录。详见 `NOTICE.md`。
