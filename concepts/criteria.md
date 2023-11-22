## Pruning Criteria





Network pruning can be
phrased as a form of neural architecture search. Such
an architecture search may involve training and evaluating
several random subnetworks based on leave-some-out approaches, but this can be quite expensive for large
models. More _efficient_ approaches assign an importance
score as pruning criteria, see following table. 



| Criteria                                                                                                       | Explanation                                                                                                |
|:---------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| <a href="https://arxiv.org/abs/1802.00124" style="color: black; text-decoration: black;">`Magnitude`</a>       | $L_1$ or $L_2$ norm of the weights                                                                         | 
| <a href="https://arxiv.org/abs/1906.10771" style="color: black; text-decoration: none;">`Taylor`</a>           | Taylor expansion including 1st or 2nd order _i.e.,_ Hessian information                                    |
| <a href="https://arxiv.org/abs/2306.11695" style="color: black; text-decoration: none;">`Wanda`</a>            | Importance score as the elementwise product between the weight magnitude and the norm of input activations |
| <a href="https://arxiv.org/abs/1811.00250" style="color: black; text-decoration: none;">`Geometric-Median`</a> | Consider the relationship between filters                                                                  | 
| <a href="https://arxiv.org/abs/1911.08114" style="color: black; text-decoration: none;">`KL-Divergence`</a>    | Kullback–leibler divergence to measure probability distributions                                           |
| <a href="https://arxiv.org/abs/2307.08483" style="color: black; text-decoration: none;">`Trainable`</a>        | Trainable importance score dynamically changes during training                                             |


