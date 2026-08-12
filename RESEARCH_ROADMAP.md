# 📚 Computer Science + Mathematics + AI Research Roadmap

This is the supplementary research track attached to my OSSU Computer Science journey.

It is intentionally more advanced than the OSSU core curriculum. The purpose is to build a bridge from undergraduate Computer Science foundations to the research literature behind modern AI systems.

> **Important:** Being listed here means **planned/reference material**, not completed material. Completion is recorded separately.

---

## 1. Mathematics Foundations

### Primary books

- *Mathematics for Computer Science* — Lehman, Leighton & Meyer
- *Concrete Mathematics* — Graham, Knuth & Patashnik
- *Calculus* — Michael Spivak
- *Linear Algebra Done Right* — Sheldon Axler
- *Introduction to Probability* — Blitzstein & Hwang
- *Convex Optimization* — Boyd & Vandenberghe
- *The Elements of Statistical Learning* — Hastie, Tibshirani & Friedman

### Core outcomes

- Mathematical proof and reasoning
- Discrete structures
- Linear algebra
- Calculus
- Probability
- Statistics
- Optimization

---

## 2. Programming, Algorithms & Theory

### Primary books

- *Structure and Interpretation of Computer Programs* — Abelson & Sussman
- *The C Programming Language* — Kernighan & Ritchie
- *Introduction to Algorithms* — Cormen, Leiserson, Rivest & Stein
- *Algorithm Design* — Kleinberg & Tardos
- *Introduction to the Theory of Computation* — Michael Sipser
- *Computational Complexity* — Arora & Barak

### Research direction

Data structures → algorithms → complexity → computability → algorithmic research.

---

## 3. Computer Systems

### Architecture

- *Computer Organization and Design* — Patterson & Hennessy
- *Computer Architecture: A Quantitative Approach* — Hennessy & Patterson
- *Digital Design and Computer Architecture* — Harris & Harris

### Operating systems

- *Operating Systems: Three Easy Pieces* — Arpaci-Dusseau & Arpaci-Dusseau
- *Modern Operating Systems* — Tanenbaum & Bos
- *The Linux Programming Interface* — Michael Kerrisk

### Networking

- *Computer Networking: A Top-Down Approach* — Kurose & Ross
- *Computer Networks* — Tanenbaum & Wetherall
- *TCP/IP Illustrated, Volume 1* — W. Richard Stevens

### Databases & distributed systems

- *Database System Concepts* — Silberschatz, Korth & Sudarshan
- *Designing Data-Intensive Applications* — Martin Kleppmann
- *Database Internals* — Alex Petrov
- *Distributed Systems* — van Steen & Tanenbaum

---

## 4. Security & Cryptography

### Primary books

- *Introduction to Modern Cryptography* — Katz & Lindell
- *Security Engineering* — Ross Anderson
- *Serious Cryptography* — Jean-Philippe Aumasson

### Research direction

Cryptographic primitives → protocols → systems security → network security → applied security research.

---

## 5. Classical Machine Learning

### Primary books

- *Pattern Recognition and Machine Learning* — Christopher Bishop
- *Probabilistic Machine Learning: An Introduction* — Kevin Murphy
- *The Elements of Statistical Learning* — Hastie, Tibshirani & Friedman
- *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow* — Aurélien Géron

### Outcomes

- Supervised learning
- Unsupervised learning
- Statistical learning theory
- Probabilistic modelling
- Optimization
- Model evaluation

---

## 6. Deep Learning

### Primary books

- *Deep Learning* — Goodfellow, Bengio & Courville
- *Dive into Deep Learning* — Zhang et al.
- *Understanding Deep Learning* — Simon J.D. Prince
- *Neural Networks and Deep Learning* — Michael Nielsen

### Research progression

Perceptrons → multilayer networks → backpropagation → CNNs → sequence models → representation learning.

---

## 7. NLP & Sequence Models

### Primary books

- *Speech and Language Processing* — Jurafsky & Martin
- *Natural Language Processing with Transformers* — Tunstall, von Werra & Wolf

### Seminal progression

```text
Word2Vec
   ↓
RNN
   ↓
LSTM
   ↓
Seq2Seq
   ↓
Bahdanau Attention
   ↓
Transformer
```

The objective is to understand **why each architectural development occurred**, not merely to learn how to call an existing model.

---

## 8. Attention & Transformers

### Primary references

- *Natural Language Processing with Transformers* — Tunstall, von Werra & Wolf
- *Transformers for Natural Language Processing* — Denis Rothman
- *Understanding Deep Learning* — Simon J.D. Prince

### Paper progression

1. Seq2Seq learning
2. Neural machine translation
3. Bahdanau attention
4. **Attention Is All You Need**
5. BERT
6. GPT family
7. T5
8. Scaling laws
9. Instruction tuning
10. RLHF / preference optimization
11. LLaMA and open-weight LLMs
12. Retrieval-augmented generation
13. Tool use and modern LLM systems

---

## 9. Representation Learning

### Primary references

- *Deep Learning* — Goodfellow, Bengio & Courville
- *Dive into Deep Learning* — Zhang et al.
- *Understanding Deep Learning* — Prince

### Research direction

Autoencoders → representation learning → self-supervised learning → contrastive learning → foundation models.

---

## 10. Computer Vision

### Primary books

- *Computer Vision: Algorithms and Applications* — Richard Szeliski
- *Deep Learning for Vision Systems* — Mohamed Elgendy
- *Multiple View Geometry in Computer Vision* — Hartley & Zisserman

### Research direction

Classical vision → CNNs → object detection → segmentation → vision transformers → multimodal models.

---

## 11. Reinforcement Learning

### Primary books

- *Reinforcement Learning: An Introduction* — Sutton & Barto
- *Algorithms for Reinforcement Learning* — Csaba Szepesvári
- *Deep Reinforcement Learning Hands-On* — Maxim Lapan

### Research direction

MDPs → dynamic programming → Monte Carlo → temporal difference learning → Q-learning → policy gradients → deep RL → preference optimization.

---

## 12. Generative Models

### Primary references

- *Probabilistic Machine Learning* — Kevin Murphy
- *Deep Generative Modeling* — Jakub Tomczak
- *Deep Learning* — Goodfellow, Bengio & Courville

### Research progression

Autoregressive models → VAEs → GANs → normalizing flows → diffusion models → multimodal generative models.

---

## 13. Large Language Models

### Primary books

- *Build a Large Language Model (From Scratch)* — Sebastian Raschka
- *Hands-On Large Language Models* — Jay Alammar & Maarten Grootendorst
- *Natural Language Processing with Transformers* — Tunstall, von Werra & Wolf
- *Designing Machine Learning Systems* — Chip Huyen

### Research progression

```text
Language modelling
      ↓
Embeddings
      ↓
Attention
      ↓
Transformers
      ↓
Pretraining
      ↓
Scaling
      ↓
Instruction tuning
      ↓
Preference optimization / RLHF
      ↓
RAG
      ↓
Tool use / agents
      ↓
Inference optimization
      ↓
Distributed LLM systems
```

---

## 14. AI Systems

### Primary books

- *Designing Machine Learning Systems* — Chip Huyen
- *Designing Data-Intensive Applications* — Martin Kleppmann
- *Programming Massively Parallel Processors* — Kirk & Hwu
- *CUDA by Example* — Sanders & Kandrot

### Research direction

GPU computing → distributed training → data pipelines → model parallelism → memory optimization → inference → serving → evaluation.

---

## 15. Graphs & Time Series

### Primary references

- *Graph Representation Learning* — William L. Hamilton
- *Forecasting: Principles and Practice* — Hyndman & Athanasopoulos

### Research direction

Graph algorithms → graph neural networks → temporal models → forecasting → spatiotemporal learning.

---

## 16. Responsible AI

### Primary references

- *Fairness and Machine Learning* — Barocas, Hardt & Narayanan
- *Weapons of Math Destruction* — Cathy O'Neil
- *The Alignment Problem* — Brian Christian

These are supplementary to the technical curriculum and are intended to develop awareness of evaluation, fairness, safety, alignment and societal impact.

---

## 17. Research Practice

### Primary references

- *The Craft of Research* — Booth, Colomb & Williams
- *How to Read a Paper* — Keshav
- *Writing Science* — Joshua Schimel

### Paper-reading protocol

For every important paper:

1. Identify the problem.
2. Understand the prior work.
3. Identify the central contribution.
4. Derive or reconstruct the important mathematics.
5. Understand the architecture/algorithm.
6. Examine the experiments.
7. Identify limitations.
8. Reproduce a simplified result where practical.
9. Record questions and follow-up papers.
10. Link the paper to the broader research lineage.

---

## 📊 Current Research-Library Milestone

**257 references** have been organized into a progressive Computer Science + Mathematics + AI research library.

The accompanying workbook contains:

- All references
- Reading sequence
- Primary books / references for each stage
- Guidance on how to use the books
- End-state learning outcomes

The library is a **research map**, not a claim that all 257 references have already been read.

---

## 🔄 Update Rule

When material is genuinely completed, update the relevant OSSU phase and record:

- Date completed
- Course/book/paper
- Key concepts learned
- Implementation/project produced
- Difficult concepts
- Follow-up material

This keeps the repository an accurate record of the actual learning journey rather than a collection of intended resources.
