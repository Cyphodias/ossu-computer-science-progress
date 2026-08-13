# Attention Is All You Need

**Authors:** Vaswani et al.

**Year:** 2017

**Research Library:** #122

**Status:** 🟡 In Progress

**Primary link:** [arXiv](https://arxiv.org/abs/1706.03762)

## Why This Paper Matters

This paper introduced the Transformer architecture, replacing recurrence and convolution as the primary mechanism for sequence transduction with attention. It established the architectural foundation for the later Transformer, BERT, GPT, T5 and modern large language model research lineage.

## Core Problem

Earlier sequence models relied heavily on recurrent or convolutional architectures. The Transformer provides a sequence-transduction architecture in which relationships between positions can be modeled directly through attention, while allowing substantially greater parallelization during training and providing a more direct path for modeling long-range dependencies.

## Core Idea

The Transformer is built around attention. Instead of processing tokens strictly one at a time, each position can directly interact with other positions through learned attention weights. This allows the model to construct representations from relationships across the sequence without requiring recurrent state to propagate information from one position to the next.

## Key Mathematics

### Scaled Dot-Product Attention

$$
\mathrm{Attention}(Q,K,V)=\mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

Where:

- $Q$ = queries
- $K$ = keys
- $V$ = values
- $d_k$ = key dimensionality

The operation has four stages:

1. $QK^T$ computes query-key compatibility scores.
2. Division by $\sqrt{d_k}$ controls the magnitude of the scores.
3. Softmax converts the scaled scores into normalized attention weights.
4. The resulting weights form a weighted combination of the value vectors in $V$.

The output therefore represents information retrieved from the values according to the compatibility between each query and the available keys.

### Learned Projections

For an input representation $X$:

$$
Q=XW^Q,\qquad K=XW^K,\qquad V=XW^V
$$

The learned matrices project the same input representation into three different representational roles. Queries determine what information a position is seeking, keys determine how positions can be matched against those queries, and values contain the information that is aggregated after the matching operation.

### Why Scale by $\sqrt{d_k}$?

As the key/query dimensionality increases, the magnitude of the dot products can increase. Large values entering softmax can make the resulting distribution excessively concentrated and produce undesirable gradient behavior. Scaling the scores by $\sqrt{d_k}$ controls this growth and keeps the softmax operating in a more useful range.

### Multi-Head Attention

$$
\mathrm{MultiHead}(Q,K,V)=\mathrm{Concat}(\mathrm{head}_1,\ldots,\mathrm{head}_h)W^O
$$

Each head performs attention using its own learned projections:

$$
\mathrm{head}_i=\mathrm{Attention}(QW_i^Q,KW_i^K,VW_i^V)
$$

Multiple heads allow the model to construct several attention representations simultaneously. Each head operates in its own learned projection subspace, allowing different heads to capture different relationships or features in the sequence before the results are concatenated and projected through $W^O$.

## Transformer Architecture

The Transformer consists of an encoder stack and a decoder stack. Its principal components are:

- Multi-head self-attention
- Encoder-decoder attention
- Position-wise feed-forward networks
- Residual connections
- Layer normalization
- Positional encoding
- Causal masking in decoder self-attention
- Linear projection and softmax output

The architecture combines these components into repeated layers rather than relying on recurrence or convolution to propagate sequence information.

### Encoder Self-Attention

Each encoder position can attend to the other positions in the input sequence. This allows the representation at a position to incorporate information from the broader input context.

### Decoder Self-Attention

The decoder uses masked self-attention so that a position cannot attend to future target positions during autoregressive generation. This preserves the causal structure required for predicting the next token from previously available tokens.

### Encoder-Decoder Attention

The decoder also attends to the encoder output. This provides the decoder with access to the source sequence representation while generating the target sequence.

## Positional Information

Self-attention by itself does not impose an inherent sequential order on the input positions. Positional information is therefore supplied explicitly. The original Transformer uses sinusoidal positional encodings that are added to the token embeddings.

The consequence is that the model receives both token content and information about the position of each token while retaining the parallel computation of attention.

## Residual Connections and Layer Normalization

Each major sublayer is surrounded by a residual connection and normalization. The residual pathway allows information to pass through the stack without requiring every layer to reconstruct the complete representation, while normalization stabilizes the transformations performed by successive layers.

## Position-Wise Feed-Forward Network

After attention, each position is transformed independently by the same feed-forward network. Attention therefore performs interaction across positions, while the feed-forward component performs nonlinear transformation within each position's representation.

This separation is fundamental to the Transformer block:

$$
\text{sequence interaction}
\rightarrow
\text{position-wise nonlinear transformation}
$$

## Why the Transformer Is Highly Parallelizable

The Transformer removes the sequential recurrence that prevents recurrent networks from processing all positions simultaneously during training. Self-attention allows the interactions for a sequence to be computed using matrix operations, making the architecture well suited to parallel hardware.

This does not eliminate all computational costs: standard self-attention requires pairwise interactions between positions, so the attention operation has quadratic dependence on sequence length in its conventional form.

## Self-Attention and Encoder-Decoder Attention

Self-attention uses queries, keys and values derived from the same sequence representation. Encoder-decoder attention instead derives the queries from the decoder representation while using encoder representations as keys and values.

The distinction allows the decoder to combine its current generated context with information encoded from the source sequence.

## Causal Masking

During autoregressive decoding, future target tokens must not influence the prediction of the current token. A causal mask therefore removes attention connections to future positions before the softmax operation.

This makes the attention pattern consistent with left-to-right generation while retaining parallel computation across positions during training.

## Research Connections

This paper is the central reference for the later Transformer sequence in the research library:

**Attention Is All You Need → BERT → GPT → T5 → efficient Transformers → modern LLM architectures**

It also connects to preceding sequence-model work on embeddings, RNNs/LSTMs and Seq2Seq attention, which established many of the sequence-processing problems that the Transformer reformulated.

## Significance for Later Attention Research

The original Transformer establishes the standard dense Q/K/V representation and scaled dot-product attention used as the baseline for many later architectures. Subsequent research modifies the attention representation, attention pattern, positional mechanism, memory usage or computational strategy while retaining the broader Transformer framework.

This provides the conceptual starting point for studying approaches such as MQA, GQA, MLA and Tensor Product Attention.

## Implementation Targets

A practical reconstruction of the paper should include:

1. Scaled dot-product attention from scratch.
2. Learned Q/K/V projections.
3. Multi-head attention from scratch.
4. Causal masking.
5. Positional encoding.
6. A minimal Transformer block.
7. A small sequence-to-sequence Transformer.

Implementation is useful because each component corresponds directly to a mathematical operation in the paper and makes the relationship between the equations and the architecture concrete.

## Current Research Status

The paper is currently being studied as the foundation for the modern attention sequence. Its concepts are being compared directly with **Tensor Product Attention Is All You Need**, with particular attention to the representation of Q/K/V, inference-time memory and the evolution of efficient attention architectures.

---

# Backpropagation and Softmax

## 1. Intuition First

### Softmax — the simple idea

Softmax takes a collection of raw scores and turns them into **relative weights that add up to 1**.

Imagine the Transformer is deciding which words are important to a particular word:

```text
The   cat   sat   on   the   mat
 5     2     8    1     3     4
```

These numbers are only scores. Softmax converts them into something like:

```text
The    0.04
cat    0.01
sat    0.72
on     0.00
the    0.03
mat    0.20
```

The Transformer can then use these values as **attention weights**.

In simple terms:

> **Softmax turns "how strongly do I score each option?" into "how much attention should I give each option?"**

### Backpropagation — the simple idea

Backpropagation is how the Transformer **learns from its mistakes**.

Suppose the model predicts:

```text
The cat sat on the ___
```

and assigns:

```text
mat    0.20
floor  0.10
chair  0.05
...
```

but the correct answer is `mat`.

The model calculates how wrong its prediction was, producing a **loss**.

Backpropagation then works backward through the entire network and determines which parameters contributed to the error and by how much. Those parameters are then adjusted.

```text
Prediction
    ↓
Calculate error
    ↓
Backpropagation
    ↓
Calculate gradients
    ↓
Update parameters
    ↓
Better prediction
```

The Transformer does **not** manually learn rules about which words should attend to one another. It learns parameters that produce useful attention patterns through gradient-based optimization.

---

## 2. Backpropagation

Backpropagation computes how the training loss changes with respect to the parameters of a neural network.

For a model with parameters $\theta$:

$$
L=L(\theta)
$$

Training seeks to minimize $L$.

The parameters are updated using gradient descent:

$$
\theta\leftarrow\theta-\eta\nabla_\theta L
$$

where:

- $L$ = loss
- $\theta$ = trainable parameters
- $\nabla_\theta L$ = gradient of the loss with respect to those parameters
- $\eta$ = learning rate

The gradient tells the optimizer **which direction each parameter should move and how strongly**.

---

## 3. The Chain Rule

Backpropagation is fundamentally an efficient application of the chain rule.

For:

$$
x\rightarrow z\rightarrow y\rightarrow L
$$

the derivative is:

$$
\frac{\partial L}{\partial x}
=
\frac{\partial L}{\partial y}
\frac{\partial y}{\partial z}
\frac{\partial z}{\partial x}
$$

A Transformer consists of many interconnected mathematical operations, so the chain rule allows the loss gradient to propagate through the entire computational graph.

For example, if:

$$
z=Wx+b
$$

and the subsequent network produces a loss $L$, then the gradient with respect to the weight matrix is:

$$
\frac{\partial L}{\partial W}
=
\frac{\partial L}{\partial z}
\frac{\partial z}{\partial W}
$$

The resulting gradients are used by the optimization algorithm to update the parameters.

---

## 4. Backpropagation Through Attention

The Transformer is differentiable end-to-end. Consequently, the loss gradient can propagate through the attention mechanism and update the parameters that generate the queries, keys and values.

The attention computation is:

$$
\mathrm{Attention}(Q,K,V)
=
\mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

The gradient therefore propagates through:

```text
Q, K, V
   ↓
QKᵀ
   ↓
QKᵀ / √dₖ
   ↓
softmax
   ↓
weighted sum
   ↓
loss
```

The learned projections are:

$$
Q=XW^Q
$$

$$
K=XW^K
$$

$$
V=XW^V
$$

Therefore, gradients from the final loss propagate back through the attention operation into $Q$, $K$, and $V$, and then into the projection matrices:

$$
\frac{\partial L}{\partial W^Q},
\qquad
\frac{\partial L}{\partial W^K},
\qquad
\frac{\partial L}{\partial W^V}
$$

This is how the Transformer learns the representations used to determine which tokens should attend to which other tokens.

---

## 5. Softmax

Softmax converts a vector of arbitrary real-valued scores into a normalized probability distribution.

For:

$$
z=(z_1,z_2,\ldots,z_n)
$$

the softmax function is:

$$
\mathrm{softmax}(z_i)
=
\frac{e^{z_i}}
{\sum_{j=1}^{n}e^{z_j}}
$$

The resulting values satisfy:

$$
0<\mathrm{softmax}(z_i)<1
$$

and:

$$
\sum_{i=1}^{n}\mathrm{softmax}(z_i)=1
$$

Therefore, softmax transforms relative scores into normalized weights.

---

## 6. Softmax in Transformer Attention

In scaled dot-product attention, the raw compatibility scores are:

$$
S=QK^T
$$

The scores are scaled:

$$
S_{\mathrm{scaled}}=\frac{QK^T}{\sqrt{d_k}}
$$

and softmax is then applied row-wise:

$$
A=\mathrm{softmax}
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)
$$

The matrix $A$ contains the attention weights.

The final attention output is:

$$
O=AV
$$

Thus:

$$
Q,K,V
\rightarrow
QK^T
\rightarrow
\frac{QK^T}{\sqrt{d_k}}
\rightarrow
\mathrm{softmax}
\rightarrow
A
\rightarrow
AV
$$

For a particular query, the corresponding row of $A$ determines how strongly that query incorporates each available value vector.

---

## 7. What the Attention Weights Mean

Suppose one row of the attention matrix is:

$$
A_i=[0.05,0.10,0.70,0.15]
$$

The corresponding output is:

$$
O_i=0.05V_1+0.10V_2+0.70V_3+0.15V_4
$$

The third value therefore contributes the most to the resulting representation.

This is the mathematical meaning of the phrase **"paying attention"**.

The model is not literally looking at words. It is calculating a weighted combination of representations.

---

## 8. Why Divide by $\sqrt{d_k}$?

The Transformer uses:

$$
\frac{QK^T}{\sqrt{d_k}}
$$

rather than simply:

$$
QK^T
$$

As $d_k$ increases, dot products can become larger in magnitude.

Large logits passed directly into softmax can produce extremely peaked distributions. For example:

$$
[0.0001,0.0002,0.9997]
$$

When softmax becomes highly saturated, its gradients can become very small and optimization can become more difficult.

Dividing by:

$$
\sqrt{d_k}
$$

helps control the magnitude of the logits before softmax.

Therefore:

$$
\text{larger dot products}
\rightarrow
\text{scaling}
\rightarrow
\text{better-controlled softmax inputs}
\rightarrow
\text{more stable optimization}
$$

This is an important part of the original Transformer attention formulation rather than an arbitrary normalization.

---

## 9. Derivative of Softmax

Softmax is differentiable, which allows backpropagation to pass through the attention weights.

For:

$$
y_i=\mathrm{softmax}(z_i)
$$

the derivative with respect to $z_j$ is:

$$
\frac{\partial y_i}{\partial z_j}
=
y_i(\delta_{ij}-y_j)
$$

where $\delta_{ij}$ is the Kronecker delta:

$$
\delta_{ij}
=
\begin{cases}
1 & i=j\\
0 & i\ne j
\end{cases}
$$

Therefore:

$$
\frac{\partial y_i}{\partial z_i}
=
y_i(1-y_i)
$$

and for $i\ne j$:

$$
\frac{\partial y_i}{\partial z_j}
=-y_i y_j
$$

This demonstrates an important property of softmax: **the output probabilities are coupled**. Changing one logit affects the entire probability distribution because all outputs share the same normalization denominator.

---

## 10. Softmax and Cross-Entropy

At the output of the Transformer, the final hidden representation is converted into vocabulary logits:

$$
z=hW^O+b
$$

Softmax converts these logits into token probabilities:

$$
p_i=\frac{e^{z_i}}{\sum_j e^{z_j}}
$$

For target token $y$, cross-entropy loss is:

$$
L=-\log p_y
$$

When softmax and cross-entropy are combined, the derivative with respect to each logit simplifies to:

$$
\frac{\partial L}{\partial z_i}=p_i-y_i
$$

where $y_i$ is the one-hot target.

This gives a particularly clear learning signal:

$$
\text{gradient}=\text{prediction}-\text{target}
$$

The output layer therefore receives a direct signal indicating which probabilities should increase and which should decrease.

---

## 11. Two Different Roles of Softmax

Softmax appears in two conceptually different places in a Transformer.

| Location | Input | Output | Purpose |
|---|---|---|---|
| Attention | $QK^T/\sqrt{d_k}$ | Attention weights | Controls information mixing between positions |
| Output layer | Vocabulary logits | Token probabilities | Predicts the next token |

This distinction is important.

**Attention softmax does not predict the next word.** It determines how strongly information from different sequence positions contributes to a representation.

The **final vocabulary softmax** converts the model's output into probabilities over possible tokens.

Backpropagation connects both operations to the training objective.

---

## 12. Complete Forward Pass

The overall relationship can be summarized as:

$$
X
\rightarrow
Q,K,V
\rightarrow
\mathrm{Attention}
\rightarrow
\mathrm{Transformer\ layers}
\rightarrow
h
\rightarrow
z
\rightarrow
\mathrm{softmax}
\rightarrow
L
$$

The attention component is:

$$
Q,K,V
\rightarrow
\frac{QK^T}{\sqrt{d_k}}
\rightarrow
\mathrm{softmax}
\rightarrow
A
\rightarrow
AV
$$

The model therefore performs a sequence of differentiable operations.

---

## 13. Complete Backward Pass

During training, the gradient travels in the opposite direction:

$$
L
\rightarrow
z
\rightarrow
h
\rightarrow
\mathrm{Transformer}
\rightarrow
A
\rightarrow
Q,K,V
\rightarrow
W^Q,W^K,W^V
$$

The optimizer then uses these gradients to update the parameters.

This establishes the complete learning loop:

$$
\text{Input}
\rightarrow
\text{Prediction}
\rightarrow
\text{Loss}
\rightarrow
\text{Backpropagation}
\rightarrow
\text{Gradient}
\rightarrow
\text{Parameter Update}
$$

---

## 14. Connection to Attention Is All You Need

The significance of backpropagation and softmax in **Attention Is All You Need** is that the Transformer is not merely a new way of calculating attention.

It is a **fully trainable differentiable architecture**.

The attention mechanism:

$$
\mathrm{softmax}
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

is embedded inside a larger computational graph.

The parameters generating $Q$, $K$, and $V$ are learned because errors from the training objective propagate backward through the attention mechanism.

Consequently, the Transformer learns representations in which useful relationships between tokens produce useful attention patterns.

---

## 15. Key Conclusions

### Softmax

Softmax converts relative scores into normalized weights.

In attention:

$$
\mathrm{softmax}
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)
$$

determines how strongly each position contributes to another position's representation.

### Backpropagation

Backpropagation calculates how the final loss depends on the parameters throughout the Transformer.

It allows the model to learn:

$$
W^Q,W^K,W^V,W^O
$$

as well as the other parameters throughout the network.

### Their Relationship

Softmax participates directly in the forward computation, while backpropagation provides the mechanism through which the consequences of that computation influence parameter learning.

Therefore:

$$
\text{Attention computation}
+
\text{differentiability}
+
\text{backpropagation}
+
\text{optimization}
\rightarrow
\text{learned attention}
$$

---

## 16. Open Points / Further Connections

The following are useful areas for deeper treatment later:

- the exact gradient flow through $QK^T$;
- the Jacobian structure of softmax;
- numerical stability when computing exponentials;
- why the scaling factor becomes particularly important as $d_k$ increases;
- the relationship between softmax saturation and vanishing gradients;
- how causal masking modifies the attention logits before softmax;
- how these mechanisms behave during autoregressive inference;
- how attention computation and backpropagation interact with the later KV-cache discussion in TPA.

---

## 17. Connection to Later Research

The concepts above form the mathematical foundation for understanding later attention variants and the TPA paper.

The progression is:

$$
\text{Dense Q/K/V}
\rightarrow
\text{Attention}
\rightarrow
\text{KV representations}
\rightarrow
\text{MHA/MQA/GQA/MLA}
\rightarrow
\text{Tensor Product Attention}
$$

The important comparison in TPA is therefore not simply a replacement of the attention equation. It concerns **how $Q$, $K$, and $V$ themselves are represented and stored**, particularly in relation to the KV-cache and memory requirements.

---

## 18. Deriving the Gradient with Respect to $X$ in Self-Attention

The next step is to follow the gradient all the way from the attention output back to the input representation $X$.

Start with:

$$
Q=XW^Q,\qquad K=XW^K,\qquad V=XW^V
$$

and:

$$
S=\frac{QK^T}{\sqrt{d_k}}
$$

$$
A=\mathrm{softmax}(S)
$$

$$
O=AV
$$

Suppose the loss $L$ has already produced an upstream gradient:

$$
G_O=\frac{\partial L}{\partial O}
$$

We now propagate this gradient backward through each operation.

### 18.1 Gradient Through $O=AV$

Because:

$$
O=AV
$$

the gradients are:

$$
\frac{\partial L}{\partial A}
=
\frac{\partial L}{\partial O}V^T
$$

and:

$$
\frac{\partial L}{\partial V}
=
A^T\frac{\partial L}{\partial O}
$$

Therefore:

$$
G_A=G_OV^T
$$

and:

$$
G_V=A^TG_O
$$

The first gradient continues backward through softmax. The second gradient goes directly into the value projection.

### 18.2 Gradient Through Softmax

We have:

$$
A=\mathrm{softmax}(S)
$$

For each row, the softmax Jacobian is:

$$
J_{\mathrm{softmax}}
=
\mathrm{diag}(A)-AA^T
$$

Therefore the gradient with respect to the score matrix $S$ is obtained by multiplying the upstream gradient by the softmax Jacobian.

For one attention row:

$$
g_S
=
\left[
\mathrm{diag}(a)-aa^T
\right]g_A
$$

Equivalently, the row-wise gradient can be written compactly as:

$$
g_S
=
a\odot
\left(
g_A-(g_A\cdot a)\mathbf{1}
\right)
$$

where $\odot$ denotes element-wise multiplication.

Thus:

$$
G_A
\rightarrow
G_S
$$

through the softmax derivative.

### 18.3 Gradient Through the Scaling Operation

The score matrix is:

$$
S=\frac{QK^T}{\sqrt{d_k}}
$$

Therefore:

$$
\frac{\partial L}{\partial(QK^T)}
=
\frac{1}{\sqrt{d_k}}G_S
$$

Define:

$$
G_M=
\frac{G_S}{\sqrt{d_k}}
$$

where:

$$
M=QK^T
$$

### 18.4 Gradient Through $QK^T$

Now consider:

$$
M=QK^T
$$

The gradients are:

$$
\frac{\partial L}{\partial Q}
=
G_MK
$$

and:

$$
\frac{\partial L}{\partial K}
=
G_M^TQ
$$

Therefore:

$$
G_Q=
\frac{G_SK}{\sqrt{d_k}}
$$

and:

$$
G_K=
\frac{G_S^TQ}{\sqrt{d_k}}
$$

At this point the gradient has reached $Q$, $K$, and $V$.

### 18.5 Gradient Through the Three Learned Projections

Recall:

$$
Q=XW^Q
$$

$$
K=XW^K
$$

$$
V=XW^V
$$

For the query projection:

$$
G_Q=\frac{\partial L}{\partial Q}
$$

so:

$$
\frac{\partial L}{\partial W^Q}
=
X^TG_Q
$$

and:

$$
\frac{\partial L}{\partial X}\bigg|_Q
=
G_Q(W^Q)^T
$$

For the key projection:

$$
\frac{\partial L}{\partial W^K}
=
X^TG_K
$$

and:

$$
\frac{\partial L}{\partial X}\bigg|_K
=
G_K(W^K)^T
$$

For the value projection:

$$
\frac{\partial L}{\partial W^V}
=
X^TG_V
$$

and:

$$
\frac{\partial L}{\partial X}\bigg|_V
=
G_V(W^V)^T
$$

### 18.6 The Critical Result: $\frac{\partial L}{\partial X}$

The same input $X$ feeds all three projections:

$$
X\rightarrow Q
$$

$$
X\rightarrow K
$$

$$
X\rightarrow V
$$

Therefore the total gradient with respect to $X$ is the sum of the three gradient paths:

$$
\boxed{
\frac{\partial L}{\partial X}
=
G_Q(W^Q)^T
+
G_K(W^K)^T
+
G_V(W^V)^T
}
$$

Substituting the attention gradients:

$$
G_Q=
\frac{G_SK}{\sqrt{d_k}}
$$

$$
G_K=
\frac{G_S^TQ}{\sqrt{d_k}}
$$

$$
G_V=A^TG_O
$$

gives:

$$
\boxed{
\frac{\partial L}{\partial X}
=
\frac{G_SK}{\sqrt{d_k}}(W^Q)^T
+
\frac{G_S^TQ}{\sqrt{d_k}}(W^K)^T
+
A^TG_O(W^V)^T
}
$$

where $G_S$ is the gradient obtained by propagating $G_A=G_OV^T$ through the softmax.

This is the important result: **the gradient with respect to $X$ is not obtained through a single path. It is the sum of the gradients arriving through the query, key and value branches.**

### 18.7 Complete Backward Computational Graph

The forward computation is:

$$
X
\rightarrow
\begin{cases}
Q=XW^Q\\
K=XW^K\\
V=XW^V
\end{cases}
\rightarrow
QK^T
\rightarrow
\frac{QK^T}{\sqrt{d_k}}
\rightarrow
A
\rightarrow
O=AV
\rightarrow
L
$$

The backward computation is:

$$
\frac{\partial L}{\partial O}
\rightarrow
\begin{cases}
\frac{\partial L}{\partial A}\\
\frac{\partial L}{\partial V}
\end{cases}
\rightarrow
\frac{\partial L}{\partial S}
\rightarrow
\begin{cases}
\frac{\partial L}{\partial Q}\\
\frac{\partial L}{\partial K}
\end{cases}
\rightarrow
\begin{cases}
\frac{\partial L}{\partial W^Q}\\
\frac{\partial L}{\partial W^K}\\
\frac{\partial L}{\partial W^V}\\
\frac{\partial L}{\partial X}
\end{cases}
$$

The three branches eventually meet again at $X$:

$$
\boxed{
\frac{\partial L}{\partial X}
=
\frac{\partial L}{\partial X}\bigg|_Q
+
\frac{\partial L}{\partial X}\bigg|_K
+
\frac{\partial L}{\partial X}\bigg|_V
}
$$

This is the concrete application of the chain rule to the Q/K/V structure of self-attention.

### 18.8 Why This Matters

The forward pass explains **how attention constructs a representation**.

The backward pass explains **how the model learns the projections that make that representation useful**.

The complete relationship is:

$$
X
\rightarrow
Q,K,V
\rightarrow
A
\rightarrow
O
\rightarrow
L
$$

followed by:

$$
L
\rightarrow
O
\rightarrow
A
\rightarrow
Q,K,V
\rightarrow
W^Q,W^K,W^V,X
$$

Thus the Transformer learns its attention behavior through ordinary differentiable optimization. There is no separate learning mechanism hidden inside attention.

---

## 19. Matrix Summary of the Attention Backward Pass

For reference, let:

$$
O=AV
$$

$$
A=\mathrm{softmax}(S)
$$

$$
S=\frac{QK^T}{\sqrt{d_k}}
$$

$$
Q=XW^Q,\qquad K=XW^K,\qquad V=XW^V
$$

Given:

$$
G_O=\frac{\partial L}{\partial O}
$$

the backward sequence is:

$$
G_A=G_OV^T
$$

$$
G_V=A^TG_O
$$

$$
G_S=\mathrm{softmax\_backward}(S,G_A)
$$

$$
G_Q=\frac{G_SK}{\sqrt{d_k}}
$$

$$
G_K=\frac{G_S^TQ}{\sqrt{d_k}}
$$

then:

$$
\frac{\partial L}{\partial W^Q}=X^TG_Q
$$

$$
\frac{\partial L}{\partial W^K}=X^TG_K
$$

$$
\frac{\partial L}{\partial W^V}=X^TG_V
$$

and finally:

$$
\boxed{
\frac{\partial L}{\partial X}
=
G_Q(W^Q)^T
+
G_K(W^K)^T
+
G_V(W^V)^T
}
$$

This completes the missing mathematical link between the attention equation and the gradient that reaches the input representation.

## 20. Next Step

The next mathematical step is to work through a **small numerical self-attention example by hand**, calculating $Q$, $K$, $V$, the attention scores, scaling, softmax, output, loss and then the corresponding backward gradients. That example should make every symbol above concrete before moving to multi-head attention and the complete Transformer block.
