# Color Object Detection

A color-based object classification system developed for the fictional KHILONA toy factory to automate the sorting of plastic objects according to their colors.

The system classifies objects into three categories:

- Blue → Belt A
- Yellow → Belt B
- Purple → Belt C

## Project Overview

This project uses a custom Convolutional Neural Network (CNN) trained completely from scratch. The system combines learned visual features from the CNN with handcrafted color features extracted from RGB and HSV color spaces.

The project was developed under the following constraints:

- No public dataset
- No pretrained models
- No ImageNet or transfer learning
- No data augmentation
- No rule-based `if/else` classification

## Dataset

The dataset was manually created for this project.

Initially, the dataset contained 432 images. After duplicate removal, 429 images remained.

| Class | Images |
|-------|--------|
| Blue | 175 |
| Yellow | 154 |
| Purple | 100 |
| **Total** | **429** |

Duplicate images were detected and removed during dataset cleaning.

## Preprocessing

Images were processed using a deterministic ResizePad procedure:

- Images resized to 128 × 128 pixels
- Aspect ratio preserved
- Padding used where required
- No data augmentation

## Color Feature Extraction

The system extracts 24 handcrafted color features:

- RGB mean and standard deviation: 6 features
- HSV mean and standard deviation: 6 features
- Hue histogram: 12 features

These color features are combined with CNN-learned visual features before classification.

## Model Architecture

The main model is a custom CNN called:

`ColorAwareScratchCNN`

The architecture contains:

- Convolutional layers
- Normalization
- Activation functions
- Pooling
- Dropout
- Global Average Pooling
- Color feature processing MLP
- Feature fusion
- Final 3-class classifier

The model was trained from scratch without using pretrained networks.

## Training Strategy

The project uses:

- Stratified holdout test split
- 5-fold stratified cross-validation
- Class-weighted loss
- Early stopping
- Learning-rate scheduling
- Label smoothing
- Dropout
- Weight decay

The final test set was kept untouched during model development.

## Results

### Cross-Validation

- Mean Validation Accuracy: **94.24%**
- Mean Validation Macro F1: **0.9399**

### Final Ensemble Test Performance

- Test Accuracy: **86.15%**
- Test Macro F1: **0.8631**
- Test Weighted F1: **0.8613**

## Confusion Matrix

The model successfully classified samples from all three classes, with some confusion between visually similar color categories.

## Technologies Used

- Python
- PyTorch
- NumPy
- Pandas
- Matplotlib
- Scikit-learn
- OpenCV
- PIL
- ImageHash


├── requirements.txt
├── .gitignore
└── LICENSE
