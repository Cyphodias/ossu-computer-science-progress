# Tensor Product Attention Is All You Need

**Authors:** Yifan Zhang, Yifeng Liu, Huizhuo Yuan, Zhen Qin, Yang Yuan, Quanquan Gu, Andrew Chi-Chih Yao

**Year:** 2025

**Status:** 🟡 In Progress

**Paper:** [arXiv:2501.06425](https://arxiv.org/abs/2501.06425)

**Project:** [Tensor Product Attention](https://tensorgi.github.io/TPA/)

## Why This Paper Matters

This paper proposes Tensor Product Attention (TPA), a different representation of queries, keys and values based on tensor decomposition. The motivation is particularly important for modern language-model inference: long contexts make the key-value cache increasingly expensive in memory.

## Core Problem

Standard attention mechanisms can require substantial KV-cache memory during autoregressive decoding. The research question is how to represent the information needed for attention more compactly without sacrificing model quality.

## Core Idea

TPA factorizes query, key and value representations into sums of contextual tensor products. The representation can therefore be lower-rank and more compact while retaining contextual information.

Conceptually, the paper moves from thinking about Q/K/V as ordinary dense representations toward a structured factorized representation.

## Mathematical Structure

The paper represents the time-step query, key and value tensors using sums of tensor products. A simplified conceptual form is:

$$
Q_t=\sum_{r=1}^{R_Q} a_r^Q(x_t)\otimes b_r^Q(x_t)
$$

with analogous forms for $K_t$ and $V_t$:

$$
K_t=\sum_{r=1}^{R_K} a_r^K(x_t)\otimes b_r^K(x_t)
$$

$$
V_t=\sum_{r=1}^{R_V} a_r^V(x_t)\otimes b_r^V(x_t)
$$

The factorization ranks $R_Q$, $R_K$ and $R_V$ can differ.

## Main Motivation: KV Cache

For autoregressive language models, previous keys and values must be retained so that future tokens can attend to them. As sequence length increases, this cache can become a major inference-memory cost.

TPA attempts to reduce this cost through compact factorized representations.

## Connection to Standard Attention

The original Transformer computes:

$$
\mathrm{Attention}(Q,K,V)=\mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

The important comparison question is therefore:

> **What changes when Q, K and V are represented as contextual tensor-product factors rather than conventional dense projections?**

The goal is not simply to replace the attention equation, but to change the representation used by the attention mechanism so that memory and computational costs can be improved.

## T6 Architecture

The paper introduces the **Tensor ProducT ATTenTion Transformer (T6)** based on TPA.

The study should examine:

- TPA factorization
- contextual factorization
- integration with RoPE
- KV-cache representation
- decoding computation
- relationship to MHA
- relationship to MQA
- relationship to GQA
- relationship to MLA
- quality/memory trade-offs

## Important Comparison

| Aspect | Original Transformer | Tensor Product Attention |
|---|---|---|
| Q/K/V representation | Learned dense projections | Contextual tensor-product factorization |
| Attention mechanism | Scaled dot-product attention | Attention using factorized representations |
| KV cache | Dense cached K/V representations | Compact factorized representation |
| Main motivation | Parallel sequence transduction | Attention memory/computation efficiency |
| Positional encoding | Original sinusoidal encoding | Designed to integrate with RoPE |
| Modern relevance | Foundation of Transformer/LLM architecture | Efficient long-context attention |

## Questions To Investigate

- How does tensor-product factorization change the effective rank of Q, K and V?
- How are the contextual factors generated?
- How does the factorization affect the attention score calculation?
- Exactly where does the KV-cache reduction come from?
- What are the trade-offs between rank, quality, memory and computation?
- Why is TPA compatible with RoPE?
- In what sense can MHA, MQA and GQA be interpreted as special cases?
- How does TPA compare with Multi-Head Latent Attention?
- Which operations dominate decoding cost after factorization?

## Relation to Attention Is All You Need

The correct learning sequence is:

**Scaled Dot-Product Attention → Multi-Head Attention → Transformer → KV Caching → MQA/GQA/MLA → Tensor Product Attention**

The purpose of studying TPA immediately after the original Transformer is to understand how modern research modifies the representation and systems properties of attention while retaining the broader Transformer paradigm.

## Implementation Targets

After understanding the paper, implement or experiment with:

1. Standard scaled dot-product attention.
2. A conventional KV cache.
3. A simplified low-rank factorization of K and V.
4. Tensor-product representations on a small synthetic problem.
5. A comparison of cache size versus factorization rank.
6. A toy comparison between MHA, MQA, GQA and a factorized representation.

## Research Status

This paper is currently being studied together with **Attention Is All You Need**. Detailed derivations, observations and experimental notes will be added as the reading progresses.
