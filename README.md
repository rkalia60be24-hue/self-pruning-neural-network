# Self-Pruning Neural Network

## Overview

This project implements a self-pruning neural network where the model learns which weights are important during training itself.

Instead of pruning the network after training, each weight is associated with a learnable gate. These gates control whether a weight contributes to the output or gets effectively removed. This helps in reducing unnecessary parameters while still maintaining good performance.

---

## Approach

* Each weight in the network has a corresponding **gate score**

* These gate scores are passed through a **sigmoid function** to convert them into values between 0 and 1

* The final weight used during computation is:

  weight × gate

* If a gate value becomes close to 0, that weight is effectively pruned

To encourage the model to remove unnecessary weights, an additional penalty is added during training.

---

## Loss Function

Total Loss = Classification Loss + λ × Sparsity Loss

* Classification Loss: CrossEntropyLoss for prediction accuracy
* Sparsity Loss: Sum of all gate values (L1 penalty)

The λ (lambda) value controls how aggressively the model prunes weights.

# Results

| Lambda | Accuracy | Sparsity |
| ------ | -------- | -------- |
| 0.001  | 38.51%   | 0.01%    |
| 0.01   | 37.65%   | 0.01%    |
| 0.1    | 37.40%   | 0.01%    |


# Observations

- The sparsity level remains extremely low (~0.01%) for all values of λ
- This suggests that the model is not effectively learning to prune weights

- Increasing λ slightly reduces accuracy, but does not increase sparsity
- This indicates that the sparsity regularization is not strong enough to push gate values towards zero

- Ideally, higher λ should result in higher sparsity, but this trend is not observed here
- This could be due to:
  - Gate values not reaching sufficiently low values after sigmoid
  - λ being too small to influence training significantly
  - The threshold used to calculate sparsity being too strict

Overall, the current model behaves more like a standard neural network rather than a self-pruning one, and further tuning is required to achieve meaningful sparsity.

## How to Run

1. Install dependencies:

   pip install -r requirements.txt

2. Run training:

   python train.py




This implementation focuses on understanding how sparsity can be introduced during training instead of as a separate step. It also shows how regularization can influence model structure dynamically.
