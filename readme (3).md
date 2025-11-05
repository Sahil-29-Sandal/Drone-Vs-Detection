# Drone vs Bird Detection — Project Package

## Project Architecture Diagram
## flowchart TD
A[Input Video] --> B[Frame Extraction (OpenCV)]
B --> C[Annotated Images from Roboflow]
C --> D[YOLOv8 Training Pipeline]
D --> E[Model Weights (.pt)]
E --> F[Inference on Drone/Bird Videos]
F --> G[Bounding Boxes + Class Labels]


## Dataset Workflow Diagram
flowchart TD
A[Raw Videos (70)] --> B[Selection (40 videos)]
B --> C[Frame Extraction every 5 sec]
C --> D[Manual Annotation in Roboflow]
D --> E[Bird Dataset Augmentation]
E --> F[Train/Test Split]
F --> G[Export YOLO format dataset]
```

---

## Google Colab Notebook Template

### **Usage**
Copy code blocks into Colab.

### **Notebook**
```python
!pip install ultralytics roboflow opencv-python

from roboflow import Roboflow
rf = Roboflow(api_key="YOUR_API_KEY")
project = rf.workspace().project("drone-vs-bird")
dataset = project.version(1).download("yolov8")

from ultralytics import YOLO
model = YOLO("yolov8n.pt")

model.train(data="data.yaml", epochs=50, imgsz=640)

model.predict(source="test_video.mp4", save=True)
```

## 📄 Abstract

This project focuses on distinguishing drones and birds using a YOLOv8 object detection model. A dataset of 70 aerial surveillance videos was collected, from which 40 high‑quality videos were selected. Frames were extracted at five‑second intervals and annotated manually using Roboflow. To improve class balance, an additional external bird dataset was merged and augmented. YOLOv8‑nano was trained for 50 epochs, achieving a mAP of approximately 68%. The system successfully identifies drones vs birds and can assist in security surveillance, aviation safety, and anti‑drone monitoring systems.

---

