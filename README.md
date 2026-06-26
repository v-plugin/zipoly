# Zipoly — Web3D 模型体积优化工作台

> Draco + Meshopt 双引擎压缩 · KTX2 GPU 纹理 · 体检诊断 · 批量处理  
> 完全本地运行，数据不离开你的电脑

[![版本](https://img.shields.io/badge/版本-v2.0.1-6366f1)](https://gitee.com/raychart/zipoly/releases)
[![平台](https://img.shields.io/badge/平台-Windows%2010%2F11-blue)](https://gitee.com/raychart/zipoly/releases)
[![许可](https://img.shields.io/badge/授权-商业软件-orange)](#授权与定价)

---

## 简介

**Zipoly** 是一款面向前端开发者、3D 美术和设计师的桌面端工具，专注 Web3D 资产交付前的质检与优化。

- 几何体积最高缩减 **90%**（Draco / Meshopt 双引擎）
- 支持 **7 种格式**互转（GLB / FBX / OBJ / STL / DAE / PLY / glTF）
- KTX2 GPU 原生纹理，渲染零开销
- 完全离线，安装包约 **5 MB**

---

## 下载

**[⬇ 下载 Zipoly v2.0.0（Windows x64）](https://gitee.com/raychart/zipoly/releases)**

系统要求：Windows 10 / 11（64 位），4 GB 内存以上，无需联网。

> 没有 Windows 电脑？[Zipoly Web 在线版](https://zipoly-web.netlify.app) 无需安装，支持 Draco 压缩和格式转换，单文件限制 100 MB。

---

## 功能概览

| 功能模块 | 说明 | 授权 |
|----------|------|:----:|
| **压缩优化** | Draco / Meshopt 几何压缩，体积缩减 70–90%，支持场景化预设 | 试用 |
| **格式转换** | FBX / OBJ / STL / DAE / PLY → GLB / glTF，外部贴图自动内嵌 | 试用 |
| **纹理优化** | 独立图片文件压缩、缩放，支持输出 JPEG / WebP / KTX2 | 试用 |
| **3D 查看器** | Three.js 实时预览，时间光照模拟，自定义灯光，截图/录制 | **永久免费** |
| **操作日志** | 历史记录，支持参数复用和报告导出 | **永久免费** |
| **体检诊断** | 导入自动扫描，检出重复顶点、超规格纹理、缺失法线等问题 | 试用 |

---

## 压缩引擎对比

|  | Draco | Meshopt（推荐） |
|--|-------|----------------|
| 压缩率 | 高 | 更高 |
| 解码速度 | 快 | 快 5–10 倍 |
| 纹理压缩 | JPEG / WebP / KTX2 | BasisU（ETC1S / UASTC） |
| 框架支持 | Three.js / Babylon.js / model-viewer | Three.js（r136+） |
| 最适合 | 旧项目、广泛兼容 | 新项目、极致性能 |

> 不确定选哪个？选 Meshopt。Meshopt 不可用时软件自动降级到 Draco，不影响处理。

### 场景化预设（v2.0.0 新增）

内置四种一键预设，自动填充最优参数，无需手动调参：

| 预设 | 推荐引擎 | 适用场景 |
|------|---------|---------|
| 🌐 Web 3D 场景 | Meshopt | 网页端 3D 展示，平衡质量与加载速度 |
| 📱 移动端应用 | Meshopt | iOS/Android，极致压缩节省流量 |
| 🏭 工业可视化 | Draco | CAD 模型，保留高精度和节点结构 |
| 🛒 电商产品展示 | Meshopt | 3D 商品预览，高质量纹理 + 快速加载 |

---

## 快速上手

### 压缩一个模型

```
① 拖入 .glb / .gltf 文件
② 选择引擎（推荐 Meshopt）或选择场景预设
③ 调整压缩级别（默认 7，适合大多数场景）
④ 点击"开始优化"
⑤ 预览压缩结果，确认外观无误后保存
```

### 在 Three.js 中加载压缩后的模型

**Draco：**
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js'

const dracoLoader = new DRACOLoader()
dracoLoader.setDecoderPath('https://www.gstatic.com/draco/v1/decoders/')

const loader = new GLTFLoader()
loader.setDRACOLoader(dracoLoader)
loader.load('model_optimized.glb', gltf => scene.add(gltf.scene))
```

**Meshopt：**
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
ktx2Loader.setTranscoderPath('https://cdn.jsdelivr.net/npm/three/examples/jsm/libs/basis/')
ktx2Loader.detectSupport(renderer)

const loader = new GLTFLoader()
loader.setMeshoptDecoder(MeshoptDecoder)
loader.setKTX2Loader(ktx2Loader)
loader.load('model_optimized.glb', gltf => scene.add(gltf.scene))
```

> Babylon.js 和 model-viewer 内置 Draco 支持，直接加载即可，但不支持 Meshopt 格式。

---

## 压缩级别参考

| 级别 | 适用场景 |
|------|---------|
| 1–3 | 工程 / 医疗模型，精度优先 |
| 4–6 | 产品展示、建筑可视化 |
| **7（默认）** | **Web3D 通用，最佳起点** |
| 8–9 | 移动端、低带宽，可接受轻微失真 |
| 10 | 远景装饰，几何失真明显 |

---

## 支持的格式

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

## 授权与定价

首次安装自动获得 **6 小时完整试用**（累计时长，关闭软件后暂停计时）。

| 套餐 | 价格 |
|------|------|
| 1 年 | ¥29.9 |
| 2 年 | ¥49.9 |
| 3 年 | ¥68 |
| **终身** | **¥99** |

所有套餐包含全部功能，设备绑定离线验证，不自动续费。一机一码，不可跨设备使用。

**购买方式**：打开软件系统设置复制设备 ID，扫码关注微信公众号 **RayChart**，回复 `zipoly` 联系购买。

---

## 常见问题

**压缩后模型加载不出来？**  
需要配置解码器，详见上方[加载代码示例](#在-threejs-中加载压缩后的模型)。

**提示"该文件已经过 Draco 压缩"？**  
Draco 不支持重复压缩，请使用从建模软件导出的原始未压缩文件。

**压缩后文件反而变大了？**  
常见于面数极少（< 1000 面）或体积本身很小（< 100 KB）的模型，压缩元数据开销超过收益，可降低级别或不压缩。

**压缩后出现变形或锯齿？**  
降低压缩级别（如 9 → 7），或提高高级参数中的位置精度 qp（仅 Draco）。

**支持 Mac 或 Linux 吗？**  
目前仅支持 Windows 10/11（64 位），Mac/Linux 支持在路线图中。

---

## 更新日志

### v2.0.0（最新）
- 架构升级：引入统一压缩引擎接口，Draco / Meshopt 热插拔，降级机制完善
- 新增场景化压缩预设（Web / 移动 / 工业 / 电商）
- 新增智能引擎推荐（根据模型特征自动建议）
- Meshopt：支持网格简化、GPU Instancing、节点合并，实时分阶段进度
- KTX2：新增 UASTC 模式，质量参数精细化
- draco_transcoder 体积精简（6 MB → 2.5 MB）

### v1.0.2
- 集成 gltfpack（Meshopt 引擎），KTX2 纹理支持，纹理优化独立 Tab，体检诊断面板

### v1.0.1
- 时间光照模拟，自定义灯光，截图与视频录制，批量压缩暂停/继续/取消

### v1.0.0
- 首次发布：Draco 压缩、格式转换、纹理优化、3D 查看器、离线授权

→ [完整更新日志](https://zipoly.netlify.app/guide/changelog)

---

## 技术栈

- **桌面端**：[Tauri 2](https://v2.tauri.app/) · Vue 3 · TypeScript · Rust
- **3D 渲染**：[Three.js](https://threejs.org/)
- **压缩引擎**：[draco_transcoder](https://github.com/google/draco) · [gltfpack](https://github.com/zeux/meshoptimizer)
- **纹理压缩**：[Basis Universal (basisu)](https://github.com/BinomialLLC/basis_universal)

---

## 链接

- 📖 [在线文档](https://zipoly.netlify.app)
- 🌐 [Web 在线版](https://zipoly-web.netlify.app)

---

© 2024 RayChart. All rights reserved.
