# Smartphone-based-Body-fluid-cells
Body fluid cell classification
# 📱🔬 Body Fluid Cell Classification using Smartphone-Based Deep Learning

## 🚀 Overview
This project presents a **cloud-deployable, explainable AI framework** for automated **body fluid cell classification** using smartphone-acquired microscopy images. The pipeline integrates:

- 📸 Smartphone microscopy (Olympus CX33 + iPhone)
- 🧠 Deep learning detection models (YOLOv8n, YOLOv10n, YOLOv11n, YOLOv11n-seg, RT-DETR)
- 🔍 ROI-based classification (ResNet18)
- 🧬 Explainable AI (Grad-CAM++)
- ☁️ FastAPI deployment (Cloud-ready)

---

## 📊 Key Features
- Multi-class detection of **7 body fluid cell types**
- Real-time inference via REST API
- Explainable predictions (Grad-CAM++)
- Smartphone-compatible image acquisition
- Scalable cloud deployment (Docker + Cloud Run)

---

## 🧪 Dataset
- **Source:** Wright–Giemsa stained cytospin slides
- **Images:** 7,149
- **Input size:** 640 × 640 pixels
- **Final classes (7):**
  - Atypical lymphocyte  
  - Eosinophil  
  - Lymphocyte  
  - Macrophage  
  - Mesothelial cell  
  - Monocyte  
  - Neutrophil  

> ⚠️ Rare classes (e.g., plasma cells, signet-ring cells) were excluded due to class imbalance.

---

---

## ⚙️ Installation

### 1. Clone repository
```bash
git clone https://github.com/your-repo/bodyfluid-ai.git
cd bodyfluid-ai

2. Install dependencies
pip install -r requirements.txt
Model Training

Train using Ultralytics:
yolo detect train \
  model=yolov11n.pt \
  data=data.yaml \
  epochs=30 \
  imgsz=640
Evaluation Metrics
Detection:
mAP@50
mAP@50–95
Precision / Recall
Classification (confusion-matrix-based):
Macro F1
Weighted F1

Explainable AI (Grad-CAM++)
ROI extracted from detection
ResNet18 classifier applied
Grad-CAM++ visualizes:
Nuclear focus regions
Morphological features

API Usage (FastAPI)
Run locally
uvicorn backend.main:app --reload

Prediction
POST /predict
Content-Type: multipart/form-data

Example Response

{
  "model": "YOLOv11n",
  "num_detections": 3,
  "detections": [
    {
      "class_name": "Neutrophil"
      "confidence": 0.92,
      "bbox": [120, 80, 250, 210]
    }
  ]
}

Docker Deployment
Build image
docker build -t bodyfluid-ai .

,Run container

docker run -p 8080:8080 bodyfluid-ai

Cloud Deployment (Recommended)
Google Cloud Run

gcloud builds submit --tag gcr.io/YOUR_PROJECT/bodyfluid-ai
gcloud run deploy --image gcr.io/YOUR_PROJECT/bodyfluid-ai --platform managed

