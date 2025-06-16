# CNN Hyperparameter Tuning Report

## Overview
This report summarizes the process and results of tuning hyperparameters for a convolutional neural network (CNN) model trained on the CIFAR-10 dataset using PyTorch.

## Optimizer & Learning Rate Tuning
We compared two optimizers: **Adam** and **SGD**, testing each across multiple learning rates. Results are shown below:

| Optimizer | Learning Rate | Accuracy (%) |
|-----------|----------------|--------------|
| Adam      | 0.1            | 10           |
|           | 0.01           | 10           |
|           | 0.001          | 67           |
|           | 0.0001         | 55           |
| SGD       | 0.1            | 60           |
|           | 0.01           | 56           |
|           | 0.001          | 28           |
|           | 0.0001         | 12           |

The best performance was obtained using the **Adam optimizer** with a learning rate of **0.001**, achieving **67% accuracy**.

## Convolutional Layer Tuning
We adjusted the number of filters for each convolutional layer, testing several combinations:

| Setup | Conv1 | Conv2 | Conv3 | Parameters | Accuracy (%) |
|-------|--------|--------|--------|------------|---------------|
| 1     | 3→10  | 10→30  | 30→50  | -          | 67            |
| 2     | 3→10  | 10→20  | 20→30  | -          | 66            |
| 3     | 3→10  | 10→30  | 30→40  | -          | 66            |
| 4     | 3→15  | 15→30  | 30→60  | -          | 67            |
| 5     | 3→22  | 22→38  | 38→75  | 292,129    | 69            |
| 6     | 3→25  | 25→50  | 50→100 | 402,260    | 68            |

The best result was **69% accuracy** with configuration **5**, which used the structure `3→22→38→75`.

## Kernel Size & Padding Tuning
We tested two different strategies for kernel size and corresponding padding:

| Kernel Sizes | Paddings | Accuracy (%) |
|--------------|----------|--------------|
| 7, 5, 3      | 3, 2, 1  | 69           |
| 3, 3, 3      | 1, 1, 1  | **71**       |

Using a **consistent kernel size of 3×3 with padding 1 across all layers** gave the best result, reaching **71% accuracy**.

## Summary
We tuned hyperparameters in the following order:
1. **Optimizer + Learning Rate**
2. **Convolutional Filter Sizes**
3. **Kernel Sizes and Padding**

Each step was tested individually before moving on to the next, ensuring accurate comparisons and clear improvements. Final configuration reached **71% accuracy**, improving from an initial 10%.

## Visualizations

### Tuning Strategy
![Tuning Strategy](1AB9F47B-49AB-4229-B914-2B56504E6070.png)

### Training Loss Interpretation
![Training Loss](0144458D-1AAF-4D5C-91D3-541AB668D49A.png)