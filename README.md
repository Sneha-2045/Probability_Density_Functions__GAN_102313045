# Probability_Density_Functions__GAN_102313045
# Learning Probability Density Function using GAN

## Overview
This project aims to learn an unknown probability density function (PDF) of a transformed variable using a Generative Adversarial Network (GAN). The model is trained only on data samples without assuming any predefined distribution.

---

## Dataset
- Dataset: India Air Quality Data  
- Feature used: NO₂ concentration (`no2`)  
- Missing values were removed before processing  

---

## Data Transformation
Each value `x` is transformed into `z` using:

z = x + a_r * sin(b_r * x)

Where:
- a_r = 0.5 × (r mod 7)
- b_r = 0.3 × ((r mod 5) + 1)
- r = YOUR ROLL NUMBER

Example:
- a_r = ______
- b_r = ______

This transformation introduces non-linearity into the dataset.

---

## GAN Methodology

### Generator
- Input: Random noise ~ N(0,1)
- Architecture:
  - Linear (1 → 32) + ReLU
  - Linear (32 → 64) + ReLU
  - Linear (64 → 1)
- Output: Fake samples (z_f)

### Discriminator
- Input: Real and fake samples
- Architecture:
  - Linear (1 → 64) + ReLU
  - Linear (64 → 32) + ReLU
  - Linear (32 → 1) + Sigmoid
- Output: Probability of sample being real

### Training Process
- Loss Function: Binary Cross Entropy (BCE)
- Optimizer: Adam
- Batch size: 64
- Epochs: 1500
- Generator tries to fool discriminator
- Discriminator tries to distinguish real vs fake

---

##  PDF Estimation
After training:
- Generated 5000 samples using generator
- Estimated PDF using Kernel Density Estimation (KDE)

---

##  Result Graph

Two plots were generated:

1. KDE Plot 
   - Shows smooth probability density curves
   - Comparison between real and generated data
   - <img width="693" height="469" alt="Screenshot 2026-02-26 at 10 57 18 PM" src="https://github.com/user-attachments/assets/b881aeba-c60e-496c-b2e5-2a6806015521" />


2. Histogram Plot (gan_histogram.png)
   - Shows frequency distribution
   - Real vs generated comparison
<img width="674" height="448" alt="Screenshot 2026-02-26 at 10 57 41 PM" src="https://github.com/user-attachments/assets/cf686f04-0de6-43ef-b7d3-7a510e1955ea" />

---

##  Observations

### Mode Coverage
The GAN successfully captured the major peaks (modes) of the distribution. Minor deviations exist in less frequent regions.

### Training Stability
Training showed stable convergence after initial fluctuations. No major instability or divergence was observed.

### Quality of Generated Distribution
The generated data closely matches the real data distribution. KDE plots show strong alignment, indicating successful learning of the PDF.

---

##  Conclusion
The GAN successfully learned the underlying probability density function of the transformed variable without prior assumptions. The generated samples closely resemble the original data distribution.

---
