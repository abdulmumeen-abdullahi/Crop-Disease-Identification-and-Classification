# 🌿 Crop Disease Detection Model (EfficientNet-B3)

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white) ![Hugging Face](https://img.shields.io/badge/Model_Weights-Hugging_Face-yellow?style=for-the-badge&logo=huggingface) ![Accuracy](https://img.shields.io/badge/Accuracy-94.8%25-success?style=for-the-badge) ![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

## 📋 Executive Summary
This repository contains the training pipeline and inference logic for a **computer vision model** designed to detect 17 different crop diseases across 5 major food crops (Wheat, Sugarcane, Corn, Rice, Potato).

Built on the **EfficientNet-B3** architecture, this model achieves **94.8% test accuracy** and is optimized for deployment in resource-constrained AgTech environments (e.g., mobile edge devices).

**🔗 [Download Pre-trained Weights (Hugging Face)](https://huggingface.co/VisionaryQuant/5_Crop_Disease_Detection/tree/main)**

---

## 📊 Model Performance

| Metric | Score | Notes |
| :--- | :--- | :--- |
| **Accuracy** | **94.8%** | Tested on 2,600+ unseen validation images |
| **Precision** | 95.4% | Minimizes false positives |
| **Recall** | 94.5% | Minimizes missed disease detection |
| **Inference Time** | ~45ms | Tested on standard GPU |

### ⚠️ Constraints & Known Limitations
While the model achieves **99-100% accuracy** on distinct classes (e.g., *Corn Rust*, *Potato Early Blight*), it faces challenges with:
* **Rice Brown Spot vs. Rice Leaf Blast:** Due to high visual similarity (small brown lesions), confusion exists between these two classes (approx. 77% precision).
* **Mitigation:** In production, this model should be paired with a secondary "Expert Model" specifically for Rice leaf pathology if higher granularity is required.

---

## 🛠️ Technical Implementation

* **Architecture:** EfficientNet-B3 (Pre-trained on ImageNet).
* **Modifications:** Custom fully connected head (1536 inputs → 17 outputs).
* **Input Resolution:** 300x300 pixels.
* **Augmentation:** RandomRotation, HorizontalFlip, ColorJitter (to simulate field lighting).

---

## 🚀 How to Run Inference

**1. Setup Environment**
- #### Clone the Git Repo
```bash
git clone https://github.com/abdulmumeen-abdullahi/Crop-Disease-Identification-and-Classification.git
```
- #### Go to the project git folder
```
cd crop-disease-detection
```
- #### Install the requirements
```
pip install -r requirements.txt
```

**2. Download Weights**
Download `best_crop_disease_model.pt` from my [Hugging Face Repository](https://huggingface.co/VisionaryQuant/5_Crop_Disease_Detection/tree/main) and place it in the root directory.

**3. Run Prediction (Python Snippet)**
Since the repository currently focuses on the training notebook, use this script to load the model for inference:

```python
import torch
from torchvision import models
import torch.nn as nn
from PIL import Image
from torchvision import transforms
```

**4. Define Architecture**
```
def get_model():
    model = models.efficientnet_b3(weights=None)
    # Re-create the classifier head to match training
    model.classifier[1] = nn.Linear(1536, 17) 
    return model
```

**5. Load Weights**
```
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model = get_model()
model.load_state_dict(torch.load('best_crop_disease_model.pt', map_location=device))
model.eval()
```

# 6. Preprocess & Predict
```
def predict(image_path):
    transform = transforms.Compose([
        transforms.Resize((300, 300)),
        transforms.ToTensor(),
        transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])
    ])
    
    img = Image.open(image_path).convert("RGB")
    img_tensor = transform(img).unsqueeze(0)
    
    with torch.no_grad():
        outputs = model(img_tensor)
        _, predicted = torch.max(outputs, 1)
        
    return predicted.item()
```

**Example Usage**
```
print(f"Predicted Class ID: {predict('test_leaf.jpg')}")
```

## 📂 Repository Structure

```text
├── crop-disease-detection.ipynb   # Full training pipeline (Data loading, Training, Eval)
├── requirements.txt               # Dependencies (torch, torchvision, pillow, etc.)
└── README.md                      # Documentation
```

## Impact
This model was developed to support UN SDG 2 (Zero Hunger) by enabling early intervention in crop disease management. It serves as the vision backend for the FarmConsultAI platform.
