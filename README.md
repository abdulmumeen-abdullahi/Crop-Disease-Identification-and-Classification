# Crop Disease Identification and Classification
## 🔹 Problem Statement
Crop diseases are one of the key challenges faced by farmers between planting and harvesting. The cost of controlling these diseases increases significantly with time-early detection is essential to reduce losses and maximize yield. However, manually inspecting thousands of plants is infeasible, especially in large-scale farming operations. <br/>
This project addresses the need for early, automated detection and classification of crop diseases using computer vision. An EfficientNet-B3-based model is developed to accurately identify common diseases in five major crops with high performance in terms of accuracy, precision, and recall, while maintaining robustness against: <br/>
- Lighting, pose, and background variations
- Intra-class variability and inter-class similarity
- Generalization to unseen environments
The model identifies and classifies diseases in Wheat, Sugarcane, Corn, Rice, and Potato with over 94.8% accuracy, contributing toward smarter agriculture and aligning with the SDG 2 – Zero Hunger, SDG 12 – Responsible Consumption and Production, SDG 13 – Climate Action, etc  through AI.

## 🔹 Dataset Description
The project uses the Five Crop Diseases Dataset from [Kaggle](https://www.kaggle.com/datasets/shubham2703/five-crop-diseases-dataset): <br/>
- Total Images: 13,324
- Classes: 17
- Crops Covered: Corn, Potato, Rice, Wheat, Sugarcane
### Breakdown by Crop:
- Corn (3,852 images): Common Rust, Gray Leaf Spot, Northern Leaf Blight, Healthy
   - Source: PlantVillage Dataset
- Potato (2,152 images): Early Blight, Late Blight, Healthy
   - Source: PlantVillage Dataset
- Rice (4,078 images): Brown Spot, Leaf Blast, Neck Blast, Healthy
   - Sources: Dhan-Shomadhan Dataset, "Rice Leafs" Dataset
- Wheat (2,942 images): Yellow Rust, Brown Rust, Healthy
   - Source: "Wheat Disease Detection" Dataset from Kaggle
- Sugarcane (300 images): Red Rot, Bacterial Blight, Healthy
   - Source: "Sugarcane Disease Dataset" from Kaggle

## 🔹 Methodology
### 1. Data Preprocessing
- Loaded and organized dataset using ImageFolder.
- Displayed sample images and performed class-wise image counting.
- Computed dataset mean and standard deviation for normalization.
- Applied data augmentation (training set only) and normalization.
- Validation set was normalized without augmentation.
### 2. Model Training & Evaluation
- Model: EfficientNet-B3 (pretrained)
- Modifications: Replaced the classifier head with a linear layer (1536 → 17)
- Split: 80% training / 20% validation
- Training Setup:
   - Epochs: 50 (Early stopping at epoch 29)
   - Cross-validation: 5 folds
   - Framework: PyTorch
- Performance:
   - Accuracy: 94.8%
   - Precision: 95.4%
   - Recall: 94.5%
   - F1 Score: 94.8%
- Evaluation Metrics:
   - Confusion matrix revealed minimal class-wise misclassification.
   - Classification report and confusion matrix visualizations were generated.

## 🔹 Model Summary
- Total Parameters: 10,722,361
- Input Size: 69.12 MB
- Parameters Size: 42.54 MB
- Total Estimated Size: 12,312.78 MB

## 🔹 Real-World Applications
- Smart Farming: On-field disease detection via mobile or drone-based imaging.
- Crop Monitoring: Scalable disease surveillance across regions.
- Yield Optimization: Early intervention leads to reduced losses and improved yield.

## 🔹 Impacts
- Food Security: Enables farmers to proactively manage crop health, reducing crop loss.
- Sustainable Agriculture: Promotes efficient use of agrochemicals.
- Market Efficiency: Reduces post-harvest losses, benefiting supply chains and economies.

================================================== <br/>
Abdullahi Olalekan Abdulmumeen <br/>
Data Scientist | Computer Vision Engineer <br/>
olalekanabdulmumeen3@gmail.com <br/>
+2347053053024
