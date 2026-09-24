# canonical 数据原件

本目录存放报告页全部头条数字的**机器可读原始 JSON**（未手抄、未改写），
每份文件标注其来源实验记录（E 编号，项目内部档案）。

| 文件 | 内容 | 来源 |
|---|---|---|
| `canonical_analysis.json` | 预算阶梯 canonical 八臂：ret_final / u8-PSNR / 质量门（0.10/0.15/0.20）达线时刻 [iters, 秒] / 独占墙钟。头条数字 T@0.15=698s、阶梯 0.038→0.243→0.337、上限 REF=0.426 均出于此 | E2026-0924-07 |
| `retention.json` | 调度格点七变体（DELAY/SHIFT 等）+ 压缩阶梯 L0–L3 的逐检查点序列（retention / psnr_u8 / n_gauss / 墙钟） | E2026-0924-09 |
| `bench.json` | 渲染基准（同 GPU 同 25 视图，warmup 10 计 50）：FPS / 可见高斯（radii>0 均值±std）/ peak VRAM。L2 的 +15.3% FPS 出于此 | E2026-0924-07（A3/REF）+ E2026-0924-09（L0–L3） |
| `ate_e18b_metric_ba.json` | AQUALOC 米制化 ATE：ate_se3_m=0.5775（canonical 行文四舍五入为 0.578）、ate_sim3_m=0.5679、sim3_scale=0.9525；对照 raw=1.6762 | E2026-0921-18 |

注：`bench.json` 中 `ply` 字段为产生该模型的内部产物路径（服务器本地），
仅作溯源用；本仓库不含 PLY 模型本体。
