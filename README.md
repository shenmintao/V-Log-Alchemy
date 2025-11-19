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

## 📦 包含的风格 (Included Looks)

### 1. FUJIFILM GFX Series (Based on F-Log2C)
利用富士中画幅 GFX 系列的色彩科学。
*   **Nostalgic Neg (怀旧负片)**: 温暖的高光，青色的阴影，极具辨识度。
*   **Classic Chrome (经典正片)**: 低饱和，强对比，纪实风格。
*   **Reala Ace**: 富士最新的色彩，色彩还原精准且硬朗。

### 2. Leica (L-Log)
*   **Leica Classic**: 德味厚重，高对比度，深沉的暗部。
*   **Leica Vivid**: 更鲜艳生动，适合风光。

### 3. Coming Soon...
*   **ARRI Alexa (K1S1)**: 电影工业标准。
*   **Kodak 2383**: 胶片印片模拟。

---

## 🛠️ 使用方法 (Usage)

### 📷 方案 A：机内监看 (In-Camera)
适用于 Panasonic S1R II, S5M2, S1H 等支持加载 LUT 的机型。
1. 下载 `Luts` 文件夹中的 `.cube` 文件（推荐使用 33-Point 版本以兼容相机性能）。
2. 将文件复制到 SD 卡。
3. 在相机菜单中加载 LUT 并应用到 V-Log 监看（V-Log View Assist）。

### 🎨 方案 B：DaVinci Resolve 工作流 (Post-Production)
为了获得最高画质（避免 LUT 带来的精度损失），建议在达芬奇中使用 DCTL 脚本。

**节点结构：**
1.  **CST Node**: Panasonic V-Gamut/V-Log -> ACES AP0 / Linear (No Tone Mapping).
2.  **DCTL Node**: 加载本项目提供的 `ACES_to_FLog2C_Inverse.dctl`。
3.  **LUT Node**: 加载富士官方 F-Log2C 胶片模拟 LUT。

---

## 🧮 核心算法 (The Math)

本项目的核心在于精确的逆运算矩阵。以 **ACES AP0 to F-Log2C** 为例，我们计算了富士官方 IDT 的逆矩阵：

```c
// ACES AP0 (Linear) to F-Gamut (Linear) Inverse Matrix
// Calculated based on Fujifilm F-Log2C official IDT v1.00
{
     1.18953639f, -0.05277977f, -0.13553403f,
     0.00071857f,  0.98909229f,  0.01132693f,
     0.00959302f,  0.00494250f,  0.98650739f
}
```

详细的 DCTL 代码请查看 DCTL 文件夹。

---

## ⚠️ 注意事项 (Disclaimer)
1. **物理限制**：虽然我们在数学上对齐了色彩空间，但不同传感器的 CFA (色彩滤镜阵列) 光谱响应特性不同。所谓的“同色异谱”现象意味着在某些极端光源下（如霓虹灯），松下的表现可能仍与原机有细微差异。
2. **曝光策略**：由于转换后的曲线特性（特别是 F-Log2C），建议拍摄时向右曝光 (ETTR) 0.5~1 档，以获得更干净的暗部。
3. **非官方**：本项目与 Panasonic, Fujifilm, Leica 无官方关联。

