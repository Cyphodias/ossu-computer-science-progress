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
\mathrm{MultiHead}(Q,K,V)=\mathrm{Concat}(head_1,\ldots,head_h)W^O
$$

Each head performs attention using its own learned projections:

$$
\mathrm{head}_i
=
\mathrm{Attention}
(QW_i^Q,KW_i^K,VW_i^V)
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

## Open Points / Ambiguities

- The precise behavior and specialization of individual attention heads is an empirical property rather than something guaranteed by the architecture.
- The original sinusoidal positional encoding should be compared separately with later approaches such as RoPE.
- The detailed memory and computational trade-offs introduced by later factorized or compressed attention mechanisms require analysis of their respective architectures and experiments.
