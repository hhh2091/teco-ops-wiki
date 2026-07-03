# teco-ops-wiki Primer

回答较宽泛的 Teco-Ops 算子开发问题前，先用这个 topic map 快速定位页面。

## Teco-Ops 项目文档（source-doc-part）

| 主题 | Page ID | 说明 |
|---|---|---|
| 算子提交规范 | `doc-teco-ops-docs-p01` | commit 消息格式、PR 规范（1 PR = 1 算子）、代码风格、cpplint 检查。 |
| 常见问题 | `doc-teco-ops-docs-p02` | proto 参数配置思路、Executor/Parser/MetaTensor 测试框架关系。 |
| 调试手册 | `doc-teco-ops-docs-p03` | printf 日志、TecoGDB、abort/assert、三类精度问题。 |
| 算子开发指南 | `doc-teco-ops-docs-p04` | interface+ual 分层架构、添加新算子九步流程、Proto 参数说明。 |
| Plugin 接口 | `doc-teco-ops-docs-p05` | Teco-Inference / TVM Relay IR 自定义算子注册。 |
| PyTorch 绑定 | `doc-teco-ops-docs-p06` | torch_ext.cpp 绑定步骤、setup.py 构建。 |
| 硬件相关知识 | `doc-teco-ops-docs-p07` | 异构计算、SU/SREG/VPU/VREG/FU/SPM、SPMD、存储与数据传输。 |
| 设计文档模板 | `doc-teco-ops-docs-p08` | 空白算子设计文档模板。 |
| flatten_rays 范例 | `doc-teco-ops-docs-p09` | 填写完整的算子设计文档范例。 |

## 策展 wiki 页面

| 主题 | Page ID | 适用场景 |
|---|---|---|
| 硬件与编程模型速览 | `hw-teco-ops-hardware-model` | 需要 SPA/SPE/SU/SREG/VPU/VREG/FU/SPM 速查表和 SPMD 切分公式时。 |
| interface+ual 分层开发 | `technique-teco-ops-interface-ual-layering` | 需要新增算子的完整九步流程与调用链路时。 |
| PyTorch 扩展绑定 | `technique-teco-ops-python-torch-binding` | 需要让算子可被 `import tecoops` 直接调用时。 |
| Plugin/TVM Relay 注册 | `technique-teco-ops-plugin-relay-registration` | 算子需要在 Teco-Inference 推理管线中使用时。 |
| 精度问题三类模式 | `pattern-teco-ops-precision-pitfalls` | 算子结果有偏差但不 crash，怀疑 half 截断/整型溢出/超越函数下溢时。 |
| flatten_rays 范例解析 | `kernel-teco-ops-flatten-rays` | 需要一个完整的 tiling + 三种暴露方式的参考实现时。 |

## 官方手册（4 份，完整结构化）

每份手册有索引页 `doc-*`（章节目录 + 分卷表 + 原文链接），完整正文在分卷页 `doc-*-p*` / `doc-*-g*`（`source-doc-part`），原文逐行存于 `sources/docs/raw/`。

| 主题 | 索引 Page ID | 用途 |
|---|---|---|
| SDAA C 语言/全部设备端 API | `doc-sdaa-c-programming-guide-v3-1-0` | 671 页权威指南：编程模型、语言规范、DMA/RMA/Broadcast/原子/matmul/transpose/SIMD 全部接口、编译调试、算子开发。 |
| 性能优化（SDAA C 篇） | `doc-perf-optimization-sdaa-c-v2-0-2` | 性能指标/采样、程序/线程/指令级并行、DMA/RMA/Broadcast 优化。 |
| 性能优化（算子篇） | `doc-perf-optimization-operator-v1-1-0` | 算子级优化方法论与案例。 |
| 入门 | `doc-sdaa-c-getting-started-v1-1-0` | 零基础教程。 |

## 常见问题快速路由

| 我想... | 先查 |
|---|---|
| 给 Teco-Ops 添加一个新算子 | `technique-teco-ops-interface-ual-layering` → `doc-teco-ops-docs-p04` |
| 写算子设计文档 | `kernel-teco-ops-flatten-rays`（有完整范例）+ `doc-teco-ops-docs-p08`（模板） |
| 让算子能被 PyTorch 直接调用 | `technique-teco-ops-python-torch-binding` |
| 让算子能在推理引擎里跑 | `technique-teco-ops-plugin-relay-registration` |
| 排查结果偏差但不崩溃的 bug | `pattern-teco-ops-precision-pitfalls` |
| 补充测试用例的 proto 参数 | `doc-teco-ops-docs-p02` |
| 提交 PR 前自查 | `doc-teco-ops-docs-p01` |
| 理解 SPA/SPE/SPMD 基础概念 | `hw-teco-ops-hardware-model` |
