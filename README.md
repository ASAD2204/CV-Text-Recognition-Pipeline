# Text Detection & Recognition

A comprehensive Computer Vision semester project (6th Semester) focused on multi-model text detection and recognition from images using a hybrid ensemble of classical, deep learning, and transformer-based OCR approaches.

## ⭐ Project Highlights
- **Unified Pipeline**: Combines detection, region processing, recognition, post-processing.
- **Multi-Engine OCR**: EasyOCR, PaddleOCR, TrOCR (Transformers), YOLO-based detection assistance, and optional MMOCR stack.
- **Ensemble Strategy**: Aggregates predictions from multiple OCR engines for improved accuracy.
- **Language Processing**: Spell checking, POS tagging, tokenization, semantic refinement (Sentence Transformers + language_tool_python).
- **Document Layout Awareness**: Optional layout parsing via `layoutparser` + `detectron2`.
- **Image Enhancement**: Super-resolution support (Real-ESRGAN) and noise / artifact reduction.
- **Advanced Preprocessing**: Albumentations-based augmentation, morphological filtering, clustering (DBSCAN) and connected component analysis (skimage/scipy).
- **Interactive UI**: Gradio interface for rapid experimentation.

## 🧠 Core Components
| Stage | Libraries | Purpose |
|-------|-----------|---------|
| Detection | YOLO (ultralytics), PaddleOCR detector, EasyOCR detector, optional MMOCR | Find text regions / boxes |
| Enhancement | Real-ESRGAN (basicsr, realesrgan), OpenCV | Improve image quality prior to recognition |
| Recognition | TrOCR (HuggingFace Transformers), EasyOCR, PaddleOCR | Extract raw text from regions |
| Post-processing | spellchecker, nltk, language_tool_python, Sentence Transformers | Cleanup, grammar, semantic consistency |
| Layout | layoutparser, detectron2 | Logical grouping by document structure |
| Utility | numpy, skimage, scipy, scikit-learn (DBSCAN), imutils | Array ops, clustering, segmentation |
| Interface | gradio, matplotlib | Visual feedback + interaction |

## 📂 Repository Structure
```
.
├── Text_Detection_&_Recognition.ipynb   # Main development / experimentation notebook
├── Results/                             # Output samples, visualizations, inference examples
├── README.md                            # Project overview (this file)
├── LICENSE                              # MIT License
├── setup.md                             # Detailed environment & setup guide
├── requirements.txt                     # Python dependencies
└── .gitignore                           # Ignore rules for repo hygiene
```

## ⚙️ Dependencies
Detected from the notebook imports:
```
opencv-python
numpy
Pillow
matplotlib
gradio
transformers
torch
spellchecker
nltk
easyocr
paddleocr
ultralytics
scikit-image
scipy
imutils
scikit-learn
albumentations
mmcv
mmdet
mmocr
layoutparser
detectron2
basicsr
realesrgan
sentence-transformers
language-tool-python
onnx
onnxruntime
```
Additional stdlib modules used: `io`, `re`, `time`, `warnings`.

> NOTE: Some libraries (e.g., `detectron2`, `mmcv`, `mmdet`, `mmocr`, `RealESRGAN`, GPU-enabled `ultralytics`) benefit from CUDA-enabled environments. If you do not need advanced layout or MMOCR functionality, you can omit those heavy dependencies for a lean setup.

## 🚀 Quick Start
```powershell
# Clone your repository after pushing it
git clone https://github.com/ASAD2204/Text-Detection-Recognition.git
cd Text-Detection-Recognition

# (Optional) Create virtual environment
python -m venv .venv
.\.venv\Scripts\activate

# Install dependencies (edit requirements.txt if trimming heavy libs)
pip install --upgrade pip
pip install -r requirements.txt

# (Optional) Download NLTK assets
python -c "import nltk; nltk.download('punkt'); nltk.download('stopwords'); nltk.download('averaged_perceptron_tagger')"

# Launch the notebook
jupyter notebook Text_Detection_&_Recognition.ipynb
```

## 🧪 Workflow Summary
1. Load / upload image.
2. Preprocess & optionally enhance (contrast, resize, super-resolution).
3. Run detection models (YOLO / Paddle / EasyOCR / optional MMOCR).
4. Normalize & merge bounding boxes.
5. Run recognition engines per box (TrOCR, EasyOCR, PaddleOCR).
6. Ensemble + confidence aggregation.
7. NLP post-processing (spellcheck, grammar, semantic similarity re-ranking).
8. Display results in Gradio UI + export to `Results/`.

## 📈 Results
Place sample input images and output overlays (bounding boxes + recognized text) in the `Results/` directory. Include:
- Original image (`original_*.png`)
- Detection visualization (`detected_*.png`)
- Recognition text file (`recognized_*.txt`)
- (Optional) Enhanced image (`enhanced_*.png`)

## 🛠 Configuration Ideas
| Option | Description | Where |
|--------|-------------|-------|
| Model selection | Enable / disable specific OCR engines | Notebook cell variables |
| Confidence threshold | Filter low-probability detections | Detection loop |
| Language model | Choose spellcheck / grammar language | Post-processing section |
| Augmentations | Control albumentations pipeline | Preprocessing function |

## 🐛 Troubleshooting
- `CUDA not available`: Some models fall back to CPU (slower). Ensure proper GPU drivers and PyTorch installation.
- `detectron2 install error`: Pin versions matching your CUDA & PyTorch; or skip if layout parsing not needed.
- `Out of memory`: Reduce image resolution or disable heavy models like MMOCR.
- `Slow inference`: Limit the number of engines in ensemble.

## 🔍 Potential Improvements / Roadmap
- Add benchmarking scripts for per-engine accuracy and latency.
- Export ONNX / optimized runtime for TrOCR.
- Integrate lightweight language model for context-aware correction.
- Batch processing CLI tool.
- Web deployment (FastAPI + frontend).
- Unit tests for preprocessing & post-processing modules.

## 🤝 Contributing
1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/my-improvement`.
3. Commit changes: `git commit -m "Add enhancement"`.
4. Push: `git push origin feature/my-improvement`.
5. Open a Pull Request describing motivation & changes.

Please keep notebook cells organized and avoid committing large model weights.

## 📜 License
This project is licensed under the MIT License – see `LICENSE` for details.

## 🙏 Acknowledgements
- HuggingFace Transformers (TrOCR)
- EasyOCR & PaddleOCR
- Ultralytics YOLO
- Real-ESRGAN authors
- Detectron2 / LayoutParser community
- NLTK & SentenceTransformers teams

## 📣 Citation (Optional)
If you use parts of this work in academic settings, cite the relevant upstream libraries (e.g., TrOCR paper, YOLO, Detectron2) alongside your own report.

```
@misc{asad2025textdetectionrecognition,
  title  = {Hybrid Multi-Engine Text Detection & Recognition},
  author = {Asad},
  year   = {2025},
  note   = {Semester Project, Computer Vision Course}
}
```

## ✅ Status
Currently in research / experimentation phase using notebook workflow. Transition to modular Python package is a future goal.

---
Feel free to tailor `requirements.txt` if deploying on constrained environments. See `setup.md` for deeper installation notes.
