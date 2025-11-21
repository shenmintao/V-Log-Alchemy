# 🧪 V-Log Alchemy (Lumix Body Snatcher)

[**中文版 (Chinese Version)**](./README_zh-CN.md)

> **Turn your Panasonic Lumix camera into a Fujifilm GFX, Leica, ARRI, and more using precise ACES inverse engineering.**

---

## 📖 Introduction

This project aims to break the "color barrier" between camera brands through mathematical means.

Many camera manufacturers (like Fujifilm, Leica) have distinctive color science, but their official LUTs typically only accept Log input from their own cameras. This project reverse-engineers this process using the **ACES (Academy Color Encoding System)** workflow:

1.  Convert Panasonic **V-Log/V-Gamut** to the standard **ACES AP0 (Linear)**.
2.  Use custom-written **DCTL (DaVinci Color Transform Language)** or high-precision matrices to perform the **inverse operation** of the target camera's IDT (Input Device Transform).
3.  Disguise the signal as the target camera's native Log/Gamut (e.g., F-Log2C, Leica Log).
4.  Apply the target manufacturer's official color LUT.

The resulting `.cube` files can be directly loaded into Panasonic cameras (like S1R II, S1H, S5 series) for real-time in-camera monitoring or used in post-production.

---

## 📂 LUT Pack Content

The LUTs in this repository are designed exclusively for **Panasonic V-Log / V-Gamut** input.

### 🗻 Fujifilm GFX Series (F-Log2C Core)
*Based on Fujifilm's medium format color science, a perfect match for high-resolution cameras like the S1R II.*

*   **`FLog2C_to_REALA-ACE_VLog.cube`**
    *   **Style**: Reala Ace (debuted with GFX100 II).
    *   **Features**: Extremely accurate color reproduction, sharp and clear. Ideal for landscapes, architecture, and high-resolution work.
*   **`FLog2C_to_CLASSIC-CHROME_VLog.cube`**
    *   **Style**: Classic Chrome.
    *   **Features**: Low saturation, high contrast, mimicking the style of old documentary magazines.
*   **`FLog2C_to_CLASSIC-Neg._VLog.cube`**
    *   **Style**: Classic Neg.
    *   **Features**: The ultimate street photography look. High contrast with warm red-orange tones, emphasizing a hard-edged look.
*   **`FLog2C_to_PROVIA_VLog.cube`**
    *   **Style**: Provia (Standard).
    *   **Features**: Standard, versatile, with natural skin tones.
*   **`FLog2C_to_Velvia_VLog.cube`**
    *   **Style**: Velvia (Vivid).
    *   **Features**: Extremely high saturation, specialized for landscapes.
*   **`FLog2C_to_ASTIA_VLog.cube`**
    *   **Style**: Astia (Soft).
    *   **Features**: Soft skin tone rendering, suitable for portraits.
*   **`FLog2C_to_ETERNA_VLog.cube`**
    *   **Style**: Eterna (Cinema).
    *   **Features**: Ultra-low contrast with a soft highlight roll-off, perfect as a video base layer.
*   **`FLog2C_to_ETERNA-BB_VLog.cube`**
    *   **Style**: Eterna Bleach Bypass.
    *   **Features**: Low saturation, extremely high contrast, with a cool, metallic feel.
*   **`FLog2C_to_PRO-Neg.Std_VLog.cube`**
    *   **Style**: Pro Neg. Std.
    *   **Features**: The standard for studio portraits, delivering fine and smooth tones.
*   **`FLog2C_to_ACROS_VLog.cube`**
    *   **Style**: Acros.
    *   **Features**: A high-texture black and white mode with a unique mid-gray tonality.

### 🔧 Technical
*   **`FLog2C_to_FLog2C-709_VLog.cube`**
    *   **Style**: Rec.709 Tech Transform.
    *   **Features**: A pure technical conversion from F-Log2C to standard Rec.709 without any film styling.
*   **`FLog2C_to_WDR_VLog.cube`**
    *   **Style**: Wide Dynamic Range.
    *   **Features**: Fujifilm's characteristic curve for video out-of-camera. Retains more highlight and shadow detail than standard Rec.709, with moderate contrast and natural colors. Ideal for quick turnarounds or live streaming.

---

### 🔴 Leica (L-Log Core)
*Based on the color science of the Leica SL/Q series, delivering the distinctively rich 'Leica look'.*

*   **`L-Log_to_Classic_VLog.cube`**
    *   **Style**: Leica Classic.
    *   **Features**: The signature 'Leica look'. High micro-contrast, deep blacks, sharp and slightly cool shadows, with warm highlights. Excellent for B&W preview or high-texture documentary photography.
*   **`L-Log_to_Natural_VLog.cube`**
    *   **Style**: Leica Natural.
    *   **Features**: More modern and neutral compared to Classic. Retains Leica's highlight roll-off but with more shadow detail, milder contrast, and exceptionally smooth, 'premium' color transitions. Suitable for fashion, portraits, or daily shooting.

---

### 🎬 ARRI (LogC Core)
*Based on the color science of the ARRI Alexa, providing the industry-standard cinematic feel.*

*   **`ARRI_LogC2Video_Classic709_VLog.cube`**
    *   **Style**: ARRI Classic 709.
    *   **Features**: The classic ARRI Rec.709 look, used in countless films and TV shows. Features true-to-life colors, excellent skin tone reproduction, and a natural highlight roll-off.

---

### 🎞️ Film Emulation (Cineon Core)
*Based on the Kodak Cineon scanning system, emulating the colors of classic motion picture film.*

*   **`Cineon_to_Fuji_3513DI_D65_VLog.cube`**
    *   **Style**: Fuji 3513DI Print Film.
    *   **Features**: Emulates the look of Fujifilm motion picture print stock, with its signature cyans and soft contrast.
*   **`Cineon_to_Kodak_2383_D65_VLog.cube`**
    *   **Style**: Kodak 2383 Print Film.
    *   **Features**: Emulates the look of Kodak motion picture print stock, the standard for Hollywood blockbusters, featuring warm colors and higher contrast.

---

### 🎥 RED Digital Cinema (RED IPP2 Core)
*Based on the IPP2 image processing pipeline from RED Digital Cinema cameras.*

*   **`REC709_MEDIUM_CONTRAST_Soft_VLog.cube`**
    *   **Style**: RED IPP2 Medium Contrast / Soft Highlight.
    *   **Features**: One of RED's official Rec.709 conversions, offering medium contrast with a soft highlight roll-off, suitable for a wide range of scenes.

---

## 🛠️ Usage

### 📷 Method A: In-Camera Monitoring
For Panasonic models that support LUT loading, such as S1R II, S5M2, S1H.
1. Download the `.cube` files from the `Luts` folder.
2. Copy the files to an SD card.
3. Load the LUT in the camera menu and apply it to V-Log View Assist.

### 🎨 Method B: DaVinci Resolve Workflow
For maximum image quality (to avoid precision loss from LUTs), using the DCTL script in DaVinci Resolve is recommended. (Please note: DCTL is a feature exclusive to the paid DaVinci Resolve Studio version).

**Node Structure:**
1.  **CST Node**: Panasonic V-Gamut/V-Log -> ACES AP0 / Linear. **Important**: In the CST node settings, disable **Tone Mapping** and **White Point Adaptation**.
2.  **DCTL Node**: Load the `ACES_to_FLog2C_Inverse.dctl` script provided in this project.
3.  **LUT Node**: Apply the official Fujifilm F-Log2C film simulation LUT.

---

## 🧮 The Math

The core of this project is a precise inverse matrix. Taking **ACES AP0 to F-Log2C** as an example, we calculated the inverse of Fujifilm's official IDT matrix:

```c
// ACES AP0 (Linear) to F-Gamut (Linear) Inverse Matrix
// Calculated based on Fujifilm F-Log2C official IDT v1.00
{
     1.18805632080277f, -0.0526707998586238f, -0.135385520944148f,
     0.000717966415014435f, 0.987967895093181f, 0.0113141384918043f,
     0.0095814146658757f, 0.00504068380666559f, 0.985377901527459f,
};
```

For detailed DCTL code, please see the `DCTL` folder.

---

## ⚠️ Disclaimer
1. **Physical Limitations**: While we have mathematically aligned the color spaces, the spectral response of different sensor CFAs (Color Filter Arrays) varies. This phenomenon, known as metamerism, means that under certain extreme lighting conditions (e.g., neon lights), the Panasonic's rendering may still have subtle differences from the original camera.
2. **Exposure Strategy**: Due to the characteristics of the transformed curve (especially F-Log2C), it is recommended to Expose to the Right (ETTR) by 0.5 to 1 stop during shooting to achieve cleaner shadows.
3. **Unofficial**: This project is not officially affiliated with Panasonic, Fujifilm, or Leica.
