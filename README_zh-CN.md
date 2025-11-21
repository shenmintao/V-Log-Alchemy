# 🧪 V-Log Alchemy (Lumix Body Snatcher)

> **Turn your Panasonic Lumix camera into a Fujifilm GFX, Leica, ARRI, and more using precise ACES inverse engineering.**
>
> 通过精确的 ACES 逆向工程，将松下 Lumix 相机（S1R II/S5M2 等）的色彩科学“数学级”转换为富士 GFX、徕卡、ARRI 等顶级电影机/中画幅风格。

---

## 📖 简介 (Introduction)

本项目旨在通过数学手段，打破相机品牌的“色彩壁垒”。

许多相机厂商（如 Fujifilm, Leica）拥有极具特色的色彩科学（Color Science），但它们的官方 LUT 通常只接受自家相机的 Log 输入。本项目通过 **ACES (Academy Color Encoding System)** 流程进行逆向工程：

1.  将 Panasonic **V-Log/V-Gamut** 转换到标准的 **ACES AP0 (Linear)**。
2.  使用自定义编写的 **DCTL (DaVinci Color Transform Language)** 或高精度转换矩阵，执行目标相机 IDT (Input Device Transform) 的**逆运算**。
3.  将信号伪装成目标相机的原生 Log/Gamut（如 F-Log2C, Leica Log）。
4.  应用目标厂商的官方色彩 LUT。

最终生成的 `.cube` 文件可直接导入松下相机（如 S1R II, S1H, S5系列）进行机内实时监看，或在后期流程中使用。

---

## 📂 文件列表与风格说明 (LUT Pack Content)

本仓库提供的 LUT 专为 **Panasonic V-Log / V-Gamut** 输入设计。

### 🗻 Fujifilm GFX Series (F-Log2C Core)
*基于富士中画幅色彩科学，高像素机型（如 S1R II）的绝配。*

*   **`FLog2C_to_REALA-ACE_VLog.cube`**
    *   **风格**: Reala Ace (GFX100 II 首发)。
    *   **特点**: 色彩还原极其精准，硬朗且通透，非常适合风景、建筑和高解析力拍摄。
*   **`FLog2C_to_CLASSIC-CHROME_VLog.cube`**
    *   **风格**: Classic Chrome (经典正片)。
    *   **特点**: 低饱和度，强对比度，模仿老式纪实杂志风格。
*   **`FLog2C_to_CLASSIC-Neg._VLog.cube`**
    *   **风格**: Classic Neg (经典负片)。
    *   **特点**: 街拍神级色彩，高对比，红橘色偏暖，强调硬调。
*   **`FLog2C_to_PROVIA_VLog.cube`**
    *   **风格**: Provia (标准)。
    *   **特点**: 标准、万能、肤色自然。
*   **`FLog2C_to_Velvia_VLog.cube`**
    *   **风格**: Velvia (鲜艳)。
    *   **特点**: 极高饱和度，风景专用。
*   **`FLog2C_to_ASTIA_VLog.cube`**
    *   **风格**: Astia (柔和)。
    *   **特点**: 柔和的肤色表现，适合人像。
*   **`FLog2C_to_ETERNA_VLog.cube`**
    *   **风格**: Eterna (电影)。
    *   **特点**: 超低对比度，柔和的高光滚降，适合视频基底。
*   **`FLog2C_to_ETERNA-BB_VLog.cube`**
    *   **风格**: Eterna Bleach Bypass (跳漂)。
    *   **特点**: 低饱和，极高对比，冷峻金属感。
*   **`FLog2C_to_PRO-Neg.Std_VLog.cube`**
    *   **风格**: Pro Neg. Std。
    *   **特点**: 影棚人像标准，细腻平滑。
*   **`FLog2C_to_ACROS_VLog.cube`**
    *   **风格**: Acros。
    *   **特点**: 质感极佳的黑白模式，有着独特的中灰影调。

### 🔧 基础转换 (Technical)
*   **`FLog2C_to_FLog2C-709_VLog.cube`**
    *   **风格**: Rec.709 Tech Transform。
    *   **特点**: 纯技术转换，将 F-Log2C 还原为标准 Rec.709，不带任何胶片风格。
*   **`FLog2C_to_WDR_VLog.cube`**
    *   **风格**: Wide Dynamic Range (宽动态范围)。
    *   **特点**: 富士特色的视频直出曲线。比标准 Rec.709 保留更多高光和阴影细节，反差适中，色彩自然，适合快速出片或直播。

---

### 🔴 Leica (L-Log Core)
*基于 Leica SL/Q 系列色彩科学，提供极具辨识度的“德味”厚重感。*

*   **`L-Log_to_Classic_VLog.cube`**
    *   **风格**: Leica Classic (经典)。
    *   **特点**: 标志性的“徕卡味”。高微反差 (Micro-contrast)，深沉的暗部，锐利且略带冷调的阴影，暖调的高光。非常适合黑白摄影预视或强调质感的纪实摄影。
*   **`L-Log_to_Natural_VLog.cube`**
    *   **风格**: Leica Natural (自然)。
    *   **特点**: 相比 Classic 更加现代和中性。保留了徕卡的高光滚降特性，但暗部细节更多，对比度更温和，色彩过渡非常平滑“高级”，适合时尚、人像或日常记录。

---

### 🎬 ARRI (LogC Core)
*基于 ARRI Alexa 电影机的色彩科学，提供行业标准的电影感。*

*   **`ARRI_LogC2Video_Classic709_VLog.cube`**
    *   **风格**: ARRI Classic 709。
    *   **特点**: 经典的 ARRI Rec.709 外观，被无数电影和电视剧使用。色彩真实，肤色表现出色，高光过渡自然。

---

### 🎞️ Film Emulation (Cineon Core)
*基于柯达 Cineon 扫描系统，模拟经典电影胶片的色彩。*

*   **`Cineon_to_Fuji_3513DI_D65_VLog.cube`**
    *   **风格**: Fuji 3513DI Print Film。
    *   **特点**: 模拟富士电影发行拷贝的色彩，具有标志性的青色和柔和的对比度。
*   **`Cineon_to_Kodak_2383_D65_VLog.cube`**
    *   **风格**: Kodak 2383 Print Film。
    *   **特点**: 模拟柯达电影发行拷贝的色彩，是好莱坞大片的标准外观，色彩温暖，对比度较高。

---

### 🎥 RED Digital Cinema (RED IPP2 Core)
*基于 RED 数字电影机的 IPP2 图像处理流程。*

*   **`REC709_MEDIUM_CONTRAST_Soft_VLog.cube`**
    *   **风格**: RED IPP2 Medium Contrast / Soft Highlight。
    *   **特点**: RED 官方 Rec.709 转换之一，提供中等对比度和柔和的高光滚降，适合各种场景。

---

## 🛠️ 使用方法 (Usage)

### 📷 方案 A：机内监看 (In-Camera)
适用于 Panasonic S1R II, S5M2, S1H 等支持加载 LUT 的机型。
1. 下载 `Luts` 文件夹中的 `.cube` 文件（推荐使用 33-Point 版本以兼容相机性能）。
2. 将文件复制到 SD 卡。
3. 在相机菜单中加载 LUT 并应用到 V-Log 监看（V-Log View Assist）。

### 🎨 方案 B：DaVinci Resolve 工作流 (Post-Production)
为了获得最高画质（避免 LUT 带来的精度损失），建议在达芬奇中使用 DCTL 脚本。(请注意：DCTL 功能为达芬奇 Studio 付费版独占功能)。

**节点结构：**
1.  **CST Node**: Panasonic V-Gamut/V-Log -> ACES AP0 / Linear。**重要提示**：请关闭此节点的 **Tone Mapping (色调映射)** 和 **White Point Adaptation (白点自适应)**。
2.  **DCTL Node**: 加载本项目提供的 `ACES_to_FLog2C_Inverse.dctl`。
3.  **LUT Node**: 加载富士官方 F-Log2C 胶片模拟 LUT。

---

## 🧮 核心算法 (The Math)

本项目的核心在于精确的逆运算矩阵。以 **ACES AP0 to F-Log2C** 为例，我们计算了富士官方 IDT 的逆矩阵：

```c
// ACES AP0 (Linear) to F-Gamut (Linear) Inverse Matrix
// Calculated based on Fujifilm F-Log2C official IDT v1.00
{
     1.18805632080277f, -0.0526707998586238f, -0.135385520944148f,
     0.000717966415014435f, 0.987967895093181f, 0.0113141384918043f,
     0.0095814146658757f, 0.00504068380666559f, 0.985377901527459f,
};
```

详细的 DCTL 代码请查看 `DCTL` 文件夹。

---

## ⚠️ 注意事项 (Disclaimer)
1. **物理限制**：虽然我们在数学上对齐了色彩空间，但不同传感器的 CFA (色彩滤镜阵列) 光谱响应特性不同。所谓的“同色异谱”现象意味着在某些极端光源下（如霓虹灯），松下的表现可能仍与原机有细微差异。
2. **曝光策略**：由于转换后的曲线特性（特别是 F-Log2C），建议拍摄时向右曝光 (ETTR) 0.5~1 档，以获得更干净的暗部。
3. **非官方**：本项目与 Panasonic, Fujifilm, Leica 无官方关联。