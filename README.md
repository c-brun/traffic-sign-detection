# German Traffic Sign Detection

*Comparing YOLOv8 and RT-DETR architectures for real-world traffic sign detection*

## 🎯 Project Overview

This project implements and compares two modern object detection architectures for German traffic sign detection using the German Traffic Sign Detection Benchmark (GTSDB). The goal is to evaluate different architectural approaches for real-world traffic sign detection systems that could support autonomous vehicles and driver assistance systems.

## 🏆 Key Results

| Metric          | YOLOv8x       | RT-DETR      | Winner     |
|-----------------|---------------|--------------|------------|
| **mAP50**       | **65.5%**     | 59.5%        | 🥇 YOLO    |
| **mAP50-95**    | 53.2%         | **53.2%**    | 🤝 Tie     |
| **Precision**   | 51.9%         | **52.2%**    | 🥇 RT-DETR |
| **Recall**      | **88.2%**     | 80.3%        | 🥇 YOLO    |
| **Speed**       | **22 FPS**    | 18 FPS       | 🥇 YOLO    |

**Key Finding**: YOLO excels at finding signs (high recall), while RT-DETR is more precise but misses more signs overall.

## 🚗 Real-World Challenge

Traffic sign detection is more complex than typical object detection because:
- **Size variations**: Signs range from distant highway signs to close-up street signs
- **Lighting conditions**: From bright sunlight to nighttime/shadowy conditions  
- **Class imbalance**: Some signs (like "Keep Right") appear 88 times while others (like "Animals") appear only twice
- **Similar appearances**: Multiple speed limit signs that look nearly identical

## 🔬 Technical Approach

### Data Strategy
- **900 real-world images** from German roads
- **43 traffic sign classes** split into standard (≥13 samples) and few-shot (<13 samples) categories
- **Smart data splitting**: 60% train / 10% validation / 30% test with no image overlap
- **Targeted augmentation**: Conservative for RT-DETR, aggressive for YOLO

### Model Architectures
- **YOLOv8x**: Traditional CNN-based single-stage detector optimized for speed
- **RT-DETR**: Modern transformer-based architecture with attention mechanisms

### Training Innovations
- **Class-aware evaluation**: Identified that performance isn't just about sample size
- **Architecture-specific augmentation**: Different strategies for each model type
- **Comprehensive metrics**: Beyond accuracy to include precision, recall, and speed

## 📁 Repository Structure

```
├── 1_standard_model_comparison.ipynb    # Main model comparison (26 standard classes)
└── README.md                           # This file
```

*Note: 2_few_shot_learning.ipynb (advanced techniques for rare signs) is currently in development*

## 🚀 How to Run

1. **Open in Colab**: Click the "Open in Colab" button on any notebook
2. **Mount Google Drive**: Follow the authentication prompts
3. **Install dependencies**: Run the setup cells (libraries auto-install)
4. **Run all cells**: Each notebook is self-contained and fully executable

**Prerequisites**: Google account for Colab access (no local setup required)

## 💡 Key Insights

**Architectural Trade-offs Discovered**:
- YOLO's single-stage approach provides better overall detection coverage
- RT-DETR's transformer architecture offers more precise detections
- Speed vs. accuracy trade-off varies significantly between architectures

**Visual Distinctiveness Matters More Than Sample Size**:
- "Speed limit 100" (28 samples) outperformed "Speed limit 120" (45 samples)
- Sign visual characteristics and validation representation are key factors

**Evaluation Reliability**:
- Classes with single test samples showed unreliable performance metrics
- Larger validation sets would improve model selection confidence

## 🛠️ Technologies Used

- **Deep Learning**: PyTorch, Ultralytics (YOLOv8x), RT-DETR
- **Computer Vision**: OpenCV
- **Data Processing**: NumPy, Pandas, scikit-learn
- **Visualization**: Matplotlib
- **Environment**: Google Colab, Python 3.8+

## 🔮 Future Improvements

**Immediate Enhancements** (Research/Accuracy Focus):
- **Multi-stage pipeline**: Separate detection and classification for 10-15% mAP improvement  
- **Comprehensive augmentation**: Advanced preprocessing techniques for 8-12% performance boost
- **Class-weighted loss functions**: Address imbalance for 5-8% boost on rare classes

**Production Optimizations**:
- Model ensemble: Combine both architectures' strengths for 2-4% overall improvement
- Model compression and quantization for faster inference
- Real-time video processing pipeline

## 📊 Few-Shot Learning Extension (In Development)

A second notebook explores advanced techniques for the 17 underrepresented sign classes using specialized augmentation and few-shot learning methods. This addresses one of the core challenges in real-world deployment where rare but critical signs must be detected reliably.

---

*This project was developed as part of a Deep Learning certification program, demonstrating practical application of modern computer vision techniques to real-world transportation challenges.*
