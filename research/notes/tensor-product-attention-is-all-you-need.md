# Tensor Product Attention Is All You Need

**Authors:** Yifan Zhang, Yifeng Liu, Huizhuo Yuan, Zhen Qin, Yang Yuan, Quanquan Gu, Andrew Chi-Chih Yao

**Year:** 2025

**Status:** 🟡 In Progress

**Paper:** [arXiv:2501.06425](https://arxiv.org/abs/2501.06425)

**Project:** [Tensor Product Attention](https://tensorgi.github.io/TPA/)

## Why This Paper Matters

This paper proposes Tensor Product Attention (TPA), a different representation of queries, keys and values based on tensor decomposition. Its motivation is particularly important for modern language-model inference: as context length increases, retaining key-value states can become a major memory cost.

TPA is therefore best understood as a change in the representation used by attention rather than simply a replacement of the attention equation.

## Core Problem

Standard attention produces dense Q/K/V representations and, during autoregressive decoding, previous keys and values must be retained for future attention operations. The resulting KV cache grows with sequence length and can become a significant inference-memory bottleneck.

The TPA approach addresses this problem by representing Q, K and V through structured contextual tensor-product factors, allowing the information required for attention to be represented more compactly.

## Core Idea

TPA factorizes query, key and value representations into sums of contextual tensor products. Instead of treating Q, K and V as unrestricted dense vectors, the representation is constructed from factorized components whose interaction captures contextual structure.

Conceptually:

$$
\text{dense Q/K/V representations}
\rightarrow
\text{contextual tensor-product factors}
$$

The factorization introduces an explicit rank structure. This can reduce the amount of information that must be stored in the KV cache while retaining a structured representation of the attention states.

## Mathematical Structure

A simplified conceptual form for a time-step query tensor is:

$$
Q_t=\sum_{r=1}^{R_Q} a_r^Q(x_t)\otimes b_r^Q(x_t)
$$

with analogous representations for keys and values:

$$
K_t=\sum_{r=1}^{R_K} a_r^K(x_t)\otimes b_r^K(x_t)
$$

$$
V_t=\sum_{r=1}^{R_V} a_r^V(x_t)\otimes b_r^V(x_t)
$$

where $\otimes$ denotes a tensor product and $R_Q$, $R_K$ and $R_V$ are factorization ranks that need not be equal.

The representation therefore replaces a single dense object with a structured sum of factor products. The selected rank controls the amount of factorized structure available to represent the underlying Q/K/V states.

## What Changes Relative to Conventional Attention?

The original Transformer computes attention using:

$$
\mathrm{Attention}(Q,K,V)=\mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

TPA does not simply discard this conceptual attention operation. Instead, it changes how the Q, K and V representations supplied to attention are constructed.

The key transformation is therefore:

$$
Q=XW^Q,\quad K=XW^K,\quad V=XW^V
$$

in the conventional dense formulation, versus contextual factorized representations of the form:

$$
Q_t=\sum_{r=1}^{R_Q}a_r^Q(x_t)\otimes b_r^Q(x_t)
$$

and analogous expressions for K and V in TPA.

The principal architectural consequence is that attention operates on a structured representation whose components can be stored and manipulated in factorized form.

## Main Motivation: KV Cache

During autoregressive decoding, previously generated tokens remain relevant to future tokens. Their key and value representations therefore need to be retained.

For conventional attention, the cache contains dense K/V representations for the preceding sequence. As the sequence becomes longer, the cache grows accordingly.

TPA addresses this storage problem by retaining factorized representations of the attention states. The resulting cache can represent the required information with fewer stored parameters when the selected factorization is sufficiently compact.

The central relationship is:

$$
\text{dense cached K/V}
\rightarrow
\text{factorized cached K/V}
\rightarrow
\text{reduced KV-cache memory}
$$

The exact reduction depends on the factorization structure and ranks used by the model.

## Contextual Factorization

The factors are contextual rather than fixed, independent basis components. Their values depend on the input representation, allowing the factorized representation to adapt to the current token context.

This distinction is important because the factorization is not merely a static compression of an already computed dense representation. The model constructs the factorized components as part of the attention representation itself.

## T6 Architecture

The paper introduces the **Tensor ProducT ATTenTion Transformer (T6)** based on TPA.

T6 incorporates the tensor-product representation into a Transformer architecture while retaining the broader Transformer framework. The resulting architecture is designed to improve the memory/computation characteristics of attention, particularly for autoregressive inference.

Important architectural components include:

- TPA factorization
- Contextual factor generation
- KV-cache representation
- Integration with RoPE
- Autoregressive decoding
- Attention computation using the factorized representations

## Comparison with Conventional Attention

| Aspect | Original Transformer | Tensor Product Attention |
|---|---|---|
| Q/K/V representation | Learned dense projections | Contextual tensor-product factorization |
| Attention mechanism | Scaled dot-product attention | Attention using factorized representations |
| KV cache | Dense cached K/V representations | Compact factorized representation |
| Main motivation | Parallel sequence transduction | Attention memory/computation efficiency |
| Positional encoding | Original sinusoidal encoding | Designed to integrate with RoPE |
| Modern relevance | Foundation of Transformer/LLM architecture | Efficient long-context attention |

The important difference is therefore representational. The original Transformer establishes the dense Q/K/V baseline; TPA changes the structure in which those representations are generated and retained.

## Relationship to MHA, MQA, GQA and MLA

TPA belongs to the broader progression of research attempting to improve the memory and computational characteristics of attention.

- **MHA** maintains separate attention heads with dense Q/K/V representations.
- **MQA** shares keys and values across query heads to reduce KV-cache size.
- **GQA** groups query heads so that several query heads share key/value representations.
- **MLA** compresses attention states into a latent representation to reduce KV-cache requirements.
- **TPA** uses contextual tensor-product factorization to represent Q/K/V in a structured form and reduce the storage requirements associated with attention states.

These approaches therefore differ in how they trade representational structure, memory consumption, computation and model quality.

## Integration with RoPE

TPA is designed to work with Rotary Position Embeddings (RoPE), allowing positional information to be incorporated while using the factorized attention representation.

This connects TPA to a later generation of Transformer architectures in which the original sinusoidal positional encoding has been replaced by positional mechanisms better suited to modern language-model designs.

## Computational and Memory Implications

The primary systems-level benefit targeted by TPA is a reduction in KV-cache memory. A compact factorized representation can reduce the amount of state that must be retained as context length grows.

The trade-off is that factorized representations introduce additional structure and operations. Consequently, the useful comparison is not simply whether the cache becomes smaller, but how rank, representation quality, computation and memory interact.

Conceptually:

$$
\text{factorization rank}
\leftrightarrow
\text{representation capacity}
\leftrightarrow
\text{memory cost}
\leftrightarrow
\text{computation}
$$

A lower rank can provide greater compression, while an insufficient rank can restrict representational capacity. The appropriate operating point therefore depends on the model and task.

## Relation to Attention Is All You Need

The conceptual progression is:

**Scaled Dot-Product Attention → Multi-Head Attention → Transformer → KV Caching → MQA/GQA/MLA → Tensor Product Attention**

The original Transformer establishes the dense attention representation. Later attention architectures modify the representation or sharing structure to address memory, computation and long-context requirements. TPA extends this progression by introducing contextual tensor-product factorization.

The most important comparison is therefore:

$$
\text{Dense Q/K/V projection}
\rightarrow
\text{Structured contextual Q/K/V representation}
$$

rather than:

$$
\text{one attention equation}
\rightarrow
\text{a completely different attention mechanism}
$$

## Implementation Targets

Practical reconstruction can proceed from the conventional baseline to the factorized representation:

1. Implement standard scaled dot-product attention.
2. Implement a conventional KV cache.
3. Implement MHA, MQA and GQA at toy scale.
4. Implement a simplified low-rank factorization of K and V.
5. Construct tensor-product representations on a small synthetic problem.
6. Compare cache size against factorization rank.
7. Compare memory, computation and output quality across the toy implementations.

These experiments make the relationship between tensor rank, representation capacity and KV-cache memory measurable rather than purely theoretical.

## Current Research Status

This paper is being studied directly after **Attention Is All You Need**. The purpose of the comparison is to understand how modern attention research changes the representation and systems properties of the original Transformer while retaining the broader attention-based architecture.

## Open Points / Ambiguities

- The exact factor-generation equations and implementation details should be read directly from the full paper before treating simplified equations in this note as a complete specification.
- The precise memory/computation trade-off depends on the factorization ranks and implementation.
- Claims about the relative quality of TPA, MHA, MQA, GQA and MLA should be interpreted in the context of the paper's experimental setup and compared against the original sources.
