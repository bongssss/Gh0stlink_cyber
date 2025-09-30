
---

### **3. Custom Object Detection (YOLOv8)**  
```markdown
#  Custom Object Detection (YOLOv8)

##  Overview
This project is a **custom-trained object detection model** using YOLOv8.  
It detects specific objects in images/videos (e.g., PPE gear, fruits, or vehicles).

##  Features
- Trained YOLOv8 model on custom dataset.
- Image & video detection.
- REST API for inference.
- Web UI for uploads + results.

##  Tech Stack
- Python, PyTorch, YOLOv8
- FastAPI backend
- Streamlit/React frontend

##  How It Works
1. Upload image/video.
2. Model predicts bounding boxes + labels.
3. Annotated result returned.

##  Example
**Input:** Workplace image  
**Output:** Bounding boxes around "Helmet", "Vest", "Boots"

##  Screenshots
(Add before/after images with detections)

##  Installation
```bash
git clone <repo>
cd object-detection
pip install -r requirements.txt
uvicorn main:app --reload
