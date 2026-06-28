# Zipoly — Web3D Model Optimizer / Web3D 模型体积优化工作台

<p align="center">
  <a href="https://zipoly.netlify.app"><img src="https://raw.githubusercontent.com/raychart/zipoly/main/docs-site/public/og-image.png" alt="Zipoly Screenshot" width="720"/></a>
</p>

<p align="center">
  <a href="https://github.com/raychart/zipoly/releases/latest"><img src="https://img.shields.io/github/v/release/raychart/zipoly?color=6366f1&label=Release" alt="Release"/></a>
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11-blue" alt="Platform"/>
  <img src="https://img.shields.io/badge/License-Commercial-orange" alt="License"/>
  <img src="https://img.shields.io/badge/Built%20with-Tauri%202%20%2B%20Rust-24c8db" alt="Tauri"/>
  <a href="https://zipoly.netlify.app"><img src="https://img.shields.io/badge/Docs-zipoly.netlify.app-6366f1" alt="Docs"/></a>
  <img src="https://img.shields.io/github/downloads/raychart/zipoly/total?color=success" alt="Downloads"/>
</p>

<p align="center">
  <b>Draco + Meshopt dual-engine · KTX2 GPU texture · Diagnostics · Batch processing · 100% offline</b><br>
  <b>Draco + Meshopt 双引擎 · KTX2 GPU 纹理 · 体检诊断 · 批量处理 · 完全离线</b>
</p>

<p align="center">
  <a href="#-english">English</a> · <a href="#-中文">中文</a>
</p>

---

## 🌍 English

### What is Zipoly?

**Zipoly** is a Windows desktop tool for 3D model optimization — built for front-end developers, 3D artists, and designers who need to deliver lightweight Web3D assets.

- Reduce geometry size by up to **90%** (Draco / Meshopt dual engine)
- Convert between **7 formats** — GLB, glTF, FBX, OBJ, STL, DAE, PLY
- GPU-native **KTX2** texture compression (Basis Universal ETC1S / UASTC)
- **100% offline** — no upload, no tracking, ~5 MB installer

### 📥 Download

**[⬇ Download Zipoly v2.0.1 for Windows x64](https://github.com/raychart/zipoly/releases/latest)**

> **Requirements:** Windows 10 / 11 (64-bit), 4 GB RAM, no internet required.

No Windows? Try [**Zipoly Web**](https://zipoly-web.netlify.app) — free, no install, supports Draco compression and format conversion (100 MB file limit).

### ✨ Features

| Module | Description | License |
|--------|-------------|:-------:|
| **Compression** | Draco / Meshopt geometry compression, 70–90% size reduction, scene presets | Trial |
| **Format Convert** | FBX / OBJ / STL / DAE / PLY → GLB / glTF, auto-embed textures | Trial |
| **Texture Optimize** | Standalone image compression, resize, JPEG / WebP / KTX2 output | Trial |
| **3D Viewer** | Three.js real-time preview, time-of-day lighting, screenshot / recording | **Free forever** |
| **History Log** | Operation history, parameter reuse, report export | **Free forever** |
| **Diagnostics** | Auto-scan on import: duplicate vertices, oversized textures, missing normals | Trial |

### ⚡ Engine Comparison

|  | Draco | Meshopt (Recommended) |
|--|-------|----------------------|
| Compression ratio | High | Higher |
| Decode speed | Fast | 5–10× faster |
| Texture compression | JPEG / WebP / KTX2 | BasisU (ETC1S / UASTC) |
| Framework support | Three.js / Babylon.js / model-viewer | Three.js (r136+) |
| Best for | Legacy projects, broad compatibility | New projects, peak performance |

> Unsure? Pick **Meshopt**. It auto-falls back to Draco when unavailable.

### 🎯 Scene Presets

One-click presets that auto-configure optimal parameters:

| Preset | Engine | Use Case |
|--------|--------|----------|
| 🌐 Web 3D | Meshopt | Web 3D scenes, balanced quality & load speed |
| 📱 Mobile | Meshopt | iOS / Android, aggressive compression |
| 🏭 Industrial | Draco | CAD / BIM, high precision + node hierarchy |
| 🛒 E-commerce | Meshopt | 3D product showcase, high-quality textures |

### 🚀 Quick Start

```
① Drop a .glb / .gltf file onto the app
② Select engine (Meshopt recommended) or pick a scene preset
③ Set compression level (default 7, works for most cases)
④ Click "Start Optimization"
⑤ Preview result — confirm visuals before saving
```

### 💻 Load Compressed Models in Three.js

**Draco:**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js'

const dracoLoader = new DRACOLoader()
dracoLoader.setDecoderPath('/draco/') // Copy from node_modules/three/examples/jsm/libs/draco
const loader = new GLTFLoader()
loader.setDRACOLoader(dracoLoader)
loader.load('model.glb', gltf => scene.add(gltf.scene))
```

**Meshopt:**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { MeshoptDecoder } from 'three/addons/libs/meshopt_decoder.module.js'

const loader = new GLTFLoader()
loader.setMeshoptDecoder(MeshoptDecoder)
loader.load('model.glb', gltf => scene.add(gltf.scene))
```

**Meshopt + KTX2:**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { MeshoptDecoder } from 'three/addons/libs/meshopt_decoder.module.js'
import { KTX2Loader } from 'three/addons/loaders/KTX2Loader.js'

const ktx2Loader = new KTX2Loader()
ktx2Loader.setTranscoderPath('/basis/') // Copy from node_modules/three/examples/jsm/libs/basis
ktx2Loader.detectSupport(renderer)

const loader = new GLTFLoader()
loader.setMeshoptDecoder(MeshoptDecoder)
loader.setKTX2Loader(ktx2Loader)
loader.load('model.glb', gltf => scene.add(gltf.scene))
```

> 💡 **Babylon.js** and **model-viewer** have built-in Draco support — no extra config needed. They do **not** support Meshopt format.

### 📦 Supported Formats

| Format | Import | Export |
|--------|:------:|:------:|
| GLB | ✅ | ✅ |
| glTF | ✅ | ✅ |
| OBJ | ✅ | ✅ |
| FBX | ✅ | — |
| STL | ✅ | ✅ |
| DAE (Collada) | ✅ | — |
| PLY | ✅ | ✅ |

### 🎚️ Compression Level Guide

| Level | Use Case |
|-------|---------|
| 1–3 | Engineering / Medical, precision first |
| 4–6 | Product display, architectural visualization |
| **7 (default)** | **General Web3D — best starting point** |
| 8–9 | Mobile / low-bandwidth, slight distortion acceptable |
| 10 | Background decor, visible geometry distortion |

### 💰 Pricing

First install gets a **6-hour free trial** (cumulative; pauses when closed).

| Plan | Price (CNY) |
|------|-------------|
| 1 Year | ¥29.9 |
| 2 Years | ¥49.9 |
| 3 Years | ¥68 |
| **Lifetime** | **¥99** |

All plans unlock full features. Device-bound offline activation. No auto-renewal.

**To purchase:** Open app → Settings → copy Device ID → follow WeChat **RayChart** and reply `zipoly`.

### ❓ FAQ

<details>
<summary><b>Model won't load after compression?</b></summary>

You need to configure a decoder. See the [loading code examples](#-load-compressed-models-in-threejs) above.
</details>

<details>
<summary><b>"File is already Draco-compressed" error?</b></summary>

Draco cannot compress an already-compressed file. Use the original uncompressed export.
</details>

<details>
<summary><b>File got larger after compression?</b></summary>

Common with tiny models (< 1,000 triangles or < 100 KB). Metadata overhead exceeds gains. Lower level or skip compression.
</details>

<details>
<summary><b>Distortion / artifacts after compression?</b></summary>

Lower compression level (9 → 7), or increase position quantization `qp` in advanced settings (Draco only).
</details>

<details>
<summary><b>Mac / Linux support?</b></summary>

Windows 10/11 (64-bit) only for now. Mac/Linux on roadmap.
</details>

### 🛠️ Tech Stack

- **Desktop:** [Tauri 2](https://v2.tauri.app/) · Vue 3 · TypeScript · Rust
- **3D:** [Three.js](https://threejs.org/)
- **Compression:** [draco_transcoder](https://github.com/google/draco) · [gltfpack](https://github.com/zeux/meshoptimizer)
- **Texture:** [Basis Universal](https://github.com/BinomialLLC/basis_universal)

### 🔗 Links

- 📖 [Documentation](https://zipoly.netlify.app)
- 🌐 [Web App (free)](https://zipoly-web.netlify.app)
- 📦 [Releases](https://github.com/raychart/zipoly/releases)
- 🐛 [Issues](https://github.com/raychart/zipoly/issues)

---

## 🇨🇳 中文

### Zipoly 是什么？

**Zipoly** 是一款面向前端开发者、3D 美术和设计师的 Windows 桌面端工具，专注 Web3D 资产交付前的质检与优化。

- 几何体积最高缩减 **90%**（Draco / Meshopt 双引擎）
- 支持 **7 种格式**互转（GLB / glTF / FBX / OBJ / STL / DAE / PLY）
- **KTX2** GPU 原生纹理压缩（Basis Universal ETC1S / UASTC）
- **完全离线**，数据不出本地，安装包约 **5 MB**

### 📥 下载

**[⬇ 下载 Zipoly v2.0.1（Windows x64）](https://github.com/raychart/zipoly/releases/latest)**

> 系统要求：Windows 10 / 11（64 位），4 GB 内存以上，无需联网。

没有 Windows？试试 [**Zipoly Web 在线版**](https://zipoly-web.netlify.app)，免费无需安装，支持 Draco 压缩和格式转换，单文件限制 100 MB。

### ✨ 功能概览

| 功能模块 | 说明 | 授权 |
|----------|------|:----:|
| **压缩优化** | Draco / Meshopt 几何压缩，体积缩减 70–90%，支持场景化预设 | 试用 |
| **格式转换** | FBX / OBJ / STL / DAE / PLY → GLB / glTF，外部贴图自动内嵌 | 试用 |
| **纹理优化** | 独立图片文件压缩、缩放，支持输出 JPEG / WebP / KTX2 | 试用 |
| **3D 查看器** | Three.js 实时预览，时间光照模拟，自定义灯光，截图/录制 | **永久免费** |
| **操作日志** | 历史记录，支持参数复用和报告导出 | **永久免费** |
| **体检诊断** | 导入自动扫描，检出重复顶点、超规格纹理、缺失法线等问题 | 试用 |

### ⚡ 压缩引擎对比

|  | Draco | Meshopt（推荐） |
|--|-------|----------------|
| 压缩率 | 高 | 更高 |
| 解码速度 | 快 | 快 5–10 倍 |
| 纹理压缩 | JPEG / WebP / KTX2 | BasisU（ETC1S / UASTC） |
| 框架支持 | Three.js / Babylon.js / model-viewer | Three.js（r136+） |
| 最适合 | 旧项目、广泛兼容 | 新项目、极致性能 |

> 不确定选哪个？选 **Meshopt**。Meshopt 不可用时软件自动降级到 Draco，不影响处理。

### 🎯 场景化预设

内置四种一键预设，自动填充最优参数：

| 预设 | 推荐引擎 | 适用场景 |
|------|---------|---------|
| 🌐 Web 3D 场景 | Meshopt | 网页端 3D 展示，平衡质量与加载速度 |
| 📱 移动端应用 | Meshopt | iOS/Android，极致压缩节省流量 |
| 🏭 工业可视化 | Draco | CAD 模型，保留高精度和节点结构 |
| 🛒 电商产品展示 | Meshopt | 3D 商品预览，高质量纹理 + 快速加载 |

### 🚀 快速上手

```
① 拖入 .glb / .gltf 文件
② 选择引擎（推荐 Meshopt）或选择场景预设
③ 调整压缩级别（默认 7，适合大多数场景）
④ 点击"开始优化"
⑤ 预览压缩结果，确认外观无误后保存
```

### 🎚️ 压缩级别参考

| 级别 | 适用场景 |
|------|---------|
| 1–3 | 工程 / 医疗模型，精度优先 |
| 4–6 | 产品展示、建筑可视化 |
| **7（默认）** | **Web3D 通用，最佳起点** |
| 8–9 | 移动端、低带宽，可接受轻微失真 |
| 10 | 远景装饰，几何失真明显 |

### 💰 授权与定价

首次安装自动获得 **6 小时完整试用**（累计时长，关闭软件后暂停计时）。

| 套餐 | 价格 |
|------|------|
| 1 年 | ¥29.9 |
| 2 年 | ¥49.9 |
| 3 年 | ¥68 |
| **终身** | **¥99** |

所有套餐包含全部功能，设备绑定离线验证，不自动续费，一机一码。

**购买方式**：打开软件系统设置复制设备 ID，扫码关注微信公众号 **RayChart**，回复 `zipoly` 联系购买。

### ❓ 常见问题

<details>
<summary><b>压缩后模型加载不出来？</b></summary>

需要配置解码器，详见上方 Three.js 加载代码示例。
</details>

<details>
<summary><b>提示"该文件已经过 Draco 压缩"？</b></summary>

Draco 不支持重复压缩，请使用从建模软件导出的原始未压缩文件。
</details>

<details>
<summary><b>压缩后文件反而变大了？</b></summary>

常见于面数极少（< 1000 面）或体积本身很小（< 100 KB）的模型，可降低级别或不压缩。
</details>

<details>
<summary><b>压缩后出现变形或锯齿？</b></summary>

降低压缩级别（如 9 → 7），或提高高级参数中的位置精度 qp（仅 Draco）。
</details>

<details>
<summary><b>支持 Mac 或 Linux 吗？</b></summary>

目前仅支持 Windows 10/11（64 位），Mac/Linux 支持在路线图中。
</details>

### 📝 更新日志

#### v2.0.1（最新）
- 修复：移除所有外部 CDN 依赖，改为完全本地化加载
- 修复：Tauri CSP 安全策略精简
- 优化：Web 端字体改用 @fontsource 本地包

#### v2.0.0
- 引入统一压缩引擎接口，Draco / Meshopt 热插拔
- 新增场景化压缩预设（Web / 移动 / 工业 / 电商）
- 新增智能引擎推荐
- Meshopt：网格简化、GPU Instancing、节点合并
- KTX2：新增 UASTC 模式

→ [完整更新日志](https://zipoly.netlify.app/guide/changelog)

### 🔗 链接

- 📖 [在线文档](https://zipoly.netlify.app)
- 🌐 [Web 在线版](https://zipoly-web.netlify.app)
- 📦 [发布页面](https://github.com/raychart/zipoly/releases)
- 🐛 [问题反馈](https://github.com/raychart/zipoly/issues)

---

## 📄 License / 授权

**Commercial Software / 商业软件**

- Free 6-hour trial / 免费试用 6 小时
- Full license starts from ¥29.9/year / 完整授权最低 ¥29.9/年
- See [Pricing](#-pricing) / [定价](#-授权与定价)

---

## 🤝 Contributing / 贡献

This is a closed-source commercial project. For bug reports or feature requests, please open an [issue](https://github.com/raychart/zipoly/issues).

本项目为闭源商业软件。如需报告问题或建议功能，请提交 [issue](https://github.com/raychart/zipoly/issues)。

---

<p align="center">
  <sub>Built with ❤️ by <a href="https://github.com/raychart">RayChart</a></sub><br>
  <sub>© 2024–2026 RayChart. All rights reserved.</sub>
</p>
