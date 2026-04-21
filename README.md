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

## Observations

- The sparsity level remains almost constant (~0.01%) across all values of λ
- This indicates that the model is not effectively pruning weights during training
- Even when λ is increased, the gate values are not being pushed close to zero

- The accuracy decreases slightly as λ increases, but without any meaningful gain in sparsity
- This suggests that the sparsity regularization is not strong enough or not influencing the gates properly

- Possible reasons could be:
  - λ value is too small to impact training
  - Gate values (after sigmoid) are not reaching very low values
  - The threshold used to measure sparsity might be too strict

Overall, the current setup does not show a strong sparsity vs accuracy trade-off, and further tuning is needed to achieve effective pruning.


## How to Run

1. Install dependencies:

   pip install -r requirements.txt

2. Run training:

   python train.py


## Notes

This implementation focuses on understanding how sparsity can be introduced during training instead of as a separate step. It also shows how regularization can influence model structure dynamically.
