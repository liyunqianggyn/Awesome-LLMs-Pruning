##  Useful Concepts  

### Outliers in LLMs

One  intriguing trait of LLMs is the exhibition of outlier features, which are the features with significantly
larger magnitudes than others. The paper of [OWL](https://arxiv.org/abs/2310.05175) claims to preserve outlier features.
Recent paper [Quantizable Transformer](https://arxiv.org/abs/2306.12929) finds that the outliers are related to softmax function in attention. See [blog](https://www.evanmiller.org/attention-is-off-by-one.html) for more details.


### Scaling laws
Increasing
model size or data brings _consistent_ performance improvements, even at very large scale. And this scaling behavior can be predictable by simple [power-law](https://arxiv.org/abs/2001.08361) curves. 
