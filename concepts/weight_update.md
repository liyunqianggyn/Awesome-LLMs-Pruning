## Weight Update

Updating the pretrained LLMs' weights can come in different forms, such as
* retraining: during pruning, retrain or fine-tune on datasets to minimize training loss.
* minimize reconstruction error: updating weights by minimizing reconstruction pruning error between non-pruned and pruned models, without any retraining. For example, [*SparseGPT*](https://arxiv.org/abs/2301.00774) updates weights by solving a layer-wise reconstruction error, without retraining.

| Retrain     | Explanation                                                                                                                                                                                                      |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Frozen`    | Pre-trained weights of LLMs keep fixed.                                                                                                                                                                          |
| `Update`    | Update the weights by retraining or minimize reconstruction error.  | 



