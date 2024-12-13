# BiTNet: AI for diagnosing ultrasound image

**BiTNet** is an AI system designed to detect abnormalities in the upper abdomen using ultrasound images. It reduces the workload of radiologists by assisting general practitioners in screening for cholangiocarcinoma and boosts their confidence in diagnosing over 25 abnormalities, including fatty liver, cirrhosis, and gallstones.

## Dataset

- **Source**: Ultrasound screening every 6 months for Isan cohort risk groups.
- **Image Count**: Each patient produces 11-15 ultrasound images.
- **Tele-Radiology**: Consultations with expert radiologists for validation.

### Data Preparation

- **Class Labels**: 14 abnormal classes + 1 normal class.
- **Data Distribution**:
  - **Train**: 366 abnormal cases (1,823 images) and 289 normal cases (3,434 images) totaling 5,257 images.
  - **Test**: 91 abnormal cases (455 images) and 71 normal cases (857 images) totaling 1,312 images.
- **Preprocessing**:
  - Remove background information (patient names, age, etc.).
  - Input image size: **456x456x3**.

### Data Augmentation

- **Horizontal Shift**
- **Vertical Shift**
- **Rotation**: up to 30°
- **Brightness Adjustment**
- **Shear Transformation**
- **Zoom**
- **No Flip**: Ultrasound anatomy has a fixed orientation.

## Model Development

**BiTNet (Biliary Tract Network)** is a custom model based on **EfficientNet-B5** with a modified architecture to include **Random Forests** for classification.

### Model Architecture

- **EfficientNet-B5**: Pre-trained on ImageNet, its early layers are frozen, and the later layers are fine-tuned for ultrasound image classification.
- **Customizations**:
  - Added Random Forest at the final classification layer.
  - Classifies 15 abnormalities and 5 viewing angles.

### Model Training Process

- **Pre-trained**: Use of ImageNet-pretrained EfficientNet-B5.
- **Freezing**: Freeze early convolutional layers; train final fully connected layers specific to the task.
- **Unfreezing**: Unfreeze layers and fine-tune.

## Applications

### 1. **Auto Pre-screening**

- **Objective**: Reduce the radiologist's workload by automatically filtering out normal images.

- **Workflow**: Sonographer inputs the image -> BiTNet pre-screens the image.
  - If the confidence for "Normal" is 100%, no further review is required.
  - If the image is flagged as "Abnormal", it is sent for review by a radiologist.

### 2. **Assisting Tool**

- **Objective**: Support general practitioners in diagnosing abnormalities before consulting radiologists.

- **Workflow**:
  - Input ultrasound image -> BiTNet assists through a web-based user interface.
  - Outputs include:
    - Classification (15 abnormalities + normal)
    - Prediction confidence
    - Model attention maps
    - Viewing angle
    - Top 3 suggestions

## Model Evaluation

### 1. **Independent Samples T-Test**

- **Objective**: Compare prediction confidence of BiTNet vs. EfficientNet.
- **Hypothesis**: The mean prediction confidence of BiTNet is significantly higher than EfficientNet.

### 2. **Paired Samples T-Test**

- **Objective 1**: Compare diagnostic performance (accuracy, precision, recall) with and without BiTNet assistance.
  - **Hypothesis**: Diagnostic performance with BiTNet assistance is significantly higher.
- **Objective 2**: Compare participant accuracy in the first and second rounds of testing.
  - **Hypothesis**: No significant difference in accuracy between rounds.
- **Objective 3**: Compare AI predictions with participant decisions (with and without BiTNet assistance).
  - **Hypothesis**: AI-assisted participants have higher agreement with final decisions.

### Performance Gains

- **Overall accuracy**: Increased by 18%.
- **General practitioner accuracy**: Increased by 26%.

## Visualization

- **Model Attention Maps**: Show which regions of the image contributed to the model's prediction.
- **Confidence Plots**: Visualize prediction confidence for normal vs. abnormal images.

## Summary

- The first AI system in the world that screens CCA via ultrasound image.
- Diagnose 25 abnormalities in the human upper abdominal.
- Currently used in Srinagarind Hospital and 205 Affiliated hospitals.
- Cloud-based AI Services.

## Future Work

- **Bigger and Better**: Development of BiTNet V2 with more robust training on the expanded dataset.
- **Expanded Dataset**:

  - 25,676 cases
  - 228,177 images
  - 10 years of historical data
