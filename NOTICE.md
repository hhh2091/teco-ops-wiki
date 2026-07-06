# NOTICE

This repository mixes four content sources with different licensing status.

## 1. Teco-Ops repository documentation (BSD-3-Clause)

`sources/docs/teco-ops-docs.md`, `sources/docs/teco-ops-docs/*.md`, and
`sources/docs/raw-teco-ops/*.txt` are derived from the `doc/` directory of
`https://github.com/Tecorigin/teco-ops` at commit
`d90ddf51f09374ea082f8b4f9dbf96190384b1f6`, which is licensed under the
BSD 3-Clause License (Copyright (c) 2025, Tecorigin Co., Ltd.). See `LICENSE`.

## 1b. Teco-AL repository documentation (BSD-3-Clause)

`sources/docs/teco-al-docs.md`, `sources/docs/teco-al-docs/*.md`, and
`sources/docs/raw-teco-al/*.txt` are derived from the `doc/` directory and
root `README.md` of `https://gitee.com/tecorigin/teco-al` (`develop` branch)
at commit `17c5cd66f0ca86d74e5f9c37d507656febfb8897`, which is licensed
under the BSD 3-Clause License (Copyright (c) 2024, Tecorigin Co., Ltd.).
The Teco-AL repository's own `LICENSE`/`NOTICE` files are not reproduced
here; the grant follows the same BSD-3-Clause terms as `LICENSE` in this
repository. Only `doc/` and `README.md` were ingested — the operator source
code under `interface/`, `ual/`, `custom_ops/`, `test/`, `samples/`, and
`SDAAC_examples/` was intentionally not copied into this knowledge base.

## 1c. PICT_smoke repository documentation (no license file; mixed authorship)

`sources/docs/pict-smoke-docs.md`, `sources/docs/pict-smoke-docs/*.md`, and
`sources/docs/raw-pict-smoke/*.txt` are derived from the root `README.md` and
`readme_en.md` of `https://github.com/Tecorigin/PICT_smoke` at commit
`9a928d46fe7370d12e7ad76ad9e6134ff949d2e5`. Unlike Teco-Ops and Teco-AL, this
repository has **no LICENSE file** (confirmed via the GitHub Licenses API,
which returned 404). Its two README files also have different authorship:

- `README.md` (Chinese) is Tecorigin-authored SDAA migration/training
  documentation, reproduced here as public repository documentation similar
  in status to the Tecorigin official manuals in section 2 below.
- `readme_en.md` (English) is substantially the original README of the
  upstream academic project *Physics-Informed Learning of Characteristic
  Trajectories for Smoke Reconstruction* (Wang, Tang, Chu; SIGGRAPH 2024;
  DOI 10.1145/3641519.3657483), copyright of the original authors, not
  Tecorigin. It is reproduced here for reference/citation purposes only.

Only the two README files were ingested — the model implementation and the
CUDA-to-SDAA custom-operator migration source
(`raymarching/src/`, `raymarching/src_sdaa/`, `src/`, `configs/`, `train.py`,
`test.py`, `env_test.py`) was intentionally not copied into this knowledge
base. If you are a rights holder (Tecorigin or the original PICT authors)
and object to this reproduction, please open an issue and it will be
addressed promptly.

## 2. Tecorigin official manuals (Tecorigin copyright, not BSD-3-Clause)

`sources/docs/sdaa-c-programming-guide-v3-1-0*`,
`sources/docs/sdaa-c-getting-started-v1-1-0*`,
`sources/docs/perf-optimization-sdaa-c-v2-0-2*`,
`sources/docs/perf-optimization-operator-v1-1-0*`,
`sources/docs/tecolibrt-user-manual-v1-2-0*`, and their corresponding
`sources/docs/raw/*.txt` files are structured excerpts of Tecorigin's own
official documentation (originally published at docs.tecorigin.net):

- SDAA C 编程指南 v3.1.0 (SDAA C Programming Guide)
- SDAA C 零基础入门 v1.1.0 (SDAA C Getting Started Guide)
- 性能优化手册-SDAA C 篇 v2.0.2 (Performance Optimization Handbook — SDAA C)
- 性能优化手册-算子篇 v1.1.0 (Performance Optimization Handbook — Operators)
- TecoLIBRT 用户手册 v1.2.0 (TecoLIBRT User Manual)

These materials are Tecorigin Co., Ltd.'s copyrighted documentation and are
reproduced here for reference and developer-education purposes only, not
under the BSD-3-Clause grant that covers the rest of this repository. All
rights to this content remain with Tecorigin Co., Ltd. If you are a rights
holder and object to this reproduction, please open an issue and it will be
addressed promptly.

## 3. Curated `wiki/` pages

The pages under `wiki/hardware/`, `wiki/techniques/`, `wiki/patterns/`, and
`wiki/kernels/` are original analysis written for this repository, synthesizing
and cross-referencing the sources above. They are covered by the
BSD-3-Clause license in `LICENSE`.
