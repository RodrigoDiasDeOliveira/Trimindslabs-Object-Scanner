# 📦 Triminds ObjectScanner

![Platform](https://img.shields.io/badge/Triminds-Platform-blue)
![Computer Vision](https://img.shields.io/badge/AI-Computer%20Vision-success)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-red)
![Android](https://img.shields.io/badge/Android-Native-brightgreen)
![Python](https://img.shields.io/badge/Python-Flask-blue)
![Oracle](https://img.shields.io/badge/Oracle-Database-red)
![License](https://img.shields.io/badge/License-MIT-yellow)


![detector](https://github.com/user-attachments/assets/37645298-c6ae-4051-8510-b6c02c6d69dc)



## Enterprise Computer Vision Platform for Warehouse Automation

**Triminds ObjectScanner** is an enterprise-grade AI-powered computer vision solution designed to identify, classify and count warehouse assets using standard Android devices.

Instead of relying on expensive specialized hardware, users can scan pallets, boxes, labels, QR Codes, barcodes, and warehouse objects directly from a smartphone. Captured information is processed locally or in the cloud using Artificial Intelligence and automatically integrated with enterprise systems.

---

# 🌐 Part of the Triminds Platform

Triminds ObjectScanner is one of the products within the **Triminds Platform** ecosystem.

Although it can operate as a standalone application, it is designed to integrate seamlessly with the **Triminds Platform UI**, sharing a common architecture, authentication, design system and user experience across the entire platform.

## Related Triminds Projects

| Project                    | Description                                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------------- |
| **Triminds Platform UI**   | Enterprise frontend, Design System and application shell shared across all Triminds products. |
| **Triminds Security**      | Enterprise Authentication, Authorization and Security services.                               |
| **Triminds Geo AI**        | Geospatial Artificial Intelligence platform for Earth Observation and satellite imagery.      |
| **Triminds SmartImageLab** | AI laboratory for image processing, experimentation and computer vision.                      |

### Platform Vision

```text
                    Triminds Platform

                           │

     ┌──────────────┬──────────────┬──────────────┐
     │              │              │              │
 Platform UI   ObjectScanner   Geo AI    SmartImageLab
     │
     └──────────────┬──────────────┐
                    │
               Security Services
```

The Triminds ecosystem follows a modular architecture where products remain independent while sharing a unified enterprise platform.

---

# 🚀 Project Overview

Triminds ObjectScanner combines an Android application with a Python backend to provide real-time object detection, counting and inventory support powered by Artificial Intelligence.

The solution integrates modern Computer Vision techniques with enterprise cloud technologies, enabling organizations to automate warehouse operations without specialized scanning hardware.

---

# ✨ Key Features

* 📱 Native Android application
* 🤖 YOLOv8 real-time object detection
* 🔍 Automatic object counting
* ☁ Azure Computer Vision fallback
* 🏭 Warehouse asset identification
* 📦 Pallet and box recognition
* 🏷 Label and barcode detection
* ☁ Cloud synchronization
* 🗄 Oracle Database integration
* 🔄 REST API
* 🧠 Custom AI model training
* 📊 Audit trail support
* 🔐 Enterprise-ready architecture

---

# 🏗 Solution Architecture

```text
                    Android Device
                           │
                     Camera Capture
                           │
                           ▼
               Image Processing Pipeline
                           │
            ┌──────────────┴──────────────┐
            │                             │
       YOLOv8 Engine         Azure Computer Vision
            │                             │
            └──────────────┬──────────────┘
                           ▼
                    Flask REST API
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   Oracle Database      Cloud Sync      TLP Integration
```

---

# 📁 Project Structure

```text
ObjectScanner/

├── PythonBackend/
│   ├── app.py
│   ├── requirements.txt
│   ├── setup_en.sh
│   ├── .env.example
│   │
│   ├── ml_model/
│   │   ├── train.py
│   │   ├── detect.py
│   │   ├── export.py
│   │   ├── config.py
│   │   └── dataset/
│   │
│   ├── services/
│   │   ├── object_count_service.py
│   │   ├── ml_detection_service.py
│   │   └── azure_service.py
│   │
│   └── config/
│       └── db_config.py
│
├── Android/
│   ├── app/
│   ├── build.gradle
│   └── settings.gradle
│
├── OracleDatabase/
│   └── schema/
│       └── create_tables.sql
│
├── docs/
│   ├── ADRs/
│   └── architecture.md
│
├── .github/workflows/
│
├── README.md
│
└── .gitignore
```

---

# 🛠 Technology Stack

| Layer             | Technologies                         |
| ----------------- | ------------------------------------ |
| Mobile            | Java, Android SDK, CameraX, Retrofit |
| Backend           | Python, Flask                        |
| AI / ML           | YOLOv8, Ultralytics, Roboflow        |
| Computer Vision   | Azure Computer Vision                |
| Database          | Oracle Database                      |
| Cloud             | Oracle Cloud, Railway, Docker        |
| CI/CD             | GitHub Actions                       |
| Frontend Platform | Triminds Platform UI                 |

---

# ⚙ Core Components

## 📱 Android Application

* CameraX integration
* Image capture
* REST communication
* Offline-ready architecture
* Mobile-first experience

---

## 🤖 AI Detection Engine

* YOLOv8 inference
* Custom datasets
* Roboflow integration
* Object counting
* Bounding box generation
* Confidence filtering

---

## ☁ Azure Vision Integration

When confidence is below the configured threshold, ObjectScanner automatically invokes Azure Computer Vision as a secondary inference engine, increasing robustness in challenging environments.

---

## 🗄 Database Layer

 
* Scan history
* Audit logs
* Detection metadata
* Historical analytics

---

## 🔄 REST API

The backend exposes REST endpoints for inference, model integration and synchronization with enterprise systems.
---

# 🚀 Installation

## Clone Repository

```bash
git clone https://github.com/RodrigoDiasDeOliveira/Object-Scanner.git
cd Object-Scanner
```

---

## Backend Setup

```bash
cd PythonBackend

# Install dependencies
bash setup_en.sh

# Configure environment variables
cp .env.example .env

# Edit the .env file with your credentials
```

Start the server:

```bash
python app.py
```

---

## Android Application

Open the **Android/** folder using Android Studio.

Update the backend URL in:

```
RetrofitClient.java
```

Run the application on a physical Android device.

---

# 📸 Usage

## Mobile Application

1. Launch the application
2. Point the camera at pallets, boxes, labels or warehouse assets
3. Tap **Capture & Analyze**
4. Review detected objects
5. Results are automatically synchronized with enterprise systems

---

# 🌐 REST API

## Object Detection

```bash
POST /detect
```

Example:

```bash
curl -X POST \
-F "image=@sample.jpg" \
http://localhost:5000/detect
```

Sample response:

```json
{
  "success": true,
  "counts": {
    "pallet": 12,
    "box": 45,
    "sack": 8
  },
  "source": "ml",
  "scan_id": 784
}
```

---

# 🧠 AI Model Training

Triminds ObjectScanner supports custom datasets, allowing organizations to train models specific to their warehouse environment.

## Dataset Preparation

1. Create or fork a dataset in Roboflow
2. Upload custom warehouse images
3. Generate a YOLOv8 dataset
4. Download the dataset

Extract it into:

```text
PythonBackend/ml_model/dataset
```

Train:

```bash
python train.py
```

Export:

```bash
python export.py
```

---

# ☁ Cloud Deployment

Supported deployment environments include:

* Oracle Cloud Infrastructure
* Railway
* Docker
* Kubernetes (future)
* Azure
* Google Cloud Platform

Docker example:

```bash
docker build -t triminds-objectscanner .

docker run -p 5000:5000 triminds-objectscanner
```

---

# 🧪 Testing

The project supports multiple testing layers.

## Unit Tests

* AI services
* Detection pipeline
* Database layer
* REST API
* Utility classes

---

## Integration Tests

* Android ↔ Backend
* Backend ↔ Oracle Database
* Backend ↔ Azure Vision
* Backend ↔ TLP System

---

## Performance Tests

* Inference latency
* Detection throughput
* Mobile upload time
* API response time

Run:

```bash
pytest
```

---

# 📊 Future Roadmap

## Artificial Intelligence

* Instance Segmentation
* Pose Estimation
* OCR integration
* Multi-model inference
* Video stream detection
* Edge AI optimization

---

## Mobile

* Offline inference
* Local TensorFlow Lite models
* Automatic synchronization
* Multi-camera support

---

## Cloud

* Kubernetes deployment
* Horizontal autoscaling
* Streaming inference
* Event-driven architecture
* Real-time dashboards

---

## Platform

* Native Triminds Platform UI integration
* Unified Authentication
* Shared Dashboard
* Centralized Notifications
* Role-based permissions
* Cross-product navigation

---

# 🎯 Design Principles

* Modular Architecture
* Cloud-Native Design
* AI-First Development
* Separation of Concerns
* Production-Ready Components
* Enterprise Security
* High Scalability
* Maintainability
* Reusability

---

# 📚 Documentation

The architecture and ADRs record intended decisions; they do not by themselves prove that the referenced backend, model, database or cloud integrations are present in this repository. See the [ObjectScanner V1 README/ADR/code evidence review](docs/object-scanner-v1-code-evidence-review-2026-10-11.md) for the tracked-tree comparison and explicit verification boundaries.

Project documentation includes:

* Architecture Decision Records (ADRs)
* System Architecture
* AI Pipeline
* Deployment Guides
* API Documentation
* Cloud Architecture

---

# 🤝 Contributing

Contributions are welcome.

Feel free to:

* Open Issues
* Submit Pull Requests
* Suggest Improvements
* Report Bugs

Please follow the project's coding standards and contribution guidelines.

---

# 📜 License

This project is licensed under the **MIT License**.

---

# 🚀 Triminds Ecosystem

Triminds ObjectScanner is part of a growing ecosystem of enterprise AI products.

```text
Triminds

├── Platform UI
│
├── Geo AI
│
├── ObjectScanner
│
├── SmartImageLab
│
├── Security
│
└── Future Enterprise Products
```

Each product is independently deployable while sharing a common platform architecture, enterprise security model and user experience through the **Triminds Platform UI**.

---

## Building the Future of Enterprise AI

**Triminds** is building a modular ecosystem of enterprise-grade Artificial Intelligence solutions focused on Computer Vision, Geospatial Intelligence, Cloud Computing, MLOps and Digital Transformation.

Every product follows the same engineering principles:

* 🧩 Modular Architecture
* ☁ Cloud-Native Infrastructure
* 🤖 AI-First Design
* 🔒 Enterprise Security
* 🚀 Production-Ready Solutions
* ♻ Reusable Components
* 🌐 Unified Platform Experience

Together, these products form a scalable platform capable of supporting multiple AI domains while maintaining consistency, maintainability and extensibility across the entire Triminds ecosystem.

