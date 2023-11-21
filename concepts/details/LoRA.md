## Introduction to Low-Rank Adaptation (LoRA)




Large language models are large, and it can be expensive to update all model weights during training due to GPU memory limitations. 
Low-rank adaptation ([LoRA](https://arxiv.org/abs/2106.09685))  is among the most widely used and effective techniques for efficiently training custom LLMs.  

Given an LLM with 7B parameters denoted as matrix $W$ (for simplicity, we refer to a single weight matrix here). During backpropagation, 
we learn a $\Delta W$ matrix, which contains information on how much we want to update the original weights to minimize the loss function during training.
The weight update is then as follows:

$W_{update} = W +  \Delta W$

Updating $\Delta W$ is expensive, which contains same 7B parameters as in $W$,  taking very much  compute and intensive memory.

The LoRA method, as shown in the figure below (source from lightning.ai), represents the $\Delta W$ with a low-rank decomposition $\Delta W = B A$ where $B$ and $A$ are two matrices with much smaller sizes than $\Delta W$ to make weight updates more efficient.  



<div align="center"><img src='../figs/LoRA.jpeg' width=550 alt=''> </img></div> 

The memory saving depends on the hyperparameter rank $r$. For example, if $\Delta W$ has $10,000$ rows and $20,000$ columns, it stores $200,000,000$ parameters. If we choose $A$ and $B$ with $r=8$, then $A$ has $10,000$ rows and $8$ columns, and $B$ has $8$ rows and $20,000$ columns, that's $10,000×8 + 8×20,000 = 240,000$ parameters, which is about $830 \times$ less than $200,000,000$.
For more details, please reach to the nice blog of <u> [Finetuning LLMs with LoRA and QLoRA Experiments](https://lightning.ai/pages/community/lora-insights/) </u>.

