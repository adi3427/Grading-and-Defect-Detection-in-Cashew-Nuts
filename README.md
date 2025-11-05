### Automated Computer Vision System for Quality Grading and Defect Detection in Cashew Nuts
#### 1. Overview
This project proposes a deterministic, rule-based grading system using OpenCV to automate cashew nut quality inspection.It addresses the subjective and labor-intensive nature of manual grading.Unlike data-heavy Deep Learning models, this computationally lightweight framework avoids the "black-box" problem by using a fully understandable, rule-based scoring system.

#### 2. Objective
[cite_start]To develop a deterministic OpenCV pipeline that integrates multi-domain features (like Shape-from-Shading, Phase Congruency, and Gabor filters) and uses the Mahalanobis distance to provide an interpretable, real-time anomaly score for nut grading.

#### 3. 5-Stage Methodology
The pipeline processes an input RGB image to produce a final grade.

* **Stage 1: Preprocessing:**
    * Convert to CIE Lab* color space.
    * Apply Multi-Scale Retinex (MSRCR) for illumination normalization.
    * Use a non-local means filter for denoising.

* **Stage 2: Segmentation:**
    * Apply Otsu's adaptive thresholding to the L* channel.
    * Use morphological operations to clean the mask and extract the main nut contour].

* **Stage 3: Multi-Domain Feature Extraction:**
    * **Morphological:** Hu Moments, Solidity, Aspect Ratio.
    * **Texture & Frequency:** Phase Congruency, Local Phase Quantization (LPQ), and Gabor filters.
    * **Surface Geometry:** Shape-from-Shading (SFS) to find dents/bumps.
    * **Photometric:** Color statistics from a* and b* channels for discoloration.

* **Stage 4: Statistical Scoring:**
    * A "good" nut profile is created by calculating a mean vector ($\mu$) and covariance matrix ($\Sigma$) from defect-free samples.
    * A new nut's anomaly score is its squared Mahalanobis distance ($D_M^2$) from this "good" profile.
    * $D_M^2 = (x - \mu)^T \Sigma^{-1} (x - \mu)$ 

* **Stage 5: Classification:**
    * The final $D_M^2$ score is compared to preset thresholds to classify the nut (e.g., "Good," "Minor Defect," "Reject") .
