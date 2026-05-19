##  Useful Concepts  

### Outliers in LLMs

One  intriguing trait of LLMs is the exhibition of outlier features, which are the features with significantly
larger magnitudes than others. The paper of [OWL](https://arxiv.org/abs/2310.05175) claims to preserve outlier features.
Recent paper [Quantizable Transformer](https://arxiv.org/abs/2306.12929) finds that the outliers are related to softmax function in attention. See [blog](https://www.evanmiller.org/attention-is-off-by-one.html) for more details.


### Scaling laws
Increasing
model size or data brings _consistent_ performance improvements, even at very large scale. And this scaling behavior can be predictable by simple [power-law](https://arxiv.org/abs/2001.08361) curves. 

### Layer or Depth pruning
Layer pruning is a technique to remove entire layers from the model. It is a coarse-grained pruning method, which may be very effective in some cases.

- Dimensional Mismatch Problem:  When pruning intermediate layers, the input and output dimensions of subsequent layers may no longer match. 
- Current LLMs Layer Pruning: Transformer blocks have the exactly same dimension of input  and output due to the residual connection. Thus, layer pruning is feasible for LLMs.
 Did not suit for situation when mismatch between new input and old input, such as VGG layer pruning.
<div align="left"><figcaption></figcaption><img src='./figs/Status_Layer_Pruning.png' width=850 alt=''> </img></div> 

In contrast, width pruning is a fine-grained pruning method, which removes channels or neurons from each layer. 

### Expert merge (MoE pruning)

In a MoE block, each **expert** is a small sub-network (typically a SwiGLU MLP with its own weights). **Expert merge** compresses the MoE by combining several experts into fewer experts, instead of only zeroing or dropping them.

- **Same-shape requirement:** Experts in a layer share the same input/output dimensions, so their weights live in the same tensor shape and can be blended—analogous to how [mergekit](https://github.com/arcee-ai/mergekit) requires compatible checkpoints for `linear` / `slerp`-style merges.
- **Procedure (typical):** Rank experts on calibration data (e.g. routing frequency, soft router mass, or [REAP](https://arxiv.org/abs/2505.08738)-style activation scores) → keep top experts → merge each discarded expert into a **nearest** kept expert, often with importance-weighted interpolation of MLP weights.
- **vs. cross-model merging:** Tools like mergekit usually **fuse separate pretrained models** (or build a MoE from dense checkpoints via `mergekit-moe`). MoE **expert merge** in pruning papers (e.g. [SlimQwen](https://arxiv.org/abs/2605.08738)) operates **inside one teacher MoE** to shrink expert count; recovery is usually large-scale continual pretraining + distillation, not a single weight-average step.
- **Partial-preservation:** Keep half of the target experts **unchanged** and form the rest by merging discarded experts into merge bases—reduces homogenizing all experts through aggressive blending ([SlimQwen](https://arxiv.org/abs/2605.08738)).

Expert **prune** (drop experts entirely) vs **merge** (fold removed experts into survivors): merge often retains more capacity before post-compression training, at the cost of a more complex one-shot step.