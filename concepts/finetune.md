## Retrain or Fine-tune

LLMs require expensive memory and computing for training, which is a challenge for retraining or fine-tuning in pruning.
We divide the retraining of pruned LLMs  into three categories based on the number of parameters updated during pruning.

| Retrain     | Explanation                                                           |
|-------------|-----------------------------------------------------------------------|
| `Without`   | No retrain or fine-tuning during pruning.                             |
| `Efficient` | Parameter-efficient fine-tuning techniques by updating few parameters | 
| `Extensive` | Update all parameters                                                 |




