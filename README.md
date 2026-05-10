# 💵 Fake Currency Detector

**Student:** Vy Vo | **Course:** ITAI 1378 – Computer Vision | **Tier:** 1  
**Houston Community College**

> A deep learning system that classifies banknote images as **real** or **fake** using ResNet50 transfer learning — 100% test accuracy, 19.80ms inference.

---

## 🎯 Problem & Solution

### The Problem
Counterfeit money causes significant financial losses for small businesses and individuals. Most small, cash-based businesses lack advanced tools to quickly verify whether a banknote is genuine.

### Our Solution
A computer vision model that takes a banknote image as input and outputs a **Real** or **Fake** prediction with confidence score — running in under 20ms, fast enough for real-time use at a register.

### Impact
- Small businesses can verify bills instantly without expensive hardware
- Zero ongoing cost after deployment (runs on CPU)
- Inference time of ~20ms allows real-time use

---

## 🔧 Technical Details

### Approach

| Component | Choice |
|-----------|--------|
| Task | Binary Image Classification |
| Model | ResNet50 (ImageNet pretrained) |
| Framework | PyTorch |
| Compute | Google Colab / CPU |

### System Architecture

```
[Banknote Image]
      ↓
[Preprocessing: Resize 224×224, Normalize (ImageNet μ/σ)]
      ↓
[ResNet50 Backbone — frozen layers 1–3]
      ↓
[Fine-tuned Layer4 + Custom FC Head (Dropout → 256 → ReLU → Dropout → 2)]
      ↓
[Softmax → Prediction: REAL or FAKE + Confidence %]
```

---

## 📊 Dataset

- **Source:** [Kaggle – Fake Currency Data](https://www.kaggle.com/datasets/mdladla/fake-currency-data)
- **Size:** 100 images total
- **Classes:** `fake` (50), `real` (50)
- **Split:** Train: 70 | Val: 15 | Test: 15
- **Preprocessing:** Resize to 224×224, ImageNet normalization
- **Augmentation (train only):** Random crop, horizontal/vertical flip, rotation ±15°, color jitter, random grayscale

> ⚠️ Dataset not included in this repo (Kaggle terms). Download from the link above and place images as:
> ```
> data/
> ├── fake/   ← fake banknote images
> └── real/   ← real banknote images
> ```

---

## 📈 Results

| Metric | Value | Target |
|--------|-------|--------|
| **Test Accuracy** | **100.00%** | ≥ 90% ✅ |
| **Precision** | **100.00%** | — ✅ |
| **Recall** | **100.00%** | — ✅ |
| **F1 Score** | **100.00%** | — ✅ |
| **Inference Time** | **19.80 ms** | < 1000 ms ✅ |
| Best Val Accuracy | 100.00% | — |
| Training stopped | Epoch 7/15 (early stopping) | — |

### Training History (per epoch)

| Epoch | Train Loss | Train Acc | Val Loss | Val Acc |
|-------|-----------|-----------|----------|---------|
| 1 | 0.6658 | 60.00% | 0.6243 | 40.00% |
| 2 | 0.4268 | 95.71% | 0.4455 | **100.00%** ✅ |
| 3 | 0.2909 | 98.57% | 0.2901 | 100.00% |
| 4 | 0.2320 | 100.00% | 0.2199 | 100.00% |
| 5 | 0.2394 | 97.14% | 0.2314 | 100.00% |
| 6 | 0.2121 | 100.00% | 0.2536 | 100.00% |
| 7 | 0.2162 | 100.00% | 0.2567 | 100.00% |

*Early stopping triggered at epoch 7 (patience=5).*

### Visualizations

| Plot | Description |
|------|-------------|
| `results/visualizations/accuracy_loss_plot.png` | Training & validation accuracy/loss curves |
| `results/visualizations/confusion_matrix.png` | Confusion matrix (counts + normalized) |
| `results/images/sample_images.png` | Sample training images grid |
| `results/images/class_distribution.png` | Dataset class balance |

---

## 🚀 How to Run

### Option 1: Google Colab (Recommended)
1. Open [`notebooks/01_exploration.ipynb`](notebooks/01_exploration.ipynb) in [Google Colab](https://colab.research.google.com/)
2. Download dataset from [Kaggle](https://www.kaggle.com/datasets/mdladla/fake-currency-data)
3. Upload and organize images into `data/fake/` and `data/real/`
4. Run all cells top to bottom

### Option 2: Local / VS Code
```bash
# Clone repo
git clone https://github.com/vhkv72/ITAI1378_Fake-Currency-Detector.git
cd ITAI1378_Fake-Currency-Detector

# Install dependencies
pip install -r requirements.txt

# Open notebook
jupyter notebook notebooks/01_exploration.ipynb
```

> **Windows / VS Code tip:** Change `num_workers=2` → `num_workers=0` in the DataLoader calls if you get a multiprocessing error.

### Single Image Prediction
```python
predict_image('path/to/banknote.jpg', model, val_test_transforms, CLASS_NAMES, device)
# Returns: ('real', 99.3)  or  ('fake', 87.6)
```

---

## 💡 Key Learnings

### What Worked Well
- Transfer learning from ImageNet converged in just **2 epochs** to 100% validation accuracy
- Data augmentation prevented overfitting despite only 70 training images
- Early stopping avoided unnecessary computation

### Challenges Faced
- **Challenge:** Only 100 images in the dataset — high risk of overfitting  
  **Solution:** Aggressive augmentation (7 transforms) + dropout + label smoothing + AdamW weight decay
- **Challenge:** `ImageFolder` requires a flat `class/images` structure  
  **Solution:** Used symlinks to expose only `fake/` and `real/` folders to the loader

### What I'd Do Differently
- Collect a larger, more diverse dataset (different currencies, lighting conditions)
- Try EfficientNet-B0 as a lighter alternative for mobile deployment
- Add Grad-CAM visualizations to show *which parts* of the bill the model focuses on

---

## 🎥 Demo Video

📺 *[Add your YouTube/Google Drive demo link here]*

---

## 🤖 AI Usage Documentation

See detailed log: [`docs/AI_usage_log.md`](docs/AI_usage_log.md)

**Summary:**
- Used **ChatGPT** to help organize proposal slides and initial README structure
- Used **Claude** to structure the notebook, suggest augmentation strategies, and assist with documentation
- All model architecture decisions, training runs, and result analysis are the student's own work
- Code attribution: ~65% written by student, ~35% AI-assisted

---

## 🔮 Future Improvements
1. Expand dataset to 1,000+ images across multiple currencies (USD, EUR, VND)
2. Add Grad-CAM heatmaps to highlight suspicious regions on the banknote
3. Deploy as a mobile app using TensorFlow Lite or ONNX export
4. Add a confidence threshold — flag uncertain predictions for human review

---

## 📚 References
1. He, K., Zhang, X., Ren, S., & Sun, J. (2016). *Deep Residual Learning for Image Recognition*. CVPR 2016.
2. Dataset: [Kaggle – Fake Currency Data by mdladla](https://www.kaggle.com/datasets/mdladla/fake-currency-data)
3. [PyTorch Documentation](https://pytorch.org/docs/)
4. [Torchvision Pretrained Models](https://pytorch.org/vision/stable/models.html)

---

## 📄 License
Academic Use Only — Houston Community College, ITAI 1378

## 🙏 Acknowledgments
- Professor for guidance throughout the semester
- Pretrained ResNet50 weights from [Torchvision / PyTorch](https://pytorch.org)
- Dataset provided by [mdladla on Kaggle](https://www.kaggle.com/datasets/mdladla/fake-currency-data)
- AI assistance from ChatGPT and Claude
