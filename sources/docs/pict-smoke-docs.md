---
id: doc-pict-smoke-docs
title: "PICT_smoke 项目文档集"
type: source-doc
source_category: public-repo-doc
product_version: "commit 9a928d4"
published_at: "2026-07-06"
created_at: "2026-07-06"
captured_at: "2026-07-10"
author: "Tecorigin/PICT_smoke (GitHub)"
doc_kind: repo-documentation
source_repo: "https://github.com/Tecorigin/PICT_smoke"
source_branch: "main"
source_commit: "9a928d46fe7370d12e7ad76ad9e6134ff949d2e5"
license: "unspecified upstream; original PICT project is SIGGRAPH 2024 academic code (see readme_en.md citation)"
source_file: "README.md, readme_en.md"
raw_text: "sources/docs/raw-pict-smoke/"
architectures: [sdaa, teco-t1]
tags: [pict-smoke, cuda-migration, model-zoo, raymarching, pytorch-extension, siggraph]
languages: [cpp, python, zh-cn]
confidence: verified
---

# PICT_smoke 项目文档集

> PICT_smoke 是 Tecorigin 对开源学术项目 *Physics-Informed Learning of Characteristic Trajectories for Smoke Reconstruction*（SIGGRAPH 2024，烟雾重建的物理信息特征轨迹学习）做 CUDA→SDAA 自定义算子迁移后的模型仓库，用于验证/演示该模型可在 SDAA 平台上运行。仓库定位为 ModelZoo 中的一个迁移示例（原文路径引用 `<ModelZoo_path>/PyTorch/build-in/Detection/PICT_smoke`），而非算子开发框架，与 Teco-Ops/Teco-AL 的性质不同。

这是 PICT_smoke 项目文档集的**索引页**。本仓库文件规模很小（45 个文件），且没有独立的 `doc/` 目录，文档内容仅为仓库根目录的两份 README。完整正文按原始文件切分在下方 `part` 子页中（共 2 部分）。

## 文档元信息

- 来源仓库：`https://github.com/Tecorigin/PICT_smoke`（公开仓库，非私有，BSD 等开源协议未在仓库中声明；原始学术项目引用信息见 p02）
- 采集分支：`main`
- 采集 commit：`9a928d46fe7370d12e7ad76ad9e6134ff949d2e5`（2026-07-06，仓库创建后 4 天内的采集）
- 采集范围：仅仓库根目录的 `README.md`（中文，SDAA 迁移与训练指南）与 `readme_en.md`（英文，原始学术项目说明与引用信息）
- 原始全文：`sources/docs/raw-pict-smoke/`（逐文件保留，未做任何改写）

## 完整内容分卷（part 子页）

| Part | 原始文件 | 主题 | 行数 | 页面 |
|------|---------|------|------|------|
| p01 | `README.md` | SDAA 迁移与训练指南（中文）：环境安装、数据集获取、raymarching 扩展的 SDAA 构建、启动训练 | 74 | `doc-pict-smoke-docs-p01` |
| p02 | `readme_en.md` | 原始学术项目说明（英文）：项目/论文/视频链接、原始 CUDA 环境搭建、训练/测试命令、SIGGRAPH 2024 引用信息 | 83 | `doc-pict-smoke-docs-p02` |

## 未收录内容（仅记录规模与位置，供按需查阅上游仓库）

以下目录是模型的实际实现代码与 CUDA→SDAA 算子迁移源码，未纳入本知识库（与 Teco-Ops/Teco-AL 的收录边界原则一致——仅收录文档，不收录源码）：

| 目录/文件 | 文件数 | 说明 |
|---|---|---|
| `raymarching/src/` | 4 | 原始 CUDA 实现：`raymarching.cu`（63,623 字节）、`raymarching.h`、`pcg32.h`、`bindings.cpp`——这是本仓库中体量最大、信息密度最高的部分。 |
| `raymarching/src_sdaa/` | 3 | 对应的 SDAA 迁移实现：`raymarching.scpp`（104,054 字节）、`raymarching.h`、`bindings.cpp`——与 `src/` 逐文件对应，构成一组完整的 CUDA→SDAA 迁移前后对照。 |
| `raymarching/` 根 | 3 | `__init__.py`、`backend.py`、`raymarching.py`（PyTorch 扩展 Python 封装层） |
| `src/` | 15 | 模型本体：`network/`（hybrid_model、lagrangian_field、neus_field、siren_basic）、`renderer/`（occupancy_grid、render_ray）、`dataset/`、`utils/` |
| `configs/` | 4 | 训练配置文件（`car.txt`/`cyl.txt`/`game.txt`/`scalar.txt`） |
| 根目录脚本 | 3 | `train.py`、`test.py`、`env_test.py` |

`raymarching/src/` 与 `raymarching/src_sdaa/` 这一对目录是一次真实的、逐文件对应的 CUDA 自定义算子到 SDAA `.scpp` 的迁移案例，体量较大（源文件超过 60KB/100KB），本知识库出于"只收录文档、不收录源码"的一贯原则未做逐字快照，仅在 `technique-pict-smoke-cuda-sdaa-model-migration` 页面中记录其构建方式与迁移涉及的环境变量/接入点，实际迁移代码需查阅上游仓库对应 commit。
