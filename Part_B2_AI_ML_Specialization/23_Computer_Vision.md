# 23. Computer Vision

> **Part B2 — AI/ML Specialization** | SIU PET Study Guide

---

## 23.1 Image Processing Basics

- [ ] **Digital Image Fundamentals**
  - Pixel, resolution, channels (RGB, grayscale)
  - Color spaces: RGB, HSV, LAB

- [ ] **Image Operations**
  - Filtering: Gaussian blur, median filter, sharpening
  - Edge detection: Sobel, Canny, Laplacian
  - Morphological operations: erosion, dilation, opening, closing
  - Histogram equalization, thresholding (Otsu's method)

## 23.2 Feature Extraction (Classical)

- [ ] **SIFT** (Scale-Invariant Feature Transform): Keypoint detection + descriptor
- [ ] **SURF** (Speeded Up Robust Features): Faster version of SIFT
- [ ] **HOG** (Histogram of Oriented Gradients): Used for pedestrian detection
- [ ] **ORB**: Open-source alternative to SIFT/SURF

## 23.3 Deep Learning for Computer Vision

- [ ] **Image Classification**: CNN architectures (see Section 21.3)

- [ ] **Object Detection**

  | Model | Type | Key Feature |
  |-------|------|-------------|
  | **R-CNN** | Two-stage | Region proposals + CNN |
  | **Fast R-CNN** | Two-stage | ROI pooling |
  | **Faster R-CNN** | Two-stage | Region Proposal Network (RPN) |
  | **YOLO** (v1-v8) | One-stage | Real-time, single pass |
  | **SSD** | One-stage | Multi-scale feature maps |
  | **RetinaNet** | One-stage | Focal loss for class imbalance |

- [ ] **Semantic Segmentation**: Classify each pixel
  - FCN (Fully Convolutional Networks)
  - U-Net (encoder-decoder with skip connections)
  - DeepLab (atrous/dilated convolution)

- [ ] **Instance Segmentation**: Detect + segment individual objects
  - Mask R-CNN

- [ ] **Image Generation**
  - GANs (see Section 21.6)
  - Style transfer: Neural style transfer
  - Diffusion models

- [ ] **Evaluation Metrics**
  - IoU (Intersection over Union)
  - mAP (mean Average Precision)
  - Pixel accuracy, Dice coefficient

---

### Recommended Resources
- **Book**: *Digital Image Processing* — Gonzalez & Woods
- **Book**: *Computer Vision: Algorithms and Applications* — Szeliski (free online)
- **Course**: CS231N — Convolutional Neural Networks (Stanford)
