# Changelog

This file records significant milestones and structural changes to the OSSU Computer Science learning repository.

## 2026-08-13

### Documentation Standards

- Established the research-note writing convention: research notes record established understanding, explanations, mathematical detail and conclusions rather than presenting the learning process as a sequence of questions.
- Preserved equations, derivations, comparisons, technical explanations and implementation targets as part of the permanent research record.
- Moved unresolved interpretations, genuine ambiguity and items requiring further verification to an **Open Points / Ambiguities** section at the end of research notes.
- Documented the distinction in `README.md`: `notes/` contains course and general knowledge notes, while `research/notes/` contains paper-specific research notes.
- Corrected the multi-head attention equation formatting in `research/notes/attention-is-all-you-need.md` so the complete equation is contained in a single GitHub-compatible `$$ ... $$` display block.
- Verified the research-note display equations use `$$ ... $$` delimiters and contain no `\operatorname` notation.
- Expanded the **Attention Is All You Need** research note with integrated backpropagation and softmax foundations while preserving the existing Transformer equations, architecture explanations, implementation targets and research connections.
- Added an **Intuition First** section explaining softmax and backpropagation intuitively before the mathematical treatment.
- Added the mathematical connection between softmax, scaled dot-product attention, cross-entropy, gradients and end-to-end Transformer learning.

### Repository Structure

- Established a clear separation between general/course knowledge notes under `notes/` and paper-specific research notes under `research/notes/`.
- Added dedicated knowledge-note areas for Mathematics, Programming, Algorithms, Systems, Networking, Databases, Security, Machine Learning and AI.

### Research Progress

- Began studying **Attention Is All You Need** (#122).
- Began studying **Tensor Product Attention Is All You Need** as supplemental current research.
- Added dedicated research notes for both papers.
- Added mathematical explanations covering Q/K/V projections, scaled dot-product attention and multi-head attention.
- Added implementation targets, research questions and comparative analysis.
- Added the TPA project reference alongside the arXiv paper.
- Corrected GitHub-incompatible LaTeX notation in the research notes.
- Added detailed notes on backpropagation, the chain rule, softmax, softmax derivatives, softmax scaling, cross-entropy and their relationship to Transformer training.
- Added `research/notes/transformer-backpropagation.md` continuing the mathematical treatment from the chain rule and linear transformations through attention, softmax and Q/K/V gradient paths.

## 2026-08-12

### Added

- Added the **Study Environment** documentation covering the Windows 11 Pro laptop, Ventoy portable laboratory, Ubuntu desktop and Proxmox VE home laboratory.
- Added the **Study Plan** section.
- Added the OSSU CS Timeline workbook, containing the `Timeline` and `Curriculum Data` sheets.
- Added the GitHub-readable `CURRICULUM.md` derived from the `Curriculum Data` sheet, preserving the existing course links.
- Added the research roadmap covering Computer Science, Mathematics, AI and Machine Learning.
- Migrated the complete **257-entry research library** into the public `research/` directory with the existing links preserved.
- Added the **36 primary books/references** used by the research sequence.
- Added the **20-stage reading sequence** connecting books, papers and progressively deeper Computer Science/AI topics.
- Added the **12 end-state capability areas** for the research track.
- Added the research reading tracker and indexed paper ranges.

### Progress Recorded

The following OSSU curriculum items were recorded as completed:

- **#1 — Introduction to Computer Science and Programming using Python**
- **#4 — Programming Languages, Part A**
- **#9 — Calculus 1A: Differentiation**
- **#10 — Calculus 1B: Integration**

### Documentation Standards

- Public documentation uses normal professional capitalization for headings, topics and technical names.
- Server hostnames are written in lowercase, for example `pve-main` and `pve-chaos`.
- Private home-server information is excluded from the public repository.
- Credentials, keys, passwords, private addresses and other sensitive infrastructure information are not committed.
