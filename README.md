> **Note:** Datasets and saved model artefacts are stored on Google Drive 
> due to GitHub file size limits. See links below.

---

## Google Drive Resources

| Resource | Link |
|---|---|
| Datasets (CSV files) | https://drive.google.com/drive/folders/1YhomYvnxp7FkzAUc6Azb4yRcO3-n8KAc?usp=sharing |
| Saved Models & Artefacts | https://drive.google.com/drive/folders/1SRG5UlalxuMuWTMD_2Azi5TlzEwwFzDq?usp=drive_link |
| Codebase | https://drive.google.com/file/d/1n9RM2vcpnDMehlBduKePcgkJed_RvKX1/view?usp=sharing |



---

## How to Run

### Option 1 — Full Training Pipeline (≈60–90 min, GPU required)

1. Open `w1956736_FYP.ipynb` in Google Colab
2. Set runtime to **GPU** (Runtime → Change runtime type → T4 GPU)
3. Mount your Google Drive and update the dataset paths in **Cell 1** 
   to point to your copied dataset folder
4. Run all cells in order (Cells 1–21)

### Option 2 — Quick Reload Demo (≈2 min, no retraining)

1. Open `w1956736_FYP.ipynb` in Google Colab
2. Set runtime to **GPU**
3. Copy the saved models folder from Drive to your own Drive
4. Update the model paths in the **Quick Reload cell**
5. Run only the **Quick Reload cell** — this loads all saved artefacts 
   and launches the Gradio interface directly

---

## Model Performance Summary

| Model | Accuracy | F1 (Weighted) | ROC-AUC |
|---|---|---|---|
| ExtraTrees | 97.61% | 0.9761 | 0.9964 |
| Random Forest | 94.62% | 0.9459 | 0.9903 |
| DistilBERT | 98.97% | 0.9897 | 0.9989 |
| **Ensemble** | **98.86%** | **0.9886** | **0.9986** |



---

## Installation (Local — optional)

```bash
git clone https://github.com/aeron02/w1956736_FYP.git
cd w1956736_FYP
pip install -r requirements.txt
```

> ⚠️ Local execution of DistilBERT inference requires a CUDA-compatible 
> GPU. CPU-only inference is supported but will be significantly slower.

---

## Key Dependencies

- Python 3.10
- scikit-learn, imbalanced-learn — classical ML pipeline
- HuggingFace Transformers — DistilBERT fine-tuning
- PyTorch — deep learning backend
- NLTK, TextStat — metadata feature extraction
- Gradio — web application deployment

---

