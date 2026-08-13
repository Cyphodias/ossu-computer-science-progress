# Attention Is All You Need

**Authors:** Vaswani et al.

**Year:** 2017

**Research Library:** #122

**Status:** 🟡 In Progress

**Primary link:** [arXiv](https://arxiv.org/abs/1706.03762)

## Why This Paper Matters

This paper introduced the Transformer architecture, replacing recurrence and convolution as the primary mechanism for sequence transduction with attention. It is a foundational paper for modern NLP and the later Transformer/LLM research lineage.

## Core Problem

Earlier sequence models relied heavily on recurrent or convolutional architectures. The authors sought an architecture that could model relationships between sequence elements while being substantially more parallelizable during training and better at handling long-range dependencies.

## Core Idea

The Transformer is built around attention. Instead of processing tokens strictly one at a time, each position can directly interact with other positions through learned attention weights.

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

The main steps are:

1. Compute query-key compatibility with $QK^T$.
2. Scale by $\sqrt{d_k}$ to control the magnitude of the dot products.
3. Apply softmax to obtain normalized attention weights.
4. Use those weights to form a weighted combination of the values.

### Learned Projections

For an input representation $X$:

$$
Q=XW^Q,\qquad K=XW^K,\qquad V=XW^V
$$

The learned matrices allow the model to construct different representations for querying, matching and retrieving information.

### Multi-Head Attention

$$
\mathrm{MultiHead}(Q,K,V)=\mathrm{Concat}(head_1,\ldots,head_h)W^O
$$

Each head performs attention using its own learned projections. Multiple heads allow the model to capture different relationships or representation subspaces simultaneously.

## Transformer Architecture

The major components to understand are:

- Encoder stack
- Decoder stack
- Multi-head self-attention
- Encoder-decoder attention
- Position-wise feed-forward networks
- Residual connections
- Layer normalization
- Positional encoding
- Masking in decoder self-attention
- Linear projection and softmax output

## Positional Information

Because the architecture does not inherently process tokens sequentially, positional information must be supplied explicitly. The original Transformer uses sinusoidal positional encodings.

The important conceptual question is not merely how the formula is written, but **why position has to be represented at all when attention itself is permutation-compatible**.

## Why Scale by $\sqrt{d_k}$?

As the key/query dimensionality increases, unscaled dot products can grow in magnitude. Large values passed into softmax can produce very concentrated distributions and undesirable gradients. Scaling by $\sqrt{d_k}$ controls this effect.

## What to Understand, Not Memorize

After studying this paper, you should be able to explain:

- Why attention replaces recurrence in this architecture.
- What queries, keys and values represent.
- Why $QK^T$ produces attention scores.
- Why softmax is used.
- Why scaling is necessary.
- Why multiple attention heads are useful.
- How positional information enters the model.
- Why residual connections and normalization are used.
- The difference between self-attention and encoder-decoder attention.
- How causal masking prevents the decoder from using future tokens.
- Why the architecture is highly parallelizable during training.

## Research Connections

This paper is the central reference for the later Transformer sequence in the research library:

**Attention Is All You Need → BERT → GPT → T5 → efficient Transformers → modern LLM architectures**

It should also be connected to the preceding sequence-model work on embeddings, RNNs/LSTMs and Seq2Seq attention.

## Current Questions / Things to Investigate

- How exactly does attention distribute information across positions?
- What does each head learn in practice?
- What are the mathematical consequences of positional encoding choices?
- How do modern positional methods such as RoPE differ from the original sinusoidal encoding?
- What changes when attention is factorized, compressed or approximated?
- How does KV caching alter the inference-time computational picture?

## Implementation Targets

After understanding the paper, implement at least:

1. Scaled dot-product attention from scratch.
2. Multi-head attention from scratch.
3. Causal masking.
4. Positional encoding.
5. A minimal Transformer block.
6. A small sequence-to-sequence Transformer.

## Related Current Reading

The next paper being studied alongside this paper is **Tensor Product Attention Is All You Need**. Its purpose is to examine a more recent attention formulation and compare the representation and memory implications with standard Transformer attention.

## Notes To Add During Reading

This document is intentionally a living research note. Additional derivations, observations, implementation findings, questions and connections should be added as the paper is worked through.
