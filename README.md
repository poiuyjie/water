# water — 水下 3D Gaussian Splatting 建图系统 · Time-to-Map

> 研究主线：**在保证地图质量的前提下，最小化"从水下视频到可用 3DGS 地图"的时间。**
> 免离线 COLMAP，浑水边采集边建图。

![位姿光度一致性决定渲染质量](docs/assets/filmstrip_slam_vs_hq.jpg)

上：常规 SLAM 位姿直接喂 3DGS（概览级）；下：光度一致位姿 + 双输出联合 init（高质量）。
位姿的局部光度一致性是水下 3DGS 画质的第一张入场券。

<p align="center">
  <video src="docs/assets/flythrough_fullseq.mp4" poster="docs/assets/video_poster.jpg" controls width="800"></video>
</p>
<p align="center"><sub>↑ 主交付 · 全序列 150k 步 · 1017 帧 · ~100 s · E-2026-1007-05（2026-10 增补）</sub></p>

## 🛰️ DIRECT 深度模型怎么用

| 分支 | 用法 | 效果 |
|------|------|------|
| **D 深度** | **几何初始化桥**：逐帧深度米制定标后反投影成点云，追加进持久高斯地图 | 整条管线**免 COLMAP**，浑水可跑 |
| **D 深度** | **米制源**：全局单参数定标 s_d = median(z/z_direct)，无真值参与 | AQUALOC 轨迹 **1.676 → 0.578 m（−65.5%）** |
| **D 深度** | **压缩调度器**：深度多视角一致性 = 逐高斯置信度，门控 densify | **高斯 −20.4% / 渲染 FPS +15.3%（实测 208→240）**，质量持平 |

## 📊 核心结果（2026-10 增补 · 我们 vs SfM）

| # | 结果 | 数字 |
|---|------|------|
| ① | **Time-to-Map** | T@0.15 = **698 s**（170 帧，含推理与评测） |
| ② | **预算响应阶梯** | 锐度 retention **0.038 → 0.243 → 0.337**（6.8k / 20.4k / 40.8k iters） |
| ③ | **我们 vs SfM**（10 月增补，E-2026-1007-05） | PSNR **31.66 vs 27.57（+4.09 dB）** · Lap **10.56 vs 12.61** · 高斯 **833k vs 912k（−8.6%）** |

**正式措辞（引用请逐字）**：

> 在 DIRECT D-init + 在线位姿 + 增量 3DGS 条件下，系统地测得优化预算是早期地图质量的
> 一阶因素；位姿质量在预算提升后成为进一步限制因素；若干直觉上的
> depth/fusion/densification 调整未显示同量级收益。

不声称"解决了水下 3DGS 核心难点"。

## 🎬 导览

- 🌐 **完整报告页（GitHub Pages）**：<https://poiuyjie.github.io/water/> ——
  双输出用法 → 主结果 → 在线 vs 离线账本，全部图表与视频。
- ▶ **对照：在线 698 s 增量建出的地图本体**（`flythrough_online_A3.mp4`）

<p align="center">
  <video src="docs/assets/flythrough_online_A3.mp4" poster="docs/assets/video_poster_online.jpg" controls width="800"></video>
</p>

- 📊 **结果数据原件**：[`data/`](data/) —— 预算阶梯 / retention 曲线 / 渲染基准 / ATE 原始 JSON。

## ⚠️ 边界（诚实条目）

- 主结论在 coral 浑水序列（170 帧，单场景）；AQUALOC（441 帧）复现预算-响应趋势。
- 在线建图为 near-online（170 帧约 15 分钟），非 real-time。
- 增量 → batch 存在 ~0.06 结构性锐度税，本页如实呈现差距而非回避。

---

*冻结于 2026-09-24 · 10 月增补（E-2026-1007-05 全序列 150k 步预算响应）· 本仓库为项目展示层，数字与图表均为最终冻结口径。*
