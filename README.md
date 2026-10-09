# LIRSRN: A Lightweight Infrared Image Super-Resolution Network

[![IEEE Xplore](https://img.shields.io/badge/IEEE%20Xplore-10558676-00629B.svg)](https://ieeexplore.ieee.org/document/10558676)
[![Conference](https://img.shields.io/badge/IEEE%20ISCAS-2024-B31B1B.svg)](https://iscas2024.it/)
[![Framework](https://img.shields.io/badge/PyTorch-%E2%89%A51.10-EE4C2C.svg)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

Official PyTorch implementation of the paper:  
**"LIRSRN: A Lightweight Infrared Image Super-Resolution Network"** (IEEE ISCAS 2024)  
*Chun-An Lin, Tsung-Jung Liu, and Kuan-Hsien Liu*

---

## 📌 News
- **[2024-05]** 🚀 LIRSRN was presented at **IEEE ISCAS 2024**.
- **[2024-05]** 📄 Paper is publicly accessible on [IEEE Xplore](https://ieeexplore.ieee.org/document/10558676).
- **[2024-05]** 💻 Code and pretrained weights released!

---

## 📖 Introduction

Infrared (IR) image super-resolution plays a critical role in surveillance, night vision, and remote sensing. However, standard deep super-resolution models often suffer from high computational complexity and parameter overhead, making deployment on edge infrared sensor devices challenging.

**LIRSRN** introduces an efficient, lightweight architecture tailored to the unique spatial and gradient distributions of thermal/infrared images:
- **Low Computational Budget**: Drastically reduces parameter count and FLOPs while preserving edge sharpness.
- **Tailored Feature Extraction**: Effectively addresses low-contrast, noisy, and blurred characteristics inherent to infrared imagery.
- **Superior Trade-off**: Outperforms existing lightweight SR benchmarks in both objective quality (PSNR/SSIM) and hardware latency.

<p align="center">
  <img src="assets/framework.png" width="90%" alt="LIRSRN Architecture"/>
</p>

---

## 🛠️ Environment Setup

```bash
# Clone the repository
git clone [https://github.com/your-username/LIRSRN.git](https://github.com/your-username/LIRSRN.git)
cd LIRSRN

# Create conda environment
conda create -n lirsrn python=3.9 -y
conda activate lirsrn

# Install dependencies
pip install -r requirements.txt
```

---

## 📂 Dataset Preparation

Organize your infrared training and testing datasets as follows:

```text
datasets/
├── Thermal_Train/
│   ├── HR/
│   └── LR_bicubic/ (or generated on-the-fly)
│       └── X2/ X3/ X4/
└── Thermal_Test/
    ├── Set5_IR/
    ├── CVC-09/
    └── FLIR/
```

---

## 🏋️ Pretrained Models

You can download the pretrained weights from the table below and place them in the `./weights/` folder:

| Model Scale | Params (M) | FLOPs (G) | Download Link |
| :---: | :---: | :---: | :---: |
| LIRSRN (x2) | ~0.xx | ~xx.x | [Google Drive / Release](#) |
| LIRSRN (x3) | ~0.xx | ~xx.x | [Google Drive / Release](#) |
| LIRSRN (x4) | ~0.xx | ~xx.x | [Google Drive / Release](#) |

---

## ⚡ Quick Start

### 1. Evaluation / Testing
To test the model on benchmark datasets using pretrained weights:

```bash
# Scale x4 evaluation
python test.py \
  --scale 4 \
  --model_path weights/lirsrn_x4.pth \
  --test_dir datasets/Thermal_Test/FLIR \
  --save_dir results/FLIR_x4
```

### 2. Training
To train LIRSRN from scratch:

```bash
# Train on x4 scale
python train.py \
  --scale 4 \
  --batch_size 16 \
  --patch_size 192 \
  --lr 5e-4 \
  --train_dir datasets/Thermal_Train \
  --val_dir datasets/Thermal_Test
```

---

## 📊 Benchmark Results

Quantitative evaluation on standard infrared image datasets:

| Scale | Method | FLOPs (G) | Params (K) | PSNR (dB) | SSIM |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **x4** | Bicubic | - | - | 28.xx | 0.81xx |
| **x4** | SRCNN | 52.7 | 57 | 30.xx | 0.85xx |
| **x4** | FSRCNN | 6.0 | 12 | 30.xx | 0.86xx |
| **x4** | **LIRSRN (Ours)** | **X.X** | **XX** | **31.xx** | **0.88xx** |

<p align="center">
  <img src="assets/visual_comparison.png" width="90%" alt="Visual Comparison"/>
</p>

---

## 📝 Citation

If this work, code, or dataset contributes to your research or project, please consider citing our paper:

### BibTeX
```bibtex
@inproceedings{lin2024lirsrn,
  title={Lirsrn: A lightweight infrared image super-resolution network},
  author={Lin, Chun-An and Liu, Tsung-Jung and Liu, Kuan-Hsien},
  booktitle={2024 IEEE International Symposium on Circuits and Systems (ISCAS)},
  pages={1--5},
  year={2024},
  organization={IEEE},
  doi={10.1109/ISCAS58748.2024.10558676}
}
```

### APA
```text
Lin, C. A., Liu, T. J., & Liu, K. H. (2024, May). Lirsrn: A lightweight infrared image super-resolution network. In 2024 IEEE International Symposium on Circuits and Systems (ISCAS) (pp. 1-5). IEEE.
```

---

## 🤝 Acknowledgements & Contact

This project is built upon insights from standard super-resolution frameworks. We thank the open-source community for their valuable contributions.

For any inquiries or feedback regarding this work, please open an issue in this repository or contact the authors.

---

## 📜 License
This project is licensed under the [Apache License 2.0](LICENSE).
