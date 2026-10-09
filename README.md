# LIRSRN: A Lightweight Infrared Image Super-Resolution Network

[![IEEE Xplore](https://img.shields.io/badge/IEEE%20Xplore-10558676-00629B.svg)](https://ieeexplore.ieee.org/document/10558676)
[![Conference](https://img.shields.io/badge/IEEE%20ISCAS-2024-B31B1B.svg)](https://iscas2024.it/)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Repository-181717.svg?logo=github)](https://github.com/julian135707/LIRSRN-A-Lightweight-Infrared-Image-Super-Resolution-Network)
[![Framework](https://img.shields.io/badge/PyTorch-%E2%89%A51.10-EE4C2C.svg?logo=pytorch)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

Official PyTorch implementation of the paper:  
**"LIRSRN: A Lightweight Infrared Image Super-Resolution Network"**  
*Chun-An Lin, Tsung-Jung Liu, and Kuan-Hsien Liu*  
Presented at **IEEE International Symposium on Circuits and Systems (ISCAS 2024)**  
[Paper on IEEE Xplore](https://ieeexplore.ieee.org/document/10558676) | [Original Release](https://reurl.cc/yYDnA6)

---

## 📌 News
- **[2024]** 🎉 LIRSRN was presented at **IEEE ISCAS 2024**, Singapore.
- **[2024]** 📄 The paper is publicly accessible on [IEEE Xplore](https://ieeexplore.ieee.org/document/10558676).
- **[2024]** 🚀 Training and evaluation codes along with pretrained weights are released.

---

## 📖 Introduction

Infrared (IR) imaging is crucial for applications such as night vision, thermal tracking, and environmental monitoring. However, IR images typically suffer from low spatial resolution, low contrast, and blurriness compared to visible light imaging. 

**LIRSRN** is a specialized, computationally efficient super-resolution architecture tailored to infrared imagery:
- **Attention Enhancement Module (AEM)**: Integrates **Pixel Self-Attention (PSA)**, **Brightness-Texture Attention (BTA)**, and **Spatial Attention (SA)** to emphasize critical gradient and structural representations across spatial and channel domains.
- **Spatial Frequency Block (SFB)**: Combines spatial convolution with 2D Fast Fourier Transform (FFT) and Fast Fourier Convolution (FFC) to extract both spatial features and frequency-domain texture characteristics.
- **Efficient Reconstruction**: Employs Depthwise Separable Convolutions (DSC) and residual connections to reconstruct sharp high-resolution details with minimal parameter overhead (only **117.32K** parameters).
- **Grayscale Optimization**: Designed natively for single-channel (1-channel) infrared processing, avoiding unnecessary multi-channel overhead while achieving higher accuracy.

---

## 📊 Benchmark Results

### Quantitative Comparisons
Quantitative evaluation against state-of-the-art super-resolution methods on `results-A` and `results-C` benchmark datasets (22 images each). Values represent **PSNR (dB) / SSIM**.

| Test Dataset | Scale | SRMD | EDSR | ESRGAN | DPSR | SPSR | IMDN | PSRGAN | **LIRSRN (Ours)** |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **results-A** | x2 | 23.21 / 0.4193 | 31.94 / 0.8106 | 32.37 / 0.8822 | 37.01 / 0.9303 | 36.41 / 0.8961 | 37.16 / 0.9343 | 37.48 / 0.9229 | **38.45 / 0.9321** |
| **results-A** | x4 | 11.90 / 0.2860 | 27.89 / 0.7076 | 28.06 / 0.7537 | 32.45 / 0.8181 | 32.46 / 0.7839 | 32.56 / 0.8239 | 33.13 / 0.8282 | **34.39 / 0.8290** |
| **results-C** | x2 | 22.92 / 0.7605 | 32.46 / 0.8294 | 33.31 / 0.8991 | 37.91 / 0.9425 | 37.23 / 0.9129 | 38.06 / 0.9465 | 38.52 / 0.9363 | **38.86 / 0.9432** |
| **results-C** | x4 | 12.52 / 0.4193 | 28.41 / 0.7332 | 29.03 / 0.7818 | 33.12 / 0.8377 | 33.14 / 0.8056 | 33.20 / 0.8435 | 33.86 / 0.8466 | **34.97 / 0.8395** |

### Efficiency & Attention Mechanism Ablation Study

Trade-offs between different attention combinations in LIRSRN:
- **P**: Pixel Self-Attention
- **B**: Brightness-Texture Attention
- **S**: Spatial Attention
- **C**: Channel Attention

| Configuration | Parameters | FLOPs | results-A (x2) | results-A (x4) | results-C (x2) | results-C (x4) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **P + B + S (Full)** | **117.32K** | **9.01G** | **38.45 / 0.9321** | **34.39 / 0.8290** | **38.86 / 0.9432** | **34.97 / 0.8395** |
| B + S | 70.76K | 5.37G | 37.33 / 0.9172 | 33.74 / 0.8161 | 38.08 / 0.9310 | 34.26 / 0.8362 |
| C + S | 25.90K | 5.89G | 36.29 / 0.9179 | 33.73 / 0.8162 | 37.03 / 0.9305 | 34.25 / 0.8363 |
| S (Ultra-light) | **10.95K** | **3.48G** | 38.40 / 0.9213 | 34.31 / 0.8179 | 38.75 / 0.9342 | 34.87 / 0.8384 |

### Single-Channel vs. Three-Channel Input Comparison
On single-channel infrared grayscale images, single-channel processing reduces parameter count by **77.2%** while delivering superior reconstruction metrics:
- **1-Channel Input**: 25.90K Parameters, 5.89G FLOPs (PSNR: 38.86 dB @ results-C x2)
- **3-Channel Input**: 113.83K Parameters, 8.63G FLOPs (PSNR: 36.97 dB @ results-C x2)

---

## 🛠️ Environment Setup

```bash
# Clone repository
git clone [https://github.com/julian135707/LIRSRN-A-Lightweight-Infrared-Image-Super-Resolution-Network.git](https://github.com/julian135707/LIRSRN-A-Lightweight-Infrared-Image-Super-Resolution-Network.git)
cd LIRSRN-A-Lightweight-Infrared-Image-Super-Resolution-Network

# Create conda environment
conda create -n lirsrn python=3.9 -y
conda activate lirsrn

# Install PyTorch (adjust CUDA version to match your environment)
pip install torch torchvision --extra-index-url [https://download.pytorch.org/whl/cu118](https://download.pytorch.org/whl/cu118)

# Install dependencies
pip install -r requirements.txt
