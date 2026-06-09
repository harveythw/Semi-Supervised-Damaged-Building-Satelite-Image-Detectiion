Semi-Supervised CNN Transfer Learning for Post-Natural Disaster Management

Master of Data Science Research Project — Harvey Wong

Overview
This project develops a semi-supervised deep learning framework for detecting building damage from satellite imagery following hurricane events. The system assists disaster response teams in rapidly identifying and prioritising aid delivery locations without relying entirely on manually annotated data.
The key challenge: annotating satellite imagery post-disaster is time-consuming and resource-intensive. This work bridges supervised and unsupervised learning to reduce annotation dependency while maintaining strong detection accuracy.

Problem
After large-scale natural disasters, aid workers struggle to identify precise delivery locations due to:

Lack of reliable information-sharing systems
No decision-support analytics tools for rapid damage assessment
Traditional supervised models requiring large volumes of labelled data
Unsupervised approaches yielding lower precision and recall


Approach
A semi-supervised transfer learning pipeline combining two object detection architectures:
ModelBackboneMechanismFaster R-CNNResNet-50 / ResNet-101 / ResNeXt-101Two-stage: feature extraction → region proposal → classificationYOLOv9cCSP + GELANSingle-pass: grid-based bounding box regression + classification
Transfer Learning: Both models were pretrained on DOTA (~11k aerial images) before fine-tuning on hurricane damage datasets.
Semi-supervised strategy: Leverages a small labelled dataset alongside unlabelled imagery to reduce annotation burden while retaining model accuracy.

Dataset
Satellite imagery sourced from Maxar's Open Data Program:
DatasetLocationEventCoverageHurricane MariaSan Juan, Puerto RicoSept 2017328 km²Hurricane IanSouthwest FloridaSept 202243 km²

288 manually tiled and annotated images (512×512 pixels each)
861 damaged building annotations
2,278 undamaged building annotations


Results
Final Model: YOLOv9c
ModelmAP@50Training Time/EpochFaster R-CNN (ResNeXt-101)0.2113.1 minYOLOv9c0.262.8 min
Key findings:

YOLOv9c outperformed Faster R-CNN in both accuracy and training speed
Higher image resolution (720px) and larger batch sizes consistently improved mAP
Semi-supervised transfer learning reduced annotation requirements while maintaining competitive detection performance


Tech Stack

Deep Learning: PyTorch, Faster R-CNN, YOLOv8/v9 (Ultralytics)
Transfer Learning: DOTA pretrained weights
Data Processing: Python, NumPy, OpenCV
Annotation: Roboflow
Deployment: Roboflow API


Future Work

Integration of geolocation data for damage severity mapping and aid prioritisation
Expansion to additional disaster types (earthquakes, floods)
Cloud masking preprocessing using ArcGIS for cleaner imagery inputs


Context
This research was completed as part of a Master of Data Science programme. The work was supervised by Dr. Riyaz Ahamed Ariyaluran Habeeb.
