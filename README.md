# Semi-Supervised CNN Transfer Learning for Post-Natural Disaster Management

> Master of Data Science Research Project — Tun Hao Wong

## Overview

This project develops a semi-supervised deep learning framework for detecting building damage from satellite imagery following hurricane events. The system assists disaster response teams in rapidly identifying and prioritising aid delivery locations without relying entirely on manually annotated data.

The key challenge: annotating satellite imagery post-disaster is time-consuming and resource-intensive. This work bridges supervised and unsupervised learning to reduce annotation dependency while maintaining strong detection accuracy.

---

## Problem

After large-scale natural disasters, aid workers struggle to identify precise delivery locations due to:
- Lack of reliable information-sharing systems
- No decision-support analytics tools for rapid damage assessment
- Traditional supervised models requiring large volumes of labelled data
- Unsupervised approaches yielding lower precision and recall

---

## Approach

A semi-supervised transfer learning pipeline combining two object detection architectures:

| Model | Backbone | Mechanism |
|---|---|---|
| **Faster R-CNN** | ResNet-50 / ResNet-101 / ResNeXt-101 | Two-stage: feature extraction → region proposal → classification |
| **YOLOv9c** | CSP + GELAN | Single-pass: grid-based bounding box regression + classification |

**Transfer Learning:** Both models were pretrained on [DOTA](https://arxiv.org/abs/1711.10398) (~11k aerial images) before fine-tuning on hurricane damage datasets.

**Semi-supervised strategy:** Leverages a small labelled dataset alongside unlabelled imagery to reduce annotation burden while retaining model accuracy.

---

## Dataset

Satellite imagery sourced from [Maxar's Open Data Program](https://www.maxar.com/open-data):

| Dataset | Location | Event | Coverage |
|---|---|---|---|
| Hurricane Maria | San Juan, Puerto Rico | Sept 2017 | 328 km² |
| Hurricane Ian | Southwest Florida | Sept 2022 | 43 km² |

- 288 manually tiled and annotated images (512×512 pixels each)
- 861 damaged building annotations
- 2,278 undamaged building annotations

---

## Results

**Final Model: YOLOv9c**

| Model | mAP@50 | Training Time/Epoch |
|---|---|---|
| Faster R-CNN (ResNeXt-101) | 0.21 | 13.1 min |
| **YOLOv9c** | **0.26** | **2.8 min** |

Key findings:
- YOLOv9c outperformed Faster R-CNN in both accuracy and training speed
- Higher image resolution (720px) and larger batch sizes consistently improved mAP
- Semi-supervised transfer learning reduced annotation requirements while maintaining competitive detection performance

---

## Tech Stack

- **Deep Learning:** PyTorch, Faster R-CNN, YOLOv8/v9 (Ultralytics)
- **Transfer Learning:** DOTA pretrained weights
- **Data Processing:** Python, NumPy, OpenCV
- **Annotation:** Roboflow
- **Deployment:** Roboflow API

---

## Future Work

- Integration of geolocation data for damage severity mapping and aid prioritisation
- Expansion to additional disaster types (earthquakes, floods)
- Cloud masking preprocessing using ArcGIS for cleaner imagery inputs

---

## Context

This research was completed as part of a Master of Data Science programme. The work was supervised by Dr. Riyaz Ahamed Ariyaluran Habeeb.

