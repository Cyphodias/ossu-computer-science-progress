# Reading Sequence

The research roadmap is organized into **20 progressive stages**. Books are used as primary learning references; papers are introduced after the required foundations are established.

## Stage 1 — Mathematical foundations

**What to master:** Calculus, discrete math, probability, linear algebra, statistics, optimization.

**Primary books / references:** Mathematics for Computer Science — Lehman, Leighton & Meyer; Calculus — Michael Spivak; Linear Algebra Done Right — Sheldon Axler; Introduction to Probability — Blitzstein & Hwang; Convex Optimization — Boyd & Vandenberghe; The Elements of Statistical Learning — Hastie, Tibshirani & Friedman.

**How to use the books:** Use the books as the primary learning material; use papers after each mathematical concept has been learned.

## Stage 2 — Programming & algorithms

**What to master:** Programming concepts, data structures, algorithms, complexity, graph theory.

**Primary books / references:** Structure and Interpretation of Computer Programs — Abelson & Sussman; The C Programming Language — Kernighan & Ritchie; Introduction to Algorithms — Cormen, Leiserson, Rivest & Stein; Algorithm Design — Kleinberg & Tardos; Concrete Mathematics — Graham, Knuth & Patashnik.

**How to use the books:** Learn the algorithmic concepts from the books, implement them yourself, then read seminal papers.

## Stage 3 — Computer architecture

**What to master:** Logic, ISA, CPU, memory hierarchy, parallelism, performance.

**Primary books / references:** Computer Organization and Design — Patterson & Hennessy; Computer Architecture: A Quantitative Approach — Hennessy & Patterson; Digital Design and Computer Architecture — Harris & Harris.

**How to use the books:** Use the introductory architecture text first, then the quantitative text for performance and modern architecture.

## Stage 4 — Operating systems

**What to master:** Processes, threads, virtual memory, filesystems, scheduling, virtualization.

**Primary books / references:** Operating Systems: Three Easy Pieces — Arpaci-Dusseau & Arpaci-Dusseau; Modern Operating Systems — Tanenbaum & Bos; The Linux Programming Interface — Michael Kerrisk; Operating System Concepts — Silberschatz, Galvin & Gagne.

**How to use the books:** Use OSTEP as the main conceptual text and Linux Programming Interface while doing practical Linux work.

## Stage 5 — Networking

**What to master:** TCP/IP, routing, congestion control, SDN, data-center networking.

**Primary books / references:** Computer Networking: A Top-Down Approach — Kurose & Ross; Computer Networks — Tanenbaum & Wetherall; TCP/IP Illustrated, Volume 1 — W. Richard Stevens.

**How to use the books:** Use Kurose/Ross as the main learning text and TCP/IP Illustrated for protocol-level depth.

## Stage 6 — Databases & distributed systems

**What to master:** Relational model, transactions, consensus, replication, distributed storage.

**Primary books / references:** Database System Concepts — Silberschatz, Korth & Sudarshan; Designing Data-Intensive Applications — Martin Kleppmann; Database Internals — Alex Petrov; Distributed Systems — van Steen & Tanenbaum.

**How to use the books:** Learn relational databases first, then use DDIA as the main bridge into distributed systems.

## Stage 7 — Theory & security

**What to master:** Computability, complexity, cryptography, security, adversarial ML.

**Primary books / references:** Introduction to the Theory of Computation — Michael Sipser; Computational Complexity — Arora & Barak; Introduction to Modern Cryptography — Katz & Lindell; Security Engineering — Ross Anderson; Serious Cryptography — Jean-Philippe Aumasson.

**How to use the books:** Build computability, complexity and cryptography foundations before tackling advanced theory/security papers.

## Stage 8 — Classical machine learning

**What to master:** Statistical learning, trees, SVMs, ensembles, evaluation.

**Primary books / references:** Pattern Recognition and Machine Learning — Christopher Bishop; The Elements of Statistical Learning — Hastie, Tibshirani & Friedman; Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow — Aurélien Géron; Probabilistic Machine Learning: An Introduction — Kevin Murphy.

**How to use the books:** Use Bishop/Murphy for theory and Géron for implementation; use ESL as the deeper statistical reference.

## Stage 9 — Deep learning

**What to master:** Backpropagation, CNNs, regularization, normalization, optimization.

**Primary books / references:** Deep Learning — Goodfellow, Bengio & Courville; Dive into Deep Learning — Zhang et al.; Understanding Deep Learning — Simon J.D. Prince; Neural Networks and Deep Learning — Michael Nielsen.

**How to use the books:** Use one theory-heavy book plus Dive into Deep Learning for implementation and experiments.

## Stage 10 — Sequence models & NLP

**What to master:** Language models, embeddings, RNN/LSTM, Seq2Seq.

**Primary books / references:** Speech and Language Processing — Jurafsky & Martin; Natural Language Processing with Transformers — Tunstall, von Werra & Wolf; Deep Learning for Natural Language Processing — Palash Goyal et al.

**How to use the books:** Learn NLP fundamentals first, then study embeddings, RNN/LSTM and Seq2Seq papers.

## Stage 11 — Attention & Transformers

**What to master:** Bahdanau attention → Transformer → BERT/GPT/T5 → efficient attention.

**Primary books / references:** Natural Language Processing with Transformers — Tunstall, von Werra & Wolf; Transformers for Natural Language Processing — Denis Rothman; Understanding Deep Learning — Simon J.D. Prince.

**How to use the books:** Use the books to understand attention mathematically and architecturally before reading the Transformer lineage.

## Stage 12 — Representation learning

**What to master:** Contrastive learning, masked modeling, multimodal learning.

**Primary books / references:** Deep Learning — Goodfellow, Bengio & Courville; Dive into Deep Learning — Zhang et al.; Understanding Deep Learning — Simon J.D. Prince.

**How to use the books:** Use the books to understand learned representations, contrastive objectives and self-supervised learning.

## Stage 13 — Computer vision

**What to master:** Detection, segmentation, ViT, NeRF and modern vision.

**Primary books / references:** Computer Vision: Algorithms and Applications — Richard Szeliski; Deep Learning for Vision Systems — Mohamed Elgendy; Multiple View Geometry in Computer Vision — Hartley & Zisserman.

**How to use the books:** Use Szeliski as the broad vision reference and the deep-learning text for modern neural vision.

## Stage 14 — Reinforcement learning

**What to master:** Q-learning, policy gradients, actor-critic, deep RL.

**Primary books / references:** Reinforcement Learning: An Introduction — Sutton & Barto; Algorithms for Reinforcement Learning — Csaba Szepesvári; Deep Reinforcement Learning Hands-On — Maxim Lapan.

**How to use the books:** Sutton & Barto is the conceptual spine; read the algorithm papers as each RL family is learned.

## Stage 15 — Generative models

**What to master:** VAE, GAN, diffusion, score-based models, latent diffusion.

**Primary books / references:** Probabilistic Machine Learning — Kevin Murphy; Deep Learning — Goodfellow, Bengio & Courville; Understanding Deep Learning — Simon J.D. Prince.

**How to use the books:** Establish probabilistic and deep-learning foundations before working through generative-model papers.

## Stage 16 — Large language models

**What to master:** Scaling laws, pretraining, instruction tuning, preference optimization, parameter-efficient fine-tuning.

**Primary books / references:** Build a Large Language Model (From Scratch) — Sebastian Raschka; Hands-On Large Language Models — Alammar & Grootendorst; Designing Machine Learning Systems — Chip Huyen.

**How to use the books:** Implement small language models and understand training/serving constraints before moving into large-scale LLM papers.

## Stage 17 — AI systems

**What to master:** Distributed training, inference, GPUs, memory efficiency, serving, monitoring and production ML systems.

**Primary books / references:** Designing Machine Learning Systems — Chip Huyen; Programming Massively Parallel Processors — Kirk & Hwu; Database Internals — Alex Petrov.

**How to use the books:** Connect system architecture concepts to the training and inference papers in the research library.

## Stage 18 — Advanced AI and multimodal systems

**What to master:** Multimodal models, agents, tool use, retrieval, reasoning and modern AI architectures.

**Primary books / references:** Natural Language Processing with Transformers — Tunstall, von Werra & Wolf; Hands-On Large Language Models — Alammar & Grootendorst; Understanding Deep Learning — Simon J.D. Prince.

**How to use the books:** Use the books as conceptual references while reading current advanced systems literature.

## Stage 19 — Responsible AI and research practice

**What to master:** Evaluation, robustness, fairness, safety, reproducibility, scientific communication and research methodology.

**Primary books / references:** The Craft of Research — Booth et al.; How to Read a Paper — Keshav; Fairness and Machine Learning — Barocas et al.

**How to use the books:** Apply the research-method principles throughout the entire paper-reading process rather than waiting until the end.

## Stage 20 — Research synthesis

**What to master:** Connect mathematical foundations, Computer Science theory, systems, ML and AI into independent research capability.

**Primary books / references:** Use the complete book library selectively according to the research problem, together with the relevant papers and implementation references.

**How to use the books:** At this stage, books become targeted references while primary research literature, experiments and original technical work become the main focus.
