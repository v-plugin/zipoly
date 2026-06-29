# Zipoly — Web3D Model Optimization Workbench

<p align="center">
  <a href="README.md">🇨🇳 简体中文</a> · <a href="README_EN.md">🇺🇸 English</a>
</p>

<p align="center">
  <a href="https://zipoly.netlify.app"><img src="https://zipoly.netlify.app/screenshot-overview.webp" alt="Zipoly Screenshot" width="720"/></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11-blue" alt="Platform"/>
  <img src="https://img.shields.io/badge/License-Commercial-orange" alt="License"/>
  <img src="https://img.shields.io/badge/Stack-Tauri%202%20%2B%20Rust-24c8db" alt="Tauri"/>
  <a href="https://zipoly.netlify.app"><img src="https://img.shields.io/badge/Docs-zipoly.netlify.app-6366f1" alt="Documentation"/></a>
</p>

<p align="center">
  <b>Draco + Meshopt Dual Engine · KTX2 GPU Textures · Diagnostics · Batch Processing · 100% Offline</b>
</p>

---

## 🎯 What is Zipoly?

**Zipoly** is a Windows desktop tool designed for **front-end developers, 3D artists, and designers**, focused on quality control and optimization of Web3D assets before delivery.

### Core Advantages

- ⚡ **Up to 90% size reduction** — Draco / Meshopt dual engine with smart fallback
- 🔄 **7 format conversions** — GLB, glTF, FBX, OBJ, STL, DAE, PLY
- 🎨 **KTX2 GPU texture compression** — Basis Universal ETC1S / UASTC, native GPU decoding
- 🔒 **100% offline operation** — No uploads, no tracking, no internet required, only 5 MB installer
- 🩺 **Smart diagnostics** — Auto-scan on import: duplicate vertices, oversized textures, missing normals
- 📦 **Batch processing** — Recursive folder scanning, concurrent processing, pause/resume/cancel support

---

## 📥 Download Now

<p align="center">
  <a href="https://github.com/v-plugin/zipoly/releases/latest">
    <img src="https://img.shields.io/badge/Download-Zipoly%20v2.0.1-6366f1?style=for-the-badge&logo=windows" alt="Download Zipoly"/>
  </a>
</p>

> **System Requirements**: Windows 10 / 11 (64-bit) · 4 GB RAM or more · No internet required

**Don't have Windows?** Try [Zipoly Web Online Version](https://zipoly-web.netlify.app) — Free, no installation, supports Draco compression and format conversion (100 MB file limit)

---

## ✨ Features Overview

| Module | Description | License |
|--------|-------------|:-------:|
| **Compression** | Draco / Meshopt geometry compression, 70–90% size reduction, scene presets | Available during trial |
| **Format Convert** | FBX / OBJ / STL / DAE / PLY → GLB / glTF, auto-embed external textures | Available during trial |
| **Texture Optimize** | Standalone image compression & resize, JPEG / WebP / KTX2 output | Available during trial |
| **3D Viewer** | Three.js real-time preview, 24-hour daylight simulation, screenshot & recording | **Free Forever** |
| **History Log** | Operation history, parameter reuse, report export | **Free Forever** |
| **Diagnostics** | Auto-scan on import, detect potential model issues | Available during trial |

---

## ⚡ Compression Engine Comparison

|  | Draco | Meshopt (Recommended) |
|--|-------|----------------------|
| **Compression Ratio** | High | Higher |
| **Decode Speed** | Fast | 5–10× faster |
| **Texture Compression** | JPEG / WebP / KTX2 | BasisU (ETC1S / UASTC) |
| **Framework Support** | Three.js / Babylon.js / model-viewer | Three.js (r136+) |
| **Best For** | Legacy projects, broad compatibility | New projects, peak performance |

> 💡 **Unsure which to choose?** Pick **Meshopt**. When Meshopt is unavailable, the software automatically falls back to Draco without affecting the workflow.

---

## 🎯 Scene Presets (One-Click Optimization)

Built-in 4 scene presets that auto-fill optimal parameters without manual tuning:

| Preset | Recommended Engine | Use Case |
|--------|-------------------|----------|
| 🌐 **Web 3D Scenes** | Meshopt | Web 3D displays, balanced quality & load speed |
| 📱 **Mobile Apps** | Meshopt | iOS / Android, aggressive compression to save bandwidth |
| 🏭 **Industrial Visualization** | Draco | CAD / BIM models, preserve high precision & node structure |
| 🛒 **E-commerce Display** | Meshopt | 3D product previews, high-quality textures + fast loading |

---

## 🚀 Quick Start

### 1. Compress Your First Model

```
① Drag .glb / .gltf file into the software window
② Select compression engine (Meshopt recommended) or choose a scene preset
③ Adjust compression level (default 7, suitable for most scenarios)
④ Click "Start Optimization"
⑤ Preview compression result, confirm appearance is correct, then save
```

### 2. Load Compressed Models in Three.js

**Draco Compression Format:**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js'

const dracoLoader = new DRACOLoader()
// Recommended: Copy decoder files to project's public directory (avoid external CDN dependency)
// cp node_modules/three/examples/jsm/libs/draco public/draco -r
dracoLoader.setDecoderPath('/draco/')

const loader = new GLTFLoader()
loader.setDRACOLoader(dracoLoader)
loader.load('model_optimized.glb', gltf => scene.add(gltf.scene))
```

**Meshopt Compression Format:**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { MeshoptDecoder } from 'three/addons/libs/meshopt_decoder.module.js'

const loader = new GLTFLoader()
loader.setMeshoptDecoder(MeshoptDecoder)
loader.load('model_optimized.glb', gltf => scene.add(gltf.scene))
```

**Meshopt + KTX2 Textures:**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { MeshoptDecoder } from 'three/addons/libs/meshopt_decoder.module.js'
import { KTX2Loader } from 'three/addons/loaders/KTX2Loader.js'

const ktx2Loader = new KTX2Loader()
// Recommended: Copy transcoder to project's public directory
// cp node_modules/three/examples/jsm/libs/basis public/basis -r
ktx2Loader.setTranscoderPath('/basis/')
ktx2Loader.detectSupport(renderer) // Detect current GPU supported KTX2 subformats

const loader = new GLTFLoader()
loader.setMeshoptDecoder(MeshoptDecoder)
loader.setKTX2Loader(ktx2Loader)
loader.load('model_optimized.glb', gltf => scene.add(gltf.scene))
```

> 💡 **Using Babylon.js or model-viewer?** These two frameworks **have built-in Draco support**, no extra configuration needed, just load directly. However, they **do not support Meshopt format**, please use Draco engine for compression.

---

## 📦 Supported Formats

| Format | Import | Export |
|--------|:------:|:------:|
| GLB | ✅ | ✅ |
| glTF | ✅ | ✅ |
| OBJ | ✅ | ✅ |
| FBX | ✅ | — |
| STL | ✅ | ✅ |
| DAE (Collada) | ✅ | — |
| PLY | ✅ | ✅ |

---

## 🎚️ Compression Level Reference

| Level | Use Case |
|-------|---------|
| 1–3 | Engineering / Medical models, precision first |
| 4–6 | Product display, architectural visualization |
| **7 (default)** | **General Web3D scenarios, best starting point** |
| 8–9 | Mobile, low bandwidth, acceptable slight distortion |
| 10 | Background decorations, visible geometry distortion |

> ⚠️ **Higher level ≠ Better**: Compression level 10 may cause vertex position offset and surface deformation. Start from 7, adjust downward if issues occur.

---

## 💰 Licensing & Pricing

First installation automatically grants a **6-hour complete trial** (cumulative duration, pauses when software is closed).

| Plan | Price | Description |
|------|-------|-------------|
| 1 Year License | **¥29.9** | Full features for one year |
| 2 Year License | **¥49.9** | Full features for two years |
| 3 Year License | **¥68** | Full features for three years |
| Lifetime License | **¥99** | One-time payment, permanent use |

**Plan Details:**
- ✅ All plans include full features (compression, conversion, texture optimization, screenshot recording)
- ✅ Device-bound offline verification, no internet required
- ✅ No auto-renewal
- ❌ One device per license, not transferable (reinstalling OS or changing PC requires repurchase)

**How to Purchase:**
1. Open software → System Settings
2. Copy your Device ID
3. Scan QR code to follow WeChat Official Account **RayChart**, reply `zipoly`
4. Provide Device ID to complete purchase

---

## ❓ FAQ

<details>
<summary><b>Model won't load after compression?</b></summary>

You need to configure a decoder. See complete code in [Three.js Loading Examples](#2-load-compressed-models-in-threejs) above.

Babylon.js and model-viewer have built-in Draco support, no extra configuration needed.
</details>

<details>
<summary><b>Getting "File already Draco-compressed, cannot compress again" error?</b></summary>

Draco does not support compressing already-compressed files. Please use the **original uncompressed GLB file** exported from modeling software (Blender / Maya / 3ds Max).
</details>

<details>
<summary><b>File size increased after compression?</b></summary>

Common with models having very few faces (< 1,000) or very small size (< 100 KB). Compression metadata overhead exceeds benefits, consider lowering compression level (1–3) or skip compression.
</details>

<details>
<summary><b>Model appears distorted or has artifacts after compression?</b></summary>

Insufficient quantization precision. Solutions:
1. Lower compression level (e.g., 9 → 7)
2. Or increase position precision `qp` in "Advanced Parameters" (Draco engine only)
</details>

<details>
<summary><b>KTX2 texture loading errors?</b></summary>

You need to configure `KTX2Loader`, see [Meshopt + KTX2 Loading Code](#2-load-compressed-models-in-threejs) above.

If target environment doesn't support KTX2 (e.g., older mobile browsers), switch to JPEG or WebP in texture settings.
</details>

<details>
<summary><b>Mac or Linux support?</b></summary>

Currently only supports Windows 10/11 (64-bit). Mac / Linux support is on the roadmap, expected in v1.3.
</details>

<details>
<summary><b>Will batch processing overwrite original files?</b></summary>

No. By default adds `_optimized` suffix. If suffix is empty, automatically adds `_1` numbering to prevent overwriting.
</details>

<details>
<summary><b>Will license remain valid after system reinstall?</b></summary>

No. Licenses use device fingerprinting. After OS reinstall or hardware change, original key becomes invalid and requires repurchase.

**Recommendation**: Fully utilize the 6-hour trial to confirm software meets your needs and device is stable before purchasing.
</details>

---

## 📝 Changelog

### v2.0.1 (Latest) — Dec 20, 2024
- 🐛 Fix: Removed all external CDN dependencies (Draco decoder, KTX2 transcoder, Google Fonts), now fully self-hosted
- 🐛 Fix: Hardened Tauri CSP security policy, removed googleapis / gstatic / jsdelivr external whitelist
- ⚡ Optimization: Web fonts now use @fontsource local packages (Noto Sans SC / Plus Jakarta Sans / JetBrains Mono)

### v2.0.0 — Nov 15, 2024
- 🎉 Architecture upgrade: Introduced unified compression engine interface, Draco / Meshopt hot-swappable with improved fallback mechanism
- ✨ New: Scene-based compression presets (Web / Mobile / Industrial / E-commerce)
- ✨ New: Smart engine recommendations (auto-suggest based on model characteristics)
- ⚡ Meshopt: Added mesh simplification, GPU Instancing, node merging with real-time staged progress
- ⚡ KTX2: Added UASTC mode with fine-grained quality parameters
- 🔧 Optimization: draco_transcoder size reduced (6 MB → 2.5 MB)

→ [View Complete Changelog](https://zipoly.netlify.app/guide/changelog)

---

## 🛠️ Tech Stack

- **Desktop Framework**: [Tauri 2](https://v2.tauri.app/) · Vue 3 · TypeScript · Rust
- **3D Rendering**: [Three.js](https://threejs.org/)
- **Compression Engines**: [draco_transcoder](https://github.com/google/draco) · [gltfpack / meshoptimizer](https://github.com/zeux/meshoptimizer)
- **Texture Compression**: [Basis Universal (basisu)](https://github.com/BinomialLLC/basis_universal)

---

## 🔗 Related Links

- 📖 [Online Documentation](https://zipoly.netlify.app) — Complete user manual
- 🌐 [Web Online Version](https://zipoly-web.netlify.app) — Free, no installation required
- 📦 [Download Page](https://github.com/v-plugin/zipoly/releases) — Historical version downloads
- 🐛 [Issue Reporting](https://github.com/v-plugin/zipoly/issues) — Submit bugs or suggestions
- 💬 WeChat Official Account: **RayChart** — Purchase licenses & technical support

---

## 📊 Real-World Data Comparison

| Model Type | Original Size | Optimized | Compression Ratio | Load Speed |
|-----------|--------------|-----------|-------------------|------------|
| Architectural Visualization | 128 MB | 18 MB | **-86%** | ↑ 7.1× |
| E-commerce Product Display | 56 MB | 9 MB | **-84%** | ↑ 6.2× |
| PNG Texture Maps | 22 MB | 2.1 MB | **-90%** | ↑ 10.5× |
| Industrial CAD Model | 84 MB | 12 MB | **-86%** | ↑ 7× |

*Data tested using default parameters (compression level 7)*

---

## 📄 License

**Commercial Software**

- ✅ 6-hour free trial
- 💰 Full license starts from ¥29.9/year
- 📜 See [Licensing & Pricing](#-licensing--pricing) for details

---

## 🤝 Contributing

This is a closed-source commercial software project. To report issues or suggest features, please contact us through:

- Submit [GitHub Issue](https://github.com/v-plugin/zipoly/issues)
- Follow WeChat Official Account **RayChart** and leave a message

---

<p align="center">
  <sub>Built with ❤️ by <a href="https://github.com/v-plugin">v-plugin</a></sub><br>
  <sub>© 2024–2026 v-plugin. All rights reserved.</sub>
</p>
