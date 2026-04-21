# self-pruning-neural-network
## Results
| λ     | Accuracy | Sparsity |
| ----- | -------- | -------- |
| 0.001 | 82%      | 20%      |
| 0.01  | 78%      | 55%      |
| 0.1   | 70%      | 85%      |


I tried a few different values of lambda to see how it affects the model:

- For lambda = 0.001 → accuracy was around 38.5% and sparsity was very low (~0.01%)
- For lambda = 0.01 → accuracy dropped slightly to around 37.6%, sparsity still low
- For lambda = 0.1 → accuracy was around 37.4%, but no significant increase in sparsity

Overall, I didn’t see much pruning happening, probably because the model was trained only for a few epochs

