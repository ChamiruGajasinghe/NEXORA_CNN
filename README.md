# NEXORA_CNN

EN3150 - Pattern Recognition  
Assignment 03

## Project Overview

This project focuses on image classification using Convolutional Neural Networks (CNNs) for low-resource and edge devices.

The project uses the **RealWaste** image dataset from the UCI Machine Learning Repository.

The same dataset split and preprocessing were used across the models so that the results could be compared fairly.

## Dataset

**Dataset:** RealWaste  
**Source:** UCI Machine Learning Repository

The dataset contains **4,752 images** from **9 classes**:

- Cardboard
- Food Organics
- Glass
- Metal
- Miscellaneous Trash
- Paper
- Plastic
- Textile Trash
- Vegetation

## Data Preparation

- Image size: **64 x 64 RGB**
- Training set: **70%**
- Validation set: **15%**
- Test set: **15%**
- Random seed: **42**
- Batch size: **32**
- Pixel values are normalized to the range **0 to 1**
- Stratified splitting is used to keep the class distribution similar between the three sets

The shared data preparation is available in:

`Data_preparation.ipynb`

## Custom Models

### Model A - Standard CNN

Model A is a standard CNN using normal 2D convolution and max-pooling layers.

- Three convolution layers with 16, 32 and 64 filters
- 3 x 3 convolution kernels
- ReLU activation
- 2 x 2 max pooling
- Dense layer with 64 units
- 9-class Softmax output
- Trainable parameters: **286,377**

Notebook:

`Kushen_ModelA.ipynb`

### Model B - Lightweight CNN

Model B is designed for low-resource devices using depthwise separable convolutions.

- Standard convolution stem
- Four depthwise separable convolution blocks
- Batch Normalization
- ReLU6 activation
- Global Average Pooling
- Dense layer with 64 units
- 9-class Softmax output
- Trainable parameters: **64,617**

Model B remains below the assignment limit of **100,000 trainable parameters**.

Notebook:

`Dumindu_ModelB.ipynb`

## Optimizer Selection and Model Evaluation

The following optimizers were compared using Model A:

- SGD
- SGD with Momentum
- Adam

Adam with a learning rate of **0.001** gave the best validation result and was selected for the final common training.

Fresh versions of Model A and Model B were then trained using the same training setup for a fair comparison.

The evaluation includes:

- Training and validation accuracy
- Training and validation loss
- Test accuracy
- Precision
- Recall
- F1-score
- Confusion matrices
- Training time
- Parameter comparison

Notebook:

`Lochana_Training_Evaluation.ipynb`

## Pretrained Models

Two lightweight pretrained models were also tested using transfer learning:

- MobileNetV2
- MobileNetV3Small

Both models used ImageNet pretrained weights and were trained using a two-stage approach:

1. Train the new classification head while the pretrained backbone is frozen.
2. Fine-tune part of the pretrained backbone using a smaller learning rate.

The pretrained models were evaluated using the same RealWaste data split and compared with Model B using accuracy, model size, parameter count and computational cost.

Notebook:

`Chamiru_Pretrained_Models.ipynb`

## Group Members and Contributions

### Kushen

- Data preparation
- Model A - Standard CNN

Branch:

`kushen-modelA`

### Dumindu

- Model B - Lightweight CNN
- Depthwise separable convolutions
- Parameter and computational-cost analysis

Branch:

`dumindu-modelB`

### Lochana

- Optimizer comparison
- Common Model A and Model B training
- Model evaluation
- Accuracy, precision, recall and F1-score
- Training and validation curves
- Confusion matrices

Branch:

`lochana-training`

### Chamiru

- MobileNetV2
- MobileNetV3Small
- Transfer learning and fine-tuning
- Pretrained-model evaluation
- Final comparison with Model B

Branch:

`chamiru-230191N`

## GitHub Workflow

The `main` branch contains the completed project work.

Each member worked on a separate branch for their assigned section.

The general workflow was:

1. Start from the latest `main` branch.
2. Work on an individual branch.
3. Make regular and meaningful commits.
4. Create a pull request after completing the assigned work.
5. Review the changes before merging them into `main`.

This workflow was used to keep each member's contributions separate and maintain a clear development history.

## Repository Structure

```text
NEXORA_CNN/
│
├── Data_preparation.ipynb
├── Kushen_ModelA.ipynb
├── Dumindu_ModelB.ipynb
├── Lochana_Training_Evaluation.ipynb
├── Chamiru_Pretrained_Models.ipynb
└── README.md
