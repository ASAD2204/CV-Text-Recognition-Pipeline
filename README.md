# Text Detection & Recognition

A multi-engine OCR system that combines transformer-based models, classical computer vision techniques, and ensemble methods for robust text detection and recognition from images.

## Overview

This project implements a hybrid pipeline that leverages multiple state-of-the-art OCR engines (TrOCR, EasyOCR, PaddleOCR) alongside YOLO-based detection to achieve high-accuracy text extraction. The system includes preprocessing, layout analysis, ensemble inference, and NLP-based post-processing to handle diverse document types and image quality conditions.

Developed as a semester project for Computer Vision course (6th Semester).

## Features

- Multi-model ensemble approach combining TrOCR, EasyOCR, and PaddleOCR
- YOLO-based text region detection with confidence aggregation
- Image enhancement pipeline using Real-ESRGAN super-resolution
- Document layout analysis via Detectron2 and LayoutParser
- Advanced preprocessing with Albumentations and morphological operations
- NLP post-processing including spell checking, grammar correction, and semantic validation
- Interactive Gradio interface for testing and visualization

## Architecture

The pipeline consists of four main stages:

1. **Detection** - Text regions are identified using YOLO, PaddleOCR detector, and EasyOCR detector. Bounding boxes are normalized and merged using clustering (DBSCAN).

2. **Preprocessing** - Images undergo contrast enhancement, noise reduction, and optional super-resolution. Albumentations handles augmentation for robust recognition.

3. **Recognition** - Multiple OCR engines process each detected region. TrOCR provides transformer-based recognition, while EasyOCR and PaddleOCR offer complementary strengths for different text styles.

4. **Post-processing** - Results are aggregated through ensemble voting. Text undergoes spell checking (pyspellchecker), grammar validation (LanguageTool), and semantic consistency checks (Sentence Transformers).

## Installation

See `setup.md` for detailed installation instructions. Quick start:

```bash
git clone https://github.com/ASAD2204/CV-Text-Recognition-Pipeline.git
cd CV-Text-Recognition-Pipeline
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

Some dependencies (detectron2, mmcv, mmdet) require specific CUDA versions. Refer to `setup.md` for platform-specific guidance.

## Usage

Launch the Jupyter notebook:

```bash
jupyter notebook Text_Detection_&_Recognition.ipynb
```

The notebook provides an interactive Gradio interface for uploading images and viewing results. Outputs are saved to the `Results/` directory.

## Dependencies

Core libraries: PyTorch, Transformers, OpenCV, NumPy, Pillow, Gradio

OCR engines: EasyOCR, PaddleOCR, TrOCR

Detection: Ultralytics YOLO, MMOCR (optional)

Enhancement: Real-ESRGAN, BasicSR

Layout: LayoutParser, Detectron2

NLP: NLTK, pyspellchecker, LanguageTool, Sentence Transformers

See `requirements.txt` for complete list.

## Project Structure

```
├── Text_Detection_&_Recognition.ipynb   # Main notebook
├── Results/                             # Output directory
├── README.md
├── LICENSE
├── setup.md                             # Installation guide
├── requirements.txt
└── .gitignore
```

## Performance Considerations

GPU acceleration is strongly recommended. The ensemble approach trades inference speed for accuracy. For faster processing, disable heavy models (MMOCR, Real-ESRGAN) or reduce the number of engines in the ensemble.

Memory usage scales with image resolution and number of active models. For large images or constrained environments, consider downsampling input or running engines sequentially.

## Known Limitations

- Detectron2 installation can be complex on Windows (requires specific CUDA/PyTorch compatibility)
- LanguageTool requires Java runtime for full functionality
- MMOCR support is optional due to dependency complexity
- Current implementation is notebook-based; modular Python package is planned

## Contributing

Contributions are welcome. Please ensure notebook cells are well-documented and avoid committing model weights or large binary files.

## License

MIT License - see `LICENSE` file.

## Acknowledgments

This project builds upon work from HuggingFace Transformers, Ultralytics, JaidedAI (EasyOCR), PaddlePaddle, Real-ESRGAN, Detectron2, and the LayoutParser team.
