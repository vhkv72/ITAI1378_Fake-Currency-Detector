# ITAI1378_Fake-Currency-Detector
**Name:** Vy Vo
**Course:** ITAI 1378
**Project Tier:** Tier 1

## Problem Statement
Counterfeit money can cause financial loss for businesses and individuals. Small businesses often do not have advanced tools to check whether a banknote is real or fake. This project aims to build a practical image classification system to help detect fake currency.

## Solution Overview
This project will build a computer vision model that predicts whether a banknote is real or fake from an input image. The system will process the image and return a simple classification result for users.

## Technical Approach
- **CV Technique:** Image Classification
- **Model:** ResNet50
- **Framework:** PyTorch
- **Why this approach:** ResNet50 is strong for image classification, and transfer learning works well when the dataset is not very large.

## Dataset Plan
- **Source:** Kaggle Fake Currency Data
- **Link:** https://www.kaggle.com/datasets/mdladla/fake-currency-data
- **Labels:** Real, Fake
- **Preparation:** Resize images, normalize, clean data if needed, and split into train/validation/test sets

## Success Metrics
- **Primary Metric:** Accuracy
- **Target:** 90% or higher
- **Secondary Metrics:** Precision, Recall, Inference speed under 1 second per image

## Week-by-Week Plan
- **Week 10:** Get dataset and set up environment
- **Week 11:** Train initial model
- **Week 12:** Evaluate and improve model
- **Week 13:** Create demo notebook
- **Week 14:** Final testing and documentation
- **Week 15:** Final presentation

## Resources Needed
- **Compute:** Google Colab
- **Frameworks:** PyTorch, Torchvision
- **Estimated Cost:** $0

## Risks & Mitigation

| Risk | Probability | Mitigation |
|------|-------------|------------|
| Low accuracy | Medium | Use data augmentation and tune hyperparameters |
| Small dataset | Medium | Apply transfer learning and augmentation |
| Data quality issues | Low | Remove unclear or duplicate images |

## AI Usage Log
- Used ChatGPT to help organize the proposal slides and GitHub README.
