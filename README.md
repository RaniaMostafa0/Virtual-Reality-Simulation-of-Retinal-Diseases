# Through the Eye: VR Simulation of Retinal Diseases for Educational Purposes

**A standalone Virtual Reality application that simulates the real-time visual symptoms of 12 retinal diseases, built with Unity and OpenCV for medical education, accessibility design, and public awareness.**

[![Paper]([https://img.shields.io/badge/Paper-IEEE%20NILES%202025-blue](https://ieeexplore.ieee.org/document/11232445))]()

---

## Overview

**Through the Eye** is a VR platform that recreates the first-person visual experience of patients living with retinal disease. Rather than relying on static diagrams or textbook descriptions, users put on a Meta Quest 2 headset and *see* the world the way someone with Retinitis Pigmentosa, AMD, or Choroideremia does — in real time, with adjustable severity, and grounded in clinically documented symptomatology.

The system was developed as a Senior Project at **Nile University** and published at **IEEE NILES 2025**.

---

## Why This Exists

Over a billion people worldwide live with some form of visual impairment. Existing tools like **NEI VR** and **OpenVisSim** cover a narrow slice of conditions (5 or fewer) and are often research toolkits requiring Unity/coding knowledge to operate. **Through the Eye** closes that gap with:

- **12 disease simulations** in one standalone app (vs. 5 for NEI VR)
- **Real-time severity control** via in-VR sliders — no code, no editor
- **No coding knowledge required** to use the final application
- A **modular architecture** that lets each disease be developed, tuned, and extended independently

---

## Diseases Simulated

| Category | Conditions |
|---|---|
| **Retinal degeneration** | Retinitis Pigmentosa (RP), Age-Related Macular Degeneration (AMD), Stargardt Disease, Choroideremia |
| **Macular / vascular** | Macular Pucker, Central Serous Chorioretinopathy (CSCR), Hypertensive Retinopathy, Pathologic Myopia |
| **Lens opacities (cataracts)** | Nuclear Cataract, Cortical Cataract, Traumatic Cataract, Posterior Subcapsular Cataract |

Each condition is modeled from clinical descriptions in **EyeWiki (AAO)**, **Webvision (University of Utah)**, and **Kanski's Clinical Ophthalmology**, and supports a **severity slider** to simulate progression from early to advanced-stage symptoms.

---

## How It Works
Live Video Capture  →  Image Processing  →  VR Integration  →  User Interaction
(External Webcam)     (Disease Filters)   (Rendered in Unity)  (Selection & severity control)

1. An **external HD webcam**, mounted on the Meta Quest 2, captures a full-color video feed (the Quest 2's native passthrough is grayscale-only).
2. The feed streams to a connected PC where **OpenCV (via OpenCVForUnity)** applies disease-specific filters in real time.
3. Processed frames are rendered inside **Unity** and displayed back to the headset over **Oculus Link**.
4. A VR GUI lets the user pick a disease and drag a severity slider to see it progress.

### Simulation Techniques

| Symptom | Technique |
|---|---|
| Blurring | Gaussian blur |
| Distortion | Sinusoidal pixel warping |
| Micropsia | Central region shrinking |
| Central Vision Loss | Center masking (scotoma) |
| Black Spots | Randomized patch masking |
| Contrast Reduction | Linear alpha/beta scaling |
| Tunnel Vision | Radial grayscale masking |
| Night Blindness | Brightness-adaptive dimming |
| Yellowish Tint | Blue-channel reduction |
| Hazy Overlays | Blur + white overlay blending |
| Glare | Bright-region detection + Gaussian halo |

Full mathematical formulations for each effect are in the [published paper](#).

---

## System Requirements

**Hardware**
- Meta Quest 2 headset (Oculus Link cable or Air Link)
- External HD webcam (head-mounted, for full-color passthrough)
- Windows 10+ PC, quad-core CPU (e.g., Intel i5 / Ryzen 5, 8 threads)
- 16 GB RAM
- VR-ready dedicated GPU (e.g., NVIDIA RTX 3050 or better)

**Software**
- Unity **2023.x**
- [OpenCVForUnity](https://assetstore.unity.com/packages/tools/integration/opencv-for-unity-21088) plugin *(Asset Store — not redistributed in this repo; you'll need your own license to open the project)*
- Oculus/Meta Quest Link software

---

## Repository Structure
├── AMD/                          # Age-Related Macular Degeneration simulation
├── Cataracts/                    # Nuclear, Cortical, Traumatic, Posterior Subcapsular
├── Central Serous Chorioretinopathy/
├── Choroideremia/
├── Diseases in Unity C#/         # Core C# disease scripts
├── Diseases with Slider/         # Severity-slider-enabled variants
├── Edge Detection/
├── Extras/
├── Hypertensive Retinopathy/
├── Image Enhancement/            # Cataract visual-aid enhancement pipeline
├── Macular Pucker/
├── Pathologic Myopia/
├── Retinitis Pigmentosa/
├── Stargardt/
└── README.md

---

## Evaluation

- **43 participants** tested the full system; average performance of **23 FPS** during live simulation, rated acceptable for educational use.
- A **visual enhancement pipeline** (unsharp masking, blue-channel boosting, CLAHE, gamma correction) was tested on cataract simulations with 32 participants — **69% reported noticeable clarity improvement**.
- Non-clinical study with lay volunteers; informed consent obtained, no formal IRB required.

| Feature | Through the Eye | OpenVisSim | NEI VR |
|---|---|---|---|
| Platform | Standalone desktop app | Unity toolkit (dev-only) | Precompiled demo |
| Disease coverage | 12 | General impairments | 5 |
| Severity control | Real-time slider | Code/editor only | Not supported |
| Ease of use | No coding needed | Requires Unity knowledge | Easy but limited |

---
