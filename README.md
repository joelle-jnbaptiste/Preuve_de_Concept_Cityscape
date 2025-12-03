# POC – Image Segmentation (Cityscapes)  
### *DeepLabV3+ vs Mask2Former Comparison*

---

## Project Objective

This Proof of Concept evaluates and compares two segmentation models — **DeepLabV3+ (baseline)** and **Mask2Former (state-of-the-art)** — on a reduced subset of the **Cityscapes** dataset.  
The project includes a full pipeline: dataset preparation, training with **MLflow**, metrics comparison, a **FastAPI** inference backend, and a **Streamlit** user interface.

---

## Project Structure

POC/
├── POC_backend/
│ ├── main.py
│ ├── model/ # Model files (ignored by Git)
│ ├── install-app
│ ├── install-conda
│ └── requirements.txt
│
├── POC_frontend/
│ ├── app.py
│ ├── img/
│ ├── metric_info/
│ ├── mlruns/ # Ignored by Git
│ └── requirements.txt
│
├── notebooks/
│ ├── notebook1.ipynb
│ └── notebook2.ipynb
│
├── slides/
├── method_note.pdf
└── README.md


---

## Dataset Used — Cityscapes

Cityscapes is a benchmark dataset of annotated urban street scenes.  
For this POC, a **reduced subset (~100 images)** was selected to enable fast experimentation while keeping visual diversity.

---

## Models Evaluated

### Baseline — DeepLabV3+ (ResNet50)
- CNN-based architecture with atrous (dilated) convolutions  
- Optimizer: AdamW  
- Fully tracked with MLflow  

### Modern Model — Mask2Former (Transformer-based)
- Universal segmentation architecture  
- Masked Attention Transformer decoder  
- Multi-scale high-resolution feature processing  
- Implementation from HuggingFace Transformers  

---

## Metrics Tracked (via MLflow)

- **Training Loss**  
- **Validation Loss**  
- **Pixel Accuracy**  
- **mIoU (mean Intersection over Union)**  
- **Images per second** (inference throughput)  
- **Training time per epoch**

---

## Results Summary

| Model            | Pixel Accuracy | mIoU  | Inference Speed (img/s) |
|------------------|----------------|-------|---------------------------|
| DeepLabV3+       | ~0.93          | ~0.64 | ~5.8                      |
| **Mask2Former**  | **~0.95+**     | **~0.77+** | **~6.4**              |

**Key takeaway:**  
**Mask2Former significantly outperforms DeepLabV3+** on all meaningful segmentation metrics while also being slightly faster to train and infer.

---

## Deployment

### Backend (FastAPI)
- Hosts the chosen trained model  
- Provides `/predict` endpoint for segmentation masks  
- Lightweight CPU-friendly preprocessing pipeline  

### Frontend (Streamlit)
- Upload an image  
- Visualize predicted segmentation  
- Compare DeepLabV3+ vs Mask2Former  
- Accessible UI with WCAG-compliant colors and alt-text descriptions  

---

## Installation & Usage

### 1️Clone the repository
```bash
git clone <your_repo_url>
cd POC

#Install backend
cd POC_backend
pip install -r requirements.txt
uvicorn main:app --reload

#Install frontend
cd ../POC_frontend
pip install -r requirements.txt
streamlit run app.py
```