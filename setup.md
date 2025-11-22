# Setup Guide

This document provides a detailed, step-by-step setup for running the Text Detection & Recognition project on Windows using PowerShell. Adjust as needed for other platforms.

## 1. Prerequisites
- Windows 10/11 (64-bit)
- Python 3.9–3.11 (64-bit recommended)
- (Optional) NVIDIA GPU + CUDA (for faster PyTorch, YOLO, Detectron2, MMOCR)
- Git installed

## 2. Clone the Repository
```powershell
git clone https://github.com/ASAD2204/Text-Detection-Recognition.git
cd Text-Detection-Recognition
```

## 3. Create & Activate Virtual Environment
```powershell
python -m venv .venv
.\.venv\Scripts\activate
```
To deactivate later: `deactivate`

## 4. Upgrade Package Tools
```powershell
python -m pip install --upgrade pip wheel setuptools
```

## 5. Install Base Dependencies
```powershell
pip install -r requirements.txt
```
If you face build issues with heavy packages (e.g., `detectron2`, `mmcv`, `mmdet`, `mmocr`), you may skip them initially by commenting them out in `requirements.txt`.

## 6. GPU (Optional but Recommended)
Install the correct CUDA-enabled PyTorch (refer to https://pytorch.org/get-started/locally/). Example:
```powershell
pip install torch --index-url https://download.pytorch.org/whl/cu118
```
Reinstall dependent libraries if needed.

## 7. NLTK Data
```powershell
python -c "import nltk; nltk.download('punkt'); nltk.download('stopwords'); nltk.download('averaged_perceptron_tagger')"
```

## 8. Verify Core Imports
```powershell
python - <<'PY'
try:
    import cv2, torch, transformers, easyocr, paddleocr, gradio
    print('Core libraries imported successfully.')
except Exception as e:
    print('Import error:', e)
PY
```

## 9. Running the Notebook
Install Jupyter if not already present:
```powershell
pip install notebook
```
Launch:
```powershell
jupyter notebook Text_Detection_&_Recognition.ipynb
```

## 10. Optional Enhancements
| Feature | Library | Install |
|---------|---------|---------|
| Layout Parsing | layoutparser, detectron2 | `pip install layoutparser` then follow detectron2 instructions |
| MMOCR Toolkit | mmocr, mmcv, mmdet | See official install docs (version compatibility matters) |
| Super Resolution | realesrgan, basicsr | `pip install realesrgan basicsr` |
| Sentence Semantics | sentence-transformers | Already in requirements |
| Grammar Checking | language-tool-python | Requires Java installed for full functionality |

## 11. Troubleshooting
| Problem | Cause | Fix |
|---------|-------|-----|
| `torch not found` | Wrong install channel | Reinstall from PyTorch site |
| `DLL load failed (cv2)` | Incompatible Python | Use official Python / reinstall opencv-python |
| `detectron2 build failed` | CUDA / VS Build Tools missing | Install proper CUDA & MSVC Build Tools or skip |
| Slow inference | CPU-only environment | Limit engines or install GPU toolchain |
| Memory errors | Large image / many models | Reduce image size, disable ensemble |

## 12. Minimal Mode (Lightweight)
If you only need basic OCR (no layout, no TrOCR ensemble):
Comment out in `requirements.txt`:
- `mmcv`, `mmdet`, `mmocr`, `layoutparser`, `detectron2`, `realesrgan`, `basicsr`
Then reinstall:
```powershell
pip install -r requirements.txt --no-deps
```
Add back missing deps manually if errors occur.

## 13. Exporting Results
The notebook saves or you can manually copy outputs into the `Results/` directory. Recommended naming:
```
original_<id>.png
enhanced_<id>.png
detected_<id>.png
recognized_<id>.txt
```

## 14. Updating Dependencies
```powershell
pip list --outdated
pip install --upgrade <package>
```
Pin versions in `requirements.txt` before publishing for reproducibility.

## 15. Next Steps
- Convert notebook logic into modular Python scripts.
- Add unit tests.
- Provide a CLI interface for batch OCR.

---
Refer back to `README.md` for conceptual overview & roadmap.
