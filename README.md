# ARM_Hackathon_PS3_Shreya_Gouri
Real-time road anomaly detection system using YOLO deployed on Raspberry Pi with ARM-optimized NCNN inference. Developed for the ARM Bharat AI-SoC Student Challenge (Problem Statement 3).

# 🚀 Road Anomaly Detection using Raspberry Pi (ARM AI-SoC Deployment)
## 📌 ARM Bharat AI-SoC Student Challenge
**Problem Statement 3:** Detect Road Anomalies using Raspberry Pi and Dashcam

Developed by:
* **Shreya Upadhyay**
* **Gouri Vast**
  Cambridge Institute of Technology

# 📖 Project Overview

This project implements a real-time road anomaly detection system using a YOLO-based deep learning model deployed on a Raspberry Pi. The objective was to detect road damages such as potholes and surface anomalies using a dashcam setup under ARM-based hardware constraints.

Two deployment strategies were explored:

1. **Method 1:** ONNX Runtime-based inference
2. **Method 2:** NCNN-based inference (Final Implementation)

After comparative evaluation, the NCNN deployment method was selected as the optimized solution for ARM-based edge inference.

# 🧠 System Architecture

Camera → Frame Preprocessing → Model Inference → Multi-Layer Filtering → Detection Output

### Key Components:

* Raspberry Pi (2GB RAM)
* PiCamera2
* YOLO-based object detection model
* NCNN inference framework (final implementation)

# ⚙️ Methods Implemented
## 🟡 Method 1: ONNX Runtime Deployment

### Workflow:

* Train YOLO model (.pt)
* Export to ONNX (.onnx)
* Deploy using ONNX Runtime
* Perform CPU-only inference

### Observations:

* FPS often below 5
* Higher runtime overhead
* Moderate bounding box stability
* Functional but not optimal for ARM

## 🟢 Method 2: NCNN Deployment (Final)

### Workflow:

* Train YOLO model (.pt)
* Export to NCNN (.param + .bin)
* Deploy using NCNN on Raspberry Pi
* ARM-optimized inference execution

### Improvements:

* Higher FPS
* Reduced latency
* Better bounding box stability
* Lower dependency stack
* Improved ARM CPU utilization

# 📊 Optimization Techniques

### Frame-Level Optimization

* Resolution scaling
* Buffer control
* Single batch inference
* Camera warm-up stabilization

### Model-Level Optimization

* Confidence threshold tuning
* Non-Maximum Suppression
* Lightweight YOLO variant
* Reduced inference input size

### Multi-Layer False Detection Reduction

1. Confidence filtering
2. Class filtering
3. Bounding box area validation
4. NMS
5. Frame-to-frame consistency check

# 🧪 Performance Summary

| Parameter              | ONNX          | NCNN            |
| ---------------------- | ------------- | --------------- |
| CPU Only               | Yes           | Yes             |
| FPS                    | <5 (unstable) | Higher & Stable |
| ARM Optimization       | Limited       | Optimized       |
| Bounding Box Stability | Moderate      | Improved        |
| Deployment Complexity  | Moderate      | Streamlined     |
| Final Selection        | Baseline      | ✅ Final         |

Detailed training metrics are provided in `results.csv`.
Runtime logs and detection outputs are included in the repository.

# 💻 Hardware Used

* Raspberry Pi (2GB RAM)
* ARM Cortex-based processor
* PiCamera2
* CPU-only inference

### Hardware Limitation Observed:

* 2GB RAM limited heavy model deployment
* CPU-only inference constrained FPS
* ≥4GB RAM recommended for improved performance

# 📂 Repository Structure
├── train/
│   ├── training_script.py
│   └── results.csv
│
├── onnx_method/
│   ├── export_to_onnx.py
│   └── onnx_inference.py
│
├── ncnn_method/
│   ├── export_to_ncnn.py
│   └── ncnn_inference.py
│
├── detected_images/
│
├── logs/
│
└── README.md

# 🔧 Installation Guide

## Common Dependencies
pip install ultralytics opencv-python numpy

## For ONNX Method
pip install onnx onnxruntime picamera2

## For NCNN Method (Final)
pip install ultralytics ncnn picamera2

# ▶️ Running the Detection Script (NCNN)

python ncnn_inference.py --model best.param --confidence 0.4 --imgsz 416

Arguments supported:

* `--confidence`
* `--imgsz`
* `--model`
* `--output`

# 🔔 Future Scope

* Integrate buzzer alert via GPIO
* Add LCD/OLED display for driver warnings
* Deploy on ≥4GB RAM hardware
* Integrate GPS-based anomaly mapping
* Upgrade to NPU-enabled ARM boards

# 📚 References

* EjElectronics.io
* Rohit Suresh (RAD Dataset) - https://www.kaggle.com/datasets/rohitsuresh15/radroad-anomaly-detection
* Raspberry Pi Documentation
* Ultralytics YOLO Documentation
* NCNN Framework Documentation
* ONNX Runtime Documentation

Hardware components were procured from the Electronics Department of Cambridge Institute of Technology.

The model was tested and validated under the guidance of
**Dr. Douglas Anthony Louis Pirya Kumar (Dean R&D)**

# ✅ Final Outcome

Problem Statement 3 — Real-time detection of road anomalies using Raspberry Pi and dashcam — has been successfully executed and implemented using NCNN-based optimized deployment.
