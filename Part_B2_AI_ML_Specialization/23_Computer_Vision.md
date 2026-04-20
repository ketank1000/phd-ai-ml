# 23. Computer Vision

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 23.1 Image Processing Basics

### 23.1.1 Digital Image Fundamentals

An image is a 2D function $f(x, y)$ where $(x, y)$ are spatial coordinates and $f$ gives the intensity.

| Concept | Description |
|---------|-------------|
| **Pixel** | Smallest unit of a digital image |
| **Resolution** | Number of pixels (e.g., 1920×1080) |
| **Grayscale** | Single channel, values 0 (black) to 255 (white) |
| **Color (RGB)** | 3 channels (Red, Green, Blue), each 0-255 |
| **Depth** | 8-bit (0-255), 16-bit, 32-bit float |

**Color spaces:**

| Space | Description | Use Case |
|-------|-------------|----------|
| **RGB** | Red, Green, Blue | Display, default |
| **HSV** | Hue, Saturation, Value | Color-based segmentation |
| **LAB** | Lightness, A (green-red), B (blue-yellow) | Perceptually uniform |
| **YCbCr** | Luminance + Chrominance | Video compression |

### 23.1.2 Image Filtering

**Convolution with kernels** (same operation as in CNNs, but hand-designed):

**Gaussian Blur** (smoothing):
$$G(x,y) = \frac{1}{2\pi\sigma^2} e^{-\frac{x^2+y^2}{2\sigma^2}}$$

Kernel example (3×3 approximation):
```
  1/16 × [1  2  1]
          [2  4  2]
          [1  2  1]
```

**Edge detection kernels:**

| Operator | Detects | Kernel |
|----------|---------|--------|
| **Sobel-X** | Vertical edges | $\begin{bmatrix}-1&0&1\\-2&0&2\\-1&0&1\end{bmatrix}$ |
| **Sobel-Y** | Horizontal edges | $\begin{bmatrix}-1&-2&-1\\0&0&0\\1&2&1\end{bmatrix}$ |
| **Laplacian** | All edges (2nd derivative) | $\begin{bmatrix}0&1&0\\1&-4&1\\0&1&0\end{bmatrix}$ |

**Canny Edge Detector** (multi-stage, most widely used):
1. Gaussian blur (noise reduction)
2. Gradient magnitude and direction (Sobel)
3. Non-maximum suppression (thin edges to 1 pixel)
4. Double thresholding and edge tracking by hysteresis

### 23.1.3 Morphological Operations

Work on binary images. Use a **structuring element** (kernel):

| Operation | Effect | Use |
|-----------|--------|-----|
| **Erosion** | Shrinks white regions, removes small noise | Clean up small objects |
| **Dilation** | Expands white regions, fills small holes | Connect nearby regions |
| **Opening** | Erosion → Dilation | Remove small noise while preserving shape |
| **Closing** | Dilation → Erosion | Fill small holes while preserving shape |

### 23.1.4 Other Operations

| Operation | Description |
|-----------|-------------|
| **Histogram Equalization** | Spread intensity values evenly → improve contrast |
| **Otsu's Thresholding** | Automatically find optimal threshold for binarization |
| **Affine Transform** | Rotation, scaling, translation, shearing |
| **Perspective Transform** | Map quadrilateral to rectangle (document scanning) |

---

## 23.2 Feature Extraction (Classical Methods)

Before deep learning, hand-crafted features were essential:

| Method | Description | Key Properties |
|--------|-------------|---------------|
| **SIFT** | Detect keypoints at multiple scales, compute 128-dim descriptor | Scale/rotation invariant |
| **SURF** | Faster SIFT using integral images + Hessian matrix | Faster, slightly less accurate |
| **HOG** | Histogram of gradient orientations in cells → concatenate | Pedestrian/object detection |
| **ORB** | Fast keypoint detector (FAST) + binary descriptor (BRIEF) | Open-source, real-time |
| **Harris Corner** | Detect corners using eigenvalues of gradient matrix | Simple, effective |

**HOG (Histogram of Oriented Gradients) — Used in pedestrian detection:**
1. Compute gradients at each pixel
2. Divide image into cells (e.g., 8×8 pixels)
3. For each cell, bin gradient orientations into a histogram
4. Normalize histograms across blocks of cells
5. Concatenate all blocks → feature vector

---

## 23.3 Deep Learning for Computer Vision

### 23.3.1 Image Classification

**Task:** Input: image → Output: class label (with confidence)

Evolution covered in Chapter 21 (LeNet → AlexNet → VGG → ResNet → EfficientNet).

**Data augmentation** (critical for vision):
- Random crop, horizontal flip, rotation
- Color jitter, brightness/contrast adjustment
- Cutout, Mixup, CutMix (modern techniques)
- RandAugment, AutoAugment (learned augmentation policies)

### 23.3.2 Object Detection

**Task:** Input: image → Output: bounding boxes + class labels for all objects.

```
  ┌───────────────────────────────┐
  │        ┌───────┐              │
  │        │  CAT  │  ┌────────┐  │
  │        │ 0.95  │  │  DOG   │  │
  │        └───────┘  │  0.87  │  │
  │                   └────────┘  │
  └───────────────────────────────┘
```

**Two-stage detectors** (accurate, slower):

| Model | Key Innovation |
|-------|---------------|
| **R-CNN** (2014) | Extract ~2000 region proposals (selective search), classify each with CNN |
| **Fast R-CNN** (2015) | Run CNN once on whole image, use ROI pooling to extract features |
| **Faster R-CNN** (2015) | Replace selective search with learned **Region Proposal Network (RPN)** |

**One-stage detectors** (fast, suitable for real-time):

| Model | Key Innovation |
|-------|---------------|
| **YOLO** (2016) | Divide image into grid, predict boxes+classes in one pass. Real-time. |
| **SSD** (2016) | Multi-scale feature maps for detecting objects of different sizes |
| **RetinaNet** (2017) | **Focal Loss** — addresses class imbalance (background >> objects) |
| **YOLOv8** (2023) | State-of-the-art real-time detection, anchor-free |

**YOLO concept:**
1. Divide image into $S \times S$ grid
2. Each cell predicts $B$ bounding boxes (x, y, w, h, confidence)
3. Each cell predicts class probabilities
4. Single forward pass → all predictions at once

**Non-Maximum Suppression (NMS):** After detection, multiple overlapping boxes may detect the same object. NMS keeps only the highest-confidence box and removes overlapping ones (IoU > threshold).

### 23.3.3 Semantic Segmentation

**Task:** Classify every pixel in the image.

```
Input Image          Segmented Output
┌──────────┐         ┌──────────┐
│ 🌳  🏠  │         │ GGG HHH  │  G=Green(tree)
│ 🌳  🏠  │   →     │ GGG HHH  │  H=House
│ 🌍  🛣️ │         │ EEE RRR  │  E=Earth, R=Road
└──────────┘         └──────────┘
```

| Architecture | Key Idea |
|-------------|----------|
| **FCN** (2015) | Replace FC layers with 1×1 conv, upsample to input size |
| **U-Net** (2015) | Encoder-decoder with **skip connections** at each level (medical imaging) |
| **DeepLab** (v1-v3+) | **Atrous (dilated) convolution** — larger receptive field without losing resolution |
| **PSPNet** | Pyramid Pooling Module — captures multi-scale context |

**U-Net Architecture (most popular for medical imaging):**

```
  Input → [Conv Conv] ──────────────────────────→ [Concat Conv Conv] → Output
             ↓                                        ↑
           [Pool]                                   [UpConv]
             ↓                                        ↑
         [Conv Conv] ──────────────────────→ [Concat Conv Conv]
             ↓                                        ↑
           [Pool]                                   [UpConv]
             ↓                                        ↑
         [Conv Conv] ──→ Bottleneck ──→ [Conv Conv]
  
  Encoder (downsampling)         Decoder (upsampling)
  ←── Skip connections connect encoder to decoder ──→
```

**Atrous/Dilated Convolution:** Insert zeros between kernel elements → larger receptive field without increasing parameters or reducing resolution.

### 23.3.4 Instance Segmentation

**Task:** Detect individual objects AND segment each one separately (combines detection + segmentation).

**Mask R-CNN** (2017): Extends Faster R-CNN by adding a **mask branch** that predicts a binary mask for each detected object. Three outputs per detection: class, bounding box, pixel mask.

### 23.3.5 Image Generation and Style Transfer

| Method | Description |
|--------|-------------|
| **Neural Style Transfer** | Combine content of one image with style of another using CNN features |
| **GANs** | Generate realistic images (Chapter 21.6) |
| **Diffusion Models** | State-of-the-art image generation (DALL-E 2, Stable Diffusion) |
| **ViT (Vision Transformer)** | Apply Transformer to image patches instead of CNN |

---

## 23.4 Evaluation Metrics for Computer Vision

### IoU (Intersection over Union)

$$\text{IoU} = \frac{\text{Area of Overlap}}{\text{Area of Union}}$$

```
  ┌───────────┐
  │  Predicted │
  │    ┌───────┼──────┐
  │    │ INTER │      │
  └────┼───────┘      │
       │   Ground Truth│
       └──────────────┘

  IoU = INTER / (Predicted + GT - INTER)
```

- IoU > 0.5: correct detection (AP@0.5)
- IoU > 0.75: strict criterion (AP@0.75)

### mAP (mean Average Precision)

1. For each class: compute precision at different recall levels → average (AP)
2. mAP = mean of AP across all classes

**COCO metric:** mAP@[0.5:0.95] — average over IoU thresholds from 0.5 to 0.95 in steps of 0.05.

### Segmentation Metrics

| Metric | Formula | Description |
|--------|---------|-------------|
| **Pixel Accuracy** | Correct pixels / Total pixels | Simple but misleading if classes imbalanced |
| **Mean IoU (mIoU)** | Average IoU across all classes | Standard metric for segmentation |
| **Dice Coefficient** | $\frac{2|A \cap B|}{|A| + |B|}$ | Similar to F1, used in medical imaging |

---

## 23.5 Practice Questions

**Q1.** Explain the difference between semantic segmentation, instance segmentation, and object detection.
> **Answer:** **Object detection** draws bounding boxes around objects and classifies them — doesn't segment pixels. **Semantic segmentation** classifies every pixel into a class but doesn't distinguish between instances (two cats in same image are both "cat" pixels). **Instance segmentation** does both — classifies every pixel AND distinguishes individual objects (cat-1 pixels vs. cat-2 pixels). Example: In a photo with 3 people — detection gives 3 boxes, semantic segmentation colors all "person" pixels the same, instance segmentation gives each person a different color. Mask R-CNN does instance segmentation.

**Q2.** Compare one-stage (YOLO) and two-stage (Faster R-CNN) object detectors.
> **Answer:** **Two-stage (Faster R-CNN):** Stage 1: Region Proposal Network generates ~300 candidate boxes. Stage 2: Classify and refine each proposal. **Pros:** Higher accuracy, better for small objects. **Cons:** Slower (~5 FPS). **One-stage (YOLO):** Single network predicts all boxes and classes in one pass by dividing image into grid cells. **Pros:** Real-time speed (30-60+ FPS), simple architecture. **Cons:** Lower accuracy on small/overlapping objects (improving with each version). **Choose Faster R-CNN** for medical imaging, satellite imagery (accuracy critical). **Choose YOLO** for autonomous driving, video surveillance (speed critical).

**Q3.** How does the Canny edge detector work? Why is it preferred over simple Sobel operators?
> **Answer:** Canny is a multi-stage algorithm: (1) **Gaussian blur** removes noise; (2) **Sobel gradient** computes edge magnitude and direction; (3) **Non-maximum suppression** thins edges to 1-pixel width by keeping only local maxima along gradient direction; (4) **Hysteresis thresholding** with two thresholds — strong edges (above high threshold) are kept, weak edges (between thresholds) are kept only if connected to strong edges. **Better than Sobel** because: Sobel only computes gradients (thick, noisy edges), while Canny adds noise reduction, edge thinning, and intelligent thresholding — producing clean, thin, connected edges.

**Q4.** Explain U-Net architecture. Why are skip connections important in segmentation?
> **Answer:** U-Net has an **encoder** (contracting path: Conv+Pool to capture context) and a **decoder** (expanding path: UpConv to recover spatial resolution). **Skip connections** concatenate encoder feature maps with decoder feature maps at each corresponding level. **Why critical:** During downsampling/pooling, fine spatial information (exact edge locations) is lost. Skip connections pass this high-resolution information directly to the decoder, enabling precise pixel-level segmentation. Without them, the decoder would produce blurry, imprecise boundaries. This is especially important in medical imaging where precise boundaries (tumor edges) are critical.

**Q5.** What is IoU and mAP? Why is mAP@[0.5:0.95] used in COCO evaluation?
> **Answer:** **IoU** = Area of intersection / Area of union between predicted and ground-truth boxes. Higher IoU = better localization. **mAP** = mean Average Precision across all classes. For each class, compute precision-recall curve at a given IoU threshold, calculate area under curve (AP), then average across classes. **mAP@0.5** (PASCAL VOC): considers a detection correct if IoU ≥ 0.5 — lenient. **mAP@[0.5:0.95]** (COCO): averages mAP at IoU thresholds 0.5, 0.55, ..., 0.95 — much stricter, rewards precise localization. This prevents models from getting high scores with sloppy bounding boxes.

---

*Previous: [Chapter 22 — NLP](22_NLP.md) | Next: [Chapter 24 — Reinforcement Learning](24_Reinforcement_Learning.md)*
