# Transformer Backpropagation: Continuing the Mathematical Foundations

**Related paper:** [Attention Is All You Need](https://arxiv.org/abs/1706.03762)

**Status:** 🟡 In Progress

This note continues the mathematical treatment of backpropagation through the Transformer, focusing on the chain rule, linear projections and the attention computation.

## 1. Linear Transformation

Consider the common neural-network operation:

$$
z=Wx+b
$$

If the subsequent network produces a loss $L$, backpropagation determines how the loss changes with respect to the parameters and input.

The principal gradients are:

$$
\frac{\partial L}{\partial W}
=
\frac{\partial L}{\partial z}x^T
$$

$$
\frac{\partial L}{\partial x}
=
W^T\frac{\partial L}{\partial z}
$$

$$
\frac{\partial L}{\partial b}
=
\frac{\partial L}{\partial z}
$$

The transpose $W^T$ in the gradient with respect to $x$ is important: during backpropagation, the gradient is propagated through the linear transformation using the transpose of its weight matrix.

## 2. The Transformer as a Computational Graph

A simplified attention path can be written as:

$$
X
\rightarrow
Q,K,V
\rightarrow
QK^T
\rightarrow
\mathrm{softmax}
\rightarrow
AV
\rightarrow
W^O
\rightarrow
L
$$

where:

$$
Q=XW^Q
$$

$$
K=XW^K
$$

$$
V=XW^V
$$

and:

$$
A=\mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)
$$

followed by:

$$
O=AV
$$

and an output projection such as:

$$
Y=OW^O
$$

During the forward pass, information flows from $X$ toward the loss. During the backward pass, gradients flow from the loss back toward $X$ and the trainable parameters.

## 3. Backpropagation Through the Attention Output

For:

$$
O=AV
$$

suppose the upstream gradient is:

$$
\frac{\partial L}{\partial O}
$$

The gradients with respect to the attention weights and values are:

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

The gradient then continues through the softmax and scaled dot-product operations.

## 4. Backpropagation Through the Attention Scores

Define:

$$
S=\frac{QK^T}{\sqrt{d_k}}
$$

and:

$$
A=\mathrm{softmax}(S)
$$

The gradient therefore follows the chain:

$$
\frac{\partial L}{\partial A}
\rightarrow
\frac{\partial L}{\partial S}
\rightarrow
\frac{\partial L}{\partial Q},
\frac{\partial L}{\partial K}
$$

The exact Jacobian of softmax is:

$$
\frac{\partial A_i}{\partial S_j}
=
A_i(\delta_{ij}-A_j)
$$

Thus the softmax operation is fully differentiable and participates directly in gradient propagation.

The scaling operation contributes the factor:

$$
\frac{1}{\sqrt{d_k}}
$$

to the gradient passing through the scaled score matrix.

## 5. Returning to Q, K and V

Because:

$$
Q=XW^Q
$$

$$
K=XW^K
$$

$$
V=XW^V
$$

the gradients ultimately reach the learned projection matrices:

$$
\frac{\partial L}{\partial W^Q},
\qquad
\frac{\partial L}{\partial W^K},
\qquad
\frac{\partial L}{\partial W^V}
$$

and the input representation $X$.

The same input $X$ contributes to three computational paths, so its total gradient is the sum of the gradients arriving through those paths:

$$
\frac{\partial L}{\partial X}
=
\frac{\partial L}{\partial X}\bigg|_Q
+
\frac{\partial L}{\partial X}\bigg|_K
+
\frac{\partial L}{\partial X}\bigg|_V
$$

This is a fundamental consequence of the chain rule in a branching computational graph.

## 6. The Complete Learning Loop

The Transformer training process can therefore be viewed as:

```text
Input tokens
    ↓
Embeddings + positional information
    ↓
Q, K, V projections
    ↓
Attention scores
    ↓
Scaling
    ↓
Softmax
    ↓
Weighted value aggregation
    ↓
Transformer layers
    ↓
Output probabilities
    ↓
Loss
    ↓
Backpropagation
    ↓
Gradients
    ↓
Parameter update
    ↓
Improved model
```

The optimizer updates parameters according to a rule such as:

$$
W_{\mathrm{new}}
=
W_{\mathrm{old}}
-
\eta
\frac{\partial L}{\partial W}
$$

where $\eta$ is the learning rate.

## 7. The Important Conceptual Point

Attention is not itself a manually programmed rule saying that one word should attend to another. The model learns the parameters that generate useful query, key and value representations.

During training:

$$
\text{parameters}
\rightarrow
\text{attention patterns}
\rightarrow
\text{prediction}
\rightarrow
\text{loss}
\rightarrow
\text{gradients}
\rightarrow
\text{parameter updates}
$$

The attention mechanism becomes useful because gradient-based optimization adjusts the parameters to reduce the training objective.

## 8. Connection to the Core Attention Equation

The entire mechanism remains summarized by:

$$
\mathrm{Attention}(Q,K,V)
=
\mathrm{softmax}\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

The important learning insight is that every operation in this equation is part of a differentiable computational graph. The loss gradient can therefore propagate through the weighted sum, softmax, scaling and dot product, eventually reaching the learned Q/K/V projections.

This is the mathematical bridge between understanding the Transformer forward pass and understanding how the Transformer actually learns.

## Next Study Step

The next step is to derive the attention gradients more explicitly, including the matrix calculus for $QK^T$, the softmax Jacobian and the gradients of $W^Q$, $W^K$ and $W^V$, before moving deeper into multi-head attention and the complete Transformer block.
