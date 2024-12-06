## Pruning Criteria





Network pruning can be
phrased as a form of neural architecture search. Such
an architecture search may involve training and evaluating
several random subnetworks based on leave-some-out approaches, but this can be quite expensive for large
models. More _efficient_ approaches assign an importance
score as pruning criteria, see following table. 



| Criteria                                                                                                       | Explanation                                                                                                                                                                                                                                                             |
|:---------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a  href="https://arxiv.org/abs/1802.00124" style="color: black; text-decoration: black;">`Magnitude`</a>      | $L_1$ or $L_2$ norm of the weights                                                                                                                                                                                                                                      | 
| <a href="https://arxiv.org/abs/1906.10771" style="color: black; text-decoration: none;">`Taylor`</a>           | Taylor expansion including 1st or 2nd order _i.e.,_ Hessian information                                                                                                                                                                                                 |
| <a href="https://arxiv.org/abs/2306.11695" style="color: black; text-decoration: none;">`Wanda`</a>            | Importance score as the elementwise product between the weight magnitude and the norm of input activations  $\mid W_{ij} \mid  \times \parallel X_i\parallel_2$                                                                                                         |
| <a href="https://openreview.net/pdf?id=Tr0lPx9woF" style="color: black; text-decoration: none;">`RIA`</a>      | Relative Importance and Activations $\left(\frac{\mid W_{i j}\mid}{\sum\mid W_{* j}\mid}+\frac{\mid W_{i j}\mid}{\sum\mid W_{i *}\mid}\right) \times\left(\parallel X_i\parallel_2\right)^a$                                                                            |
| <a href="https://arxiv.org/abs/1811.00250" style="color: black; text-decoration: none;">`Geometric-Median`</a> | Consider the relationship between filters                                                                                                                                                                                                                               | 
| <a href="https://arxiv.org/abs/1911.08114" style="color: black; text-decoration: none;">`KL-Divergence`</a>    | Kullback–leibler divergence to measure probability distributions                                                                                                                                                                                                        |
| <a href="https://arxiv.org/abs/2402.02834" style="color: black; text-decoration: none;">`Perplexity (PPL)`</a> | Remove each Transformer block and monitor its influence on PPL: $I_{\mathrm{PPL}}^n = \exp \left( -\frac{1}{S L} \sum_s \sum_l \log p_{\theta^n}\left(x_l^{(s)} \mid x_{<l}^{(s)}\right) \right)$  derived from the next-token prediction loss, only forward pass required |
| <a href="https://arxiv.org/pdf/2403.03853" style="color: black; text-decoration: none;">`Block Influence`</a>  | cosine similarity between input state and output state  to measure the degree of transformation performed by each layer: $\[\text{BI}_i = 1 - E_{X, t} \left( \frac{X_{i, t}^T X_{i+1, t}}{\mid X_{i, t} \mid_2 \mid X_{i+1, t} \mid_2} \right),\]$               |
| <a href="https://arxiv.org/abs/2307.08483" style="color: black; text-decoration: none;">`Trainable`</a>        | Trainable importance score dynamically changes during training                                                                                                                                                                                                          |
