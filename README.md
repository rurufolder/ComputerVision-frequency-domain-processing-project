# Frequency‑Domain vs Spatial‑Domain Image Filtering: A Comparative Study

## 1. Overview

This repository contains a Python implementation that compares **frequency‑domain** and **spatial‑domain** filtering techniques for image processing. The project evaluates three common filtering tasks:

- **Noise reduction** using Low‑Pass Filters (LPF) in the frequency domain versus Gaussian blur in the spatial domain.  
- **Edge enhancement** using High‑Pass Filters (HPF).  
- **Texture isolation** using Band‑Pass Filters (BPF).

Performance is assessed quantitatively using **Peak Signal‑to‑Noise Ratio (PSNR)** and **Structural Similarity Index (SSIM)**.

---

## 2. Objectives

- Demonstrate the theoretical and practical differences between frequency‑domain and spatial‑domain filtering.  
- Provide a reusable codebase for applying custom frequency masks (low‑pass, high‑pass, band‑pass) to any grayscale image.  
- Compare the effectiveness of a frequency‑domain LPF against a spatial Gaussian blur for Gaussian noise removal.  
- Visualise the magnitude and phase spectra of input images.

---

## 3. Methodology

### 3.1 Dataset

Three grayscale images are used as test cases:

| Filename        | Description          |
|----------------|----------------------|
| `urban.jpg`     | Urban streetscape    |
| `forset.jpg`    | Forest landscape     |
| `flowers.jpg`   | Flower close‑up      |

All images are loaded using OpenCV and converted to grayscale if necessary.

### 3.2 Filter Design

- **Low‑Pass Filter** – circular mask keeping low frequencies (center of the spectrum).  
- **High‑Pass Filter** – complementary mask that removes low frequencies.  
- **Band‑Pass Filter** – annular mask that retains a specific ring of frequencies.

The masks are applied in the frequency domain after performing a 2D Fast Fourier Transform (FFT) and shifting the zero‑frequency component to the centre.

### 3.3 Noise Model

Additive white Gaussian noise with zero mean and standard deviation of 20 is added to each image to simulate a noisy input.

### 3.4 Evaluation Metrics

- **PSNR (dB)** – measures pixel‑wise reconstruction error. Higher values indicate better quality.  
- **SSIM** – measures structural similarity between the filtered image and the original ground truth. Values range from 0 to 1, with 1 indicating perfect similarity.

---

## 4. Implementation Details

### 4.1 Requirements

The code requires Python 3.7+ and the following libraries:

- `opencv-python`
- `numpy`
- `matplotlib`

Installation:

```bash
pip install opencv-python numpy matplotlib
```

### 4.2 File Structure

```
.
├── CV_Final.py          # Main script
├── urban.jpg            # Example image (user‑provided)
├── forset.jpg           # Example image (user‑provided)
├── flowers.jpg          # Example image (user‑provided)
└── README.md            # Project documentation
```

### 4.3 Usage

1. Update the `image_files` dictionary in the script with the correct paths to your images.  
2. Run the script:

```bash
python CV_Final.py
```

3. The script will sequentially:
   - Load and display each image.  
   - Show the magnitude and phase spectra.  
   - Add Gaussian noise, then denoise using both frequency‑domain LPF and spatial Gaussian blur.  
   - Output PSNR and SSIM for both methods.  
   - Display the original, noisy, denoised, and ground‑truth images.  
   - Compute and display edge‑enhanced (HPF) and texture‑isolated (BPF) results.

---

## 5. Results Summary

For each image, the script prints quantitative metrics. Typical observations:

- The frequency‑domain LPF consistently achieves **higher PSNR and SSIM** than the spatial Gaussian blur when the noise is Gaussian.  
- The high‑pass filter effectively extracts edges, producing an image that highlights contours and fine details.  
- The band‑pass filter isolates mid‑frequency components, revealing texture patterns that are not visible in either the original or the edge‑only output.

*Example output for the urban image:*

```
Processing Urban...
  [Denoising] Freq LPF PSNR: 28.34 dB, SSIM: 0.9123
  [Denoising] Spatial PSNR:  26.71 dB, SSIM: 0.8901
```

---

## 6. Visualisation Examples

The script generates the following plots for each image:

- Magnitude spectrum (log scale) and phase spectrum.  
- Side‑by‑side comparison of noisy input, LPF‑denoised output, Gaussian‑denoised output, and ground truth.  
- Comparison of original, edge‑enhanced, and texture‑isolated outputs.

These visualisations help illustrate the practical effects of each filtering technique.

---

## 7. Conclusions

This project confirms that frequency‑domain filtering, when appropriately designed, can outperform simple spatial filters for certain tasks such as Gaussian noise reduction. The flexibility to design arbitrary masks (low‑pass, high‑pass, band‑pass) makes the frequency domain a powerful tool for image analysis. However, spatial filters remain computationally simpler and are often sufficient for real‑time applications with modest requirements.

The code is modular and can be easily extended to include additional filters, metrics, or colour image processing.

---


---
## Implemented by
Reema AlFayez & Shatha Alghamdi - DS473 course project at Saudi Electronic University
