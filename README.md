# Zipoly — Web3D 模型体积优化工作台

<p align="center">
  <a href="https://zipoly.netlify.app"><img src="https://zipoly.netlify.app/screenshot-overview.webp" alt="Zipoly 截图" width="720"/></a>
</p>

<p align="center">
  <a href="https://github.com/raychart/zipoly/releases/latest"><img src="https://img.shields.io/github/v/release/raychart/zipoly?color=6366f1&label=最新版本" alt="版本"/></a>
  <img src="https://img.shields.io/badge/平台-Windows%2010%2F11-blue" alt="平台"/>
  <img src="https://img.shields.io/badge/授权-商业软件-orange" alt="授权"/>
  <img src="https://img.shields.io/badge/技术栈-Tauri%202%20%2B%20Rust-24c8db" alt="Tauri"/>
  <img src="https://img.shields.io/github/downloads/raychart/zipoly/total?color=success&label=下载量" alt="下载量"/>
</p>

<p align="center">
  <b>Draco + Meshopt 双引擎 · KTX2 GPU 纹理 · 体检诊断 · 批量处理 · 完全离线</b>
</p>

<p align="center">
  <a href="README_ZH.md">🇨🇳 简体中文</a> · <a href="README_EN.md">🇺🇸 English</a>
</p>

---

## 🎯 Zipoly 是什么？

**Zipoly** 是一款专为**前端开发者、3D 美术、设计师**打造的 Windows 桌面工具，聚焦 Web3D 资产交付前的质检与优化。

### 核心优势

- ⚡ **体积最高缩减 90%** — Draco / Meshopt 双引擎，智能降级
- 🔄 **支持 7 种格式互转** — GLB、glTF、FBX、OBJ、STL、DAE、PLY
- 🎨 **KTX2 GPU 纹理压缩** — Basis Universal ETC1S / UASTC，GPU 原生解码
- 🔒 **100% 离线运行** — 数据不上传，不联网，安装包仅 5 MB
- 🩺 **智能体检诊断** — 导入即扫描，检出重复顶点、超规格纹理、缺失法线
- 📦 **批量处理** — 文件夹递归扫描，并发处理，支持暂停/继续/取消

---

## 📥 立即下载

<p align="center">
  <a href="https://github.com/raychart/zipoly/releases/latest">
    <img src="https://img.shields.io/badge/下载-Zipoly%20v2.0.1-6366f1?style=for-the-badge&logo=windows" alt="下载 Zipoly"/>
  </a>
</p>

> **系统要求**：Windows 10 / 11（64 位）· 4 GB 内存以上 · 无需联网

**没有 Windows 电脑？** 试试 [Zipoly Web 在线版](https://zipoly-web.netlify.app) — 免费，无需安装，支持 Draco 压缩和格式转换（单文件限制 100 MB）

---

## ✨ 功能一览

| 模块 | 功能说明 | 授权 |
|------|---------|:----:|
| **压缩优化** | Draco / Meshopt 几何压缩，体积缩减 70–90%，支持场景化预设 | 试用期内可用 |
| **格式转换** | FBX / OBJ / STL / DAE / PLY → GLB / glTF，外部贴图自动内嵌 | 试用期内可用 |
| **纹理优化** | 独立图片文件压缩、缩放，支持 JPEG / WebP / KTX2 输出 | 试用期内可用 |
| **3D 查看器** | Three.js 实时预览，24 小时光照模拟，截图与录制 | **永久免费** |
| **操作日志** | 历史记录，参数复用，导出报告 | **永久免费** |
| **体检诊断** | 导入自动扫描，检出模型潜在问题 | 试用期内可用 |

---

## ⚡ 压缩引擎对比

|  | Draco | Meshopt（推荐） |
|--|-------|----------------|
| **压缩率** | 高 | 更高 |
| **解码速度** | 快 | 快 5–10 倍 |
| **纹理压缩** | JPEG / WebP / KTX2 | BasisU（ETC1S / UASTC） |
| **框架兼容** | Three.js / Babylon.js / model-viewer | Three.js（r136+） |
| **最适合** | 旧项目、广泛兼容 | 新项目、极致性能 |

> 💡 **不确定选哪个？** 选 **Meshopt**。Meshopt 不可用时软件会自动降级到 Draco，不影响处理流程。

---

## 🎯 场景化预设（一键优化）

软件内置 4 种场景预设，自动填充最优参数，无需手动调参：

| 预设 | 推荐引擎 | 适用场景 |
|------|---------|---------|
| 🌐 **Web 3D 场景** | Meshopt | 网页端 3D 展示，平衡质量与加载速度 |
| 📱 **移动端应用** | Meshopt | iOS / Android，极致压缩节省流量 |
| 🏭 **工业可视化** | Draco | CAD / BIM 模型，保留高精度和节点结构 |
| 🛒 **电商产品展示** | Meshopt | 3D 商品预览，高质量纹理 + 快速加载 |

---

## 🚀 快速开始

### 1. 压缩第一个模型

```
① 拖入 .glb / .gltf 文件到软件窗口
② 选择压缩引擎（推荐 Meshopt）或选择场景预设
③ 调整压缩级别（默认 7，适合绝大多数场景）
④ 点击"开始优化"
⑤ 预览压缩结果，确认外观无误后保存
```

### 2. 在 Three.js 中加载压缩后的模型

**Draco 压缩格式：**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js'

const dracoLoader = new DRACOLoader()
// 推荐：将解码器文件复制到项目 public 目录（避免依赖外部 CDN）
// cp node_modules/three/examples/jsm/libs/draco public/draco -r
dracoLoader.setDecoderPath('/draco/')

const loader = new GLTFLoader()
loader.setDRACOLoader(dracoLoader)
loader.load('model_optimized.glb', gltf => scene.add(gltf.scene))
```

**Meshopt 压缩格式：**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { MeshoptDecoder } from 'three/addons/libs/meshopt_decoder.module.js'

const loader = new GLTFLoader()
loader.setMeshoptDecoder(MeshoptDecoder)
loader.load('model_optimized.glb', gltf => scene.add(gltf.scene))
```

**Meshopt + KTX2 纹理：**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { MeshoptDecoder } from 'three/addons/libs/meshopt_decoder.module.js'
import { KTX2Loader } from 'three/addons/loaders/KTX2Loader.js'

const ktx2Loader = new KTX2Loader()
// 推荐：将转码器复制到项目 public 目录
// cp node_modules/three/examples/jsm/libs/basis public/basis -r
ktx2Loader.setTranscoderPath('/basis/')
ktx2Loader.detectSupport(renderer) // 检测当前 GPU 支持的 KTX2 子格式

const loader = new GLTFLoader()
loader.setMeshoptDecoder(MeshoptDecoder)
loader.setKTX2Loader(ktx2Loader)
loader.load('model_optimized.glb', gltf => scene.add(gltf.scene))
```

> 💡 **使用 Babylon.js 或 model-viewer？** 这两个框架**内置 Draco 支持**，无需额外配置，直接加载即可。但它们**不支持 Meshopt 格式**，请使用 Draco 引擎压缩。

---

## 📦 支持的格式

| 格式 | 导入 | 导出 |
|------|:----:|:----:|
| GLB | ✅ | ✅ |
| glTF | ✅ | ✅ |
| OBJ | ✅ | ✅ |
| FBX | ✅ | — |
| STL | ✅ | ✅ |
| DAE (Collada) | ✅ | — |
| PLY | ✅ | ✅ |

---

## 🎚️ 压缩级别参考

| 级别 | 适用场景 |
|------|---------|
| 1–3 | 工程 / 医疗模型，精度优先 |
| 4–6 | 产品展示、建筑可视化 |
| **7（默认）** | **Web3D 通用场景，最佳起点** |
| 8–9 | 移动端、低带宽，可接受轻微失真 |
| 10 | 远景装饰物，几何失真明显 |

> ⚠️ **级别越高 ≠ 越好**：压缩级别 10 可能导致顶点位置偏移、曲面变形。建议从 7 开始，遇到问题再向下调整。

---

## 💰 授权与定价

首次安装自动获得 **6 小时完整试用**（累计时长，关闭软件后暂停计时）。

| 套餐 | 价格 | 说明 |
|------|------|------|
| 1 年授权 | **¥29.9** | 一年内全功能使用 |
| 2 年授权 | **¥49.9** | 两年内全功能使用 |
| 3 年授权 | **¥68** | 三年内全功能使用 |
| 终身授权 | **¥99** | 一次付费永久使用 |

**套餐说明：**
- ✅ 所有套餐包含全部功能（压缩、转换、纹理优化、截图录制）
- ✅ 设备绑定离线验证，无需联网
- ✅ 不自动续费
- ❌ 一机一码，不可跨设备使用（重装系统或更换电脑需重新购买）

**购买方式：**
1. 打开软件 → 系统设置
2. 复制你的设备 ID
3. 扫码关注微信公众号 **RayChart**，回复 `zipoly`
4. 提供设备 ID 完成购买

---

## ❓ 常见问题

<details>
<summary><b>压缩后模型加载不出来怎么办？</b></summary>

需要配置解码器。完整代码见上方 [Three.js 加载示例](#2-在-threejs-中加载压缩后的模型)。

Babylon.js 和 model-viewer 内置 Draco 支持，无需额外配置。
</details>

<details>
<summary><b>提示"该文件已经过 Draco 压缩，无法重复压缩"？</b></summary>

Draco 不支持对已压缩文件再次压缩。请使用从建模软件（Blender / Maya / 3ds Max）导出的**原始未压缩 GLB 文件**。
</details>

<details>
<summary><b>压缩后文件反而变大了？</b></summary>

常见于面数极少（< 1000 面）或体积本身很小（< 100 KB）的模型。压缩元数据开销超过收益，可以降低压缩级别（1–3）或直接不压缩。
</details>

<details>
<summary><b>压缩后模型出现变形、锯齿怎么办？</b></summary>

量化精度不足。解决方案：
1. 降低压缩级别（如 9 → 7）
2. 或在"高级参数"中提高位置精度 `qp`（仅 Draco 引擎）
</details>

<details>
<summary><b>KTX2 纹理加载报错？</b></summary>

需要配置 `KTX2Loader`，见上方 [Meshopt + KTX2 加载代码](#2-在-threejs-中加载压缩后的模型)。

如果目标环境不支持 KTX2（如旧版移动浏览器），在纹理设置中切换为 JPEG 或 WebP。
</details>

<details>
<summary><b>支持 Mac 或 Linux 吗？</b></summary>

目前仅支持 Windows 10/11（64 位）。Mac / Linux 支持在产品路线图中，预计 v1.3 版本。
</details>

<details>
<summary><b>批量处理会覆盖原文件吗？</b></summary>

不会。默认追加 `_optimized` 后缀，如果后缀为空会自动添加 `_1` 序号防止覆盖。
</details>

<details>
<summary><b>重装系统后授权还在吗？</b></summary>

不在。授权采用设备指纹绑定，重装系统或更换硬件后原密钥失效，需重新购买。

**建议**：购买前充分试用 6 小时，确认软件满足需求且设备稳定再购买。
</details>

---

## 📝 更新日志

### v2.0.1（最新）— 2024-12-20
- 🐛 修复：移除所有外部 CDN 依赖（Draco 解码器、KTX2 转码器、Google Fonts），改为完全本地化加载
- 🐛 修复：Tauri CSP 安全策略精简，移除 googleapis / gstatic / jsdelivr 外网白名单
- ⚡ 优化：Web 端字体改用 @fontsource 本地包（Noto Sans SC / Plus Jakarta Sans / JetBrains Mono）

### v2.0.0 — 2024-11-15
- 🎉 架构升级：引入统一压缩引擎接口，Draco / Meshopt 热插拔，降级机制完善
- ✨ 新增：场景化压缩预设（Web / 移动 / 工业 / 电商）
- ✨ 新增：智能引擎推荐（根据模型特征自动建议）
- ⚡ Meshopt：支持网格简化、GPU Instancing、节点合并，实时分阶段进度
- ⚡ KTX2：新增 UASTC 模式，质量参数精细化
- 🔧 优化：draco_transcoder 体积精简（6 MB → 2.5 MB）

→ [查看完整更新日志](https://zipoly.netlify.app/guide/changelog)

---

## 🛠️ 技术栈

- **桌面端框架**：[Tauri 2](https://v2.tauri.app/) · Vue 3 · TypeScript · Rust
- **3D 渲染**：[Three.js](https://threejs.org/)
- **压缩引擎**：[draco_transcoder](https://github.com/google/draco) · [gltfpack / meshoptimizer](https://github.com/zeux/meshoptimizer)
- **纹理压缩**：[Basis Universal (basisu)](https://github.com/BinomialLLC/basis_universal)

---

## 🔗 相关链接

- 📖 [在线文档](https://zipoly.netlify.app) — 完整使用手册
- 🌐 [Web 在线版](https://zipoly-web.netlify.app) — 免费，无需安装
- 📦 [下载页面](https://github.com/raychart/zipoly/releases) — 历史版本下载
- 🐛 [问题反馈](https://github.com/raychart/zipoly/issues) — 提交 Bug 或建议
- 💬 微信公众号：**RayChart** — 购买授权与技术支持

---

## 📊 数据对比（真实案例）

| 模型类型 | 原始大小 | 优化后 | 压缩率 | 加载提速 |
|---------|---------|--------|--------|---------|
| 建筑可视化模型 | 128 MB | 18 MB | **-86%** | ↑ 7.1× |
| 电商产品展示 | 56 MB | 9 MB | **-84%** | ↑ 6.2× |
| PNG 纹理贴图 | 22 MB | 2.1 MB | **-90%** | ↑ 10.5× |
| 工业 CAD 模型 | 84 MB | 12 MB | **-86%** | ↑ 7× |

*以上数据使用默认参数（压缩级别 7）测试*

---

## 📄 开源协议 / 授权

**商业软件 / Commercial Software**

- ✅ 免费试用 6 小时
- 💰 完整授权最低 ¥29.9/年
- 📜 详见 [授权与定价](#-授权与定价)

---

## 🤝 参与贡献

本项目为闭源商业软件。如需报告问题或建议功能，请通过以下方式联系：

- 提交 [GitHub Issue](https://github.com/raychart/zipoly/issues)
- 关注微信公众号 **RayChart** 留言

---

<p align="center">
  <sub>由 <a href="https://github.com/raychart">RayChart</a> 用 ❤️ 打造</sub><br>
  <sub>© 2024–2026 RayChart. 保留所有权利。</sub>
</p>
