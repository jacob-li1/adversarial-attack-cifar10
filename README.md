# Adversarial Attacks on CIFAR-10

This project implements several adversarial attack methods on image classifiers trained on the CIFAR-10 dataset using PyTorch.

We evaluate the robustness of a target model against different gradient-based adversarial attacks and an ensemble attack.

---

# Dataset

A subset of the CIFAR-10 dataset is used.

- 10 classes
- 20 images per class
- Total: **200 images**

Classes include:

- airplane
- automobile
- bird
- cat
- deer
- dog
- frog
- horse
- ship
- truck

---

# Models

Pretrained models from **pytorchcv** are used.

### Target model

- **ResNet110**

### Surrogate models (for transfer attack)

- ResNet56
- DenseNet40_k12
- WideResNet28-10

The surrogate models are used to generate transferable adversarial examples.

---

# Attack Methods

We implement the following adversarial attack algorithms.

### FGSM

Fast Gradient Sign Method:

\[
x_{adv} = x + \epsilon \cdot sign(\nabla_x L(x,y))
\]

---

### I-FGSM

Iterative version of FGSM with multiple small updates.

---

### PGD

Projected Gradient Descent attack with iterative updates and projection into the ε-ball.

---

### Ensemble Attack

Instead of attacking a single model, gradients from multiple surrogate models are combined to generate adversarial examples.

This improves **transferability** to the target model.

---

# Benign Performance

Performance of the target model (ResNet110) on clean images:

| Model | Accuracy | Loss |
|------|------|------|
| ResNet110 | **0.95000** | 0.22678 |

---

# FGSM Attack Results

| Model | Accuracy | Loss |
|------|------|------|
| ResNet56 | 0.65000 | 1.88393 |
| DenseNet40 | 0.65000 | 1.85999 |
| WRN28 | 0.74000 | 1.39888 |

---

# I-FGSM Attack Results

| Model | Accuracy | Loss |
|------|------|------|
| ResNet56 | 0.32000 | 4.52877 |
| DenseNet40 | 0.64000 | 1.87941 |
| WRN28 | 0.67500 | 1.78542 |

---

# PGD Attack Results

| Model | Accuracy | Loss |
|------|------|------|
| ResNet56 | 0.43000 | 3.67697 |
| DenseNet40 | 0.66000 | 1.72951 |
| WRN28 | 0.66500 | 1.83135 |

---

# Ensemble Attack Results

| Attack | Accuracy | Loss |
|------|------|------|
| Ensemble | **0.29000** | 4.99305 |

The ensemble attack produces stronger adversarial examples and significantly reduces model accuracy.

---

# Implementation

The project is implemented using **PyTorch**.

Main components include:

- loading pretrained models from `pytorchcv`
- generating adversarial examples
- evaluating model performance

---

# Requirements
## Discussion

From the experimental results we observe:

- Iterative attacks (I-FGSM, PGD) are generally stronger than single-step attacks such as FGSM.
- Adversarial examples generated from surrogate models can transfer to other architectures.
- The ensemble attack significantly reduces model accuracy, demonstrating improved attack transferability.
- ## Repository Structure

```
.
├── hw10_adversarial_attack.ipynb
├── data/
├── images/
└── README.md
```
