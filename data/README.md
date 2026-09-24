# 结果数据原件

本目录存放报告页头条数字的**机器可读原始 JSON**（未手抄、未改写）。

| 文件 | 内容 | 支撑的头条数字 |
|---|---|---|
| `canonical_analysis.json` | Time-to-Map 各档位：ret_final / u8-PSNR / 质量门（0.10/0.15/0.20）达线时刻 [iters, 秒] / 独占墙钟 | T@0.15=698s、预算阶梯 0.038→0.243→0.337、上限 0.426 |
| `retention.json` | 调度与压缩各配置的逐检查点序列（retention / psnr_u8 / n_gauss / 墙钟） | 调度不敏感、"何时生长"非杠杆、压缩阶梯曲线 |
| `bench.json` | 渲染基准（同 GPU 同 25 视图，warmup 10 计 50）：FPS / 可见高斯（radii>0 均值±std）/ peak VRAM | L2 档 −20.4% 高斯 / +15.3% FPS / −7.5% VRAM |
| `ate_e18b_metric_ba.json` | AQUALOC 米制化 ATE：ate_se3_m=0.5775（行文四舍五入为 0.578）、ate_sim3_m=0.5679、sim3_scale=0.9525；对照 raw=1.6762 | 米制化 −65.5% ATE |

注：`bench.json` 中 `ply` 字段为产生该模型的内部产物路径（本地训练机），
仅作溯源用；本仓库不含 PLY 模型本体。
