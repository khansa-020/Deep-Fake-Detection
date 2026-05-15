# Deep-Fake-Detection
Comparative analysis of ML and DL techniques for Deep Fake Detection using efficientNetB3 as framework or baseline
| Model                     | Pretrained     | Fine-tuned | Hybrid    | Notes                 |
| ------------------------- | -------------- | ---------- | --------- | --------------------- |
| Simple CNN                | No             | No         | No        | Basic baseline        |
| InceptionV3               | Yes (ImageNet) | Yes        | No        | Transfer learning     |
| InceptionV3 + DenseNet121 | Yes            | Yes        | Yes       | Feature fusion hybrid |
| EfficientNet-B3           | Yes (ImageNet) | Yes        | No        | Proposed final model  |


# detail
It compares several **Deep Learning (DL)** models for DeepFake detection.

1. **Which DL models were used**
2. **Which pretrained backbone was used**
3. **How fine-tuning was done**
4. **Whether models were standalone or hybrid/combined**
5. **Which model is the baseline**
6. **Implementation details for each model**

---

# Deep Learning Techniques Used

| DL Technique              | Pretrained Backbone             | Fine-tuning / Transfer Learning | Combination Type                    | Accuracy |
| ------------------------- | ------------------------------- | ------------------------------- | ----------------------------------- | -------- |
| EfficientNet-B3           | ImageNet pretrained             | Yes                             | Single model                        | 97.95%   |
| InceptionV3 + DenseNet121 | Both pretrained on ImageNet     | Yes                             | Hybrid / combined architecture      | 90.5%    |
| InceptionV3-based model   | ImageNet pretrained             | Yes                             | Single model with transfer learning | 91.47%   |
| Simple CNN                | No pretrained weights mentioned | Trained from scratch            | Single shallow CNN                  | 89.59%   |

---

# 1. EfficientNet-B3 (Main Proposed Model)

## Model Type

* Deep CNN architecture
* Transfer learning based

## Pretrained On

* ImageNet dataset

## Fine-Tuning Strategy

The paper clearly states:

* Initially lower layers were frozen
* Higher/deeper layers were unfrozen later
* Fine-tuning focused on DeepFake-specific artifacts

This is standard staged transfer learning.

---

## Architecture Details

The original EfficientNet-B3 classifier was replaced with a custom binary head:

### Custom Head

Input Features → FC(128) → ReLU → Dropout(0.3)
→ FC(64) → ReLU → Dropout(0.2)
→ FC(1) → Sigmoid

---

## Training Configuration

| Parameter     | Value                |
| ------------- | -------------------- |
| Input size    | 224×224              |
| Optimizer     | Adam                 |
| Learning rate | 0.0001               |
| Loss          | Binary Cross Entropy |
| Batch size    | 8                    |
| Epochs        | 10                   |
| Activation    | Sigmoid              |
| Framework     | PyTorch + timm       |

---

## Data Augmentation

Training images:

* Random horizontal flip
* Random rotation (±30°)
* Resize
* Normalize

Validation/Test:

* Resize only
* Normalize only

---

## Why It Performed Best

EfficientNet-B3:

* Uses compound scaling
* Uses depthwise separable convolutions
* Uses squeeze-and-excitation blocks
* Better feature extraction with fewer parameters

It achieved:

* 97.95% test accuracy
* 98.08% peak accuracy at 3K images
* 100% on unseen ChatGPT/Gemini generated images

---

# 2. InceptionV3 + DenseNet121 (Hybrid Model)

## Model Type

Combined / hybrid deep architecture

## Pretrained On

Most likely:

* InceptionV3 pretrained on ImageNet
* DenseNet121 pretrained on ImageNet

(The paper implies transfer learning usage.)

---

## Combination Strategy

The paper does NOT provide exact implementation, but from wording:

> “InceptionV3 and DenseNet121 hybrid model”

This usually means:

### Likely Architecture

Feature Extraction:

* InceptionV3 branch
* DenseNet121 branch

Then:

* Concatenate extracted features
* Fully connected classifier
* Binary output layer

---

## Possible Flow

Input Image
↓
InceptionV3 Features
+
DenseNet121 Features
↓
Feature Fusion / Concatenation
↓
Dense Layers
↓
Sigmoid Output

---

## Fine-Tuning

Likely:

* Pretrained weights loaded
* Top layers retrained
* Final classification head modified

---

## Accuracy

* 90.5%

---

# 3. InceptionV3-based Transfer Learning Model

## Model Type

Single pretrained CNN

## Pretrained On

* ImageNet

## Fine-Tuning

Explicitly mentioned:

* Transfer learning
* Fine-tuning

---

## Likely Implementation

Base:

* InceptionV3 pretrained backbone

Modification:

* Replace final softmax layer
* Add binary classifier head

Typical setup:

GlobalAveragePooling
→ Dense Layer
→ Dropout
→ Sigmoid

---

## Accuracy

* 91.47%

---

## Why Better Than Hybrid

The paper says:

* Fine-tuned pretrained weights improved performance
* Deep semantic learning improved DeepFake detection

---

# 4. Simple CNN Model

## Model Type

Basic CNN trained from scratch

## Pretraining

* No pretrained weights mentioned

## Architecture

The exact layers are not provided.

Likely included:

* Conv layers
* MaxPooling
* Flatten
* Dense layers
* Sigmoid output

---

## Characteristics

Shallow architecture:

* Lower feature extraction capability
* Poorer semantic understanding
* Less robust to complex forgery artifacts

---

## Accuracy

* 89.59%

---

# Which Model is the Baseline?

The paper does not explicitly say “baseline,” but practically:

| Baseline Type           | Model               |
| ----------------------- | ------------------- |
| Traditional ML baseline | GLCM + RandomForest |
| DL baseline             | Simple CNN          |
| Main proposed model     | EfficientNet-B3     |

So:

* **Simple CNN** acts as the DL baseline
* **EfficientNet-B3** is the proposed advanced model

---

# Overall DL Comparison

| Model                     | Pretrained     | Fine-tuned | Combined? | Notes                 |
| ------------------------- | -------------- | ---------- | --------- | --------------------- |
| Simple CNN                | No             | No         | No        | Basic baseline        |
| InceptionV3               | Yes (ImageNet) | Yes        | No        | Transfer learning     |
| InceptionV3 + DenseNet121 | Yes            | Yes        | Yes       | Feature fusion hybrid |
| EfficientNet-B3           | Yes (ImageNet) | Yes        | No        | Proposed final model  |

---

# Best Performing Model

## EfficientNet (EfficientNet-B3)

### Why best:

* Efficient scaling
* Strong semantic representation
* Lower parameter count
* Better generalization
* Strong transfer learning capability

### Final Performance:

* 97.95% overall accuracy
* 98.08% peak accuracy
* 100% on unseen AI-generated images

---

# Likely Actual Implementation Pipeline

## Proposed EfficientNet-B3 Workflow

```text
Input Image
↓
Resize (224×224)
↓
Augmentation
↓
Normalization
↓
EfficientNet-B3 Backbone
(pretrained on ImageNet)
↓
Feature Extraction
↓
FC(128) + ReLU + Dropout
↓
FC(64) + ReLU + Dropout
↓
FC(1) + Sigmoid
↓
Real / Fake Prediction
```

---

# Important Observation

The paper gives:

* Complete implementation details only for EfficientNet-B3
* Partial details for InceptionV3 and hybrid model
* Minimal details for Simple CNN

So:

* EfficientNet-B3 is the actual proposed architecture
* Other DL models are comparative baselines/benchmarks
# Author
KHANSA
