---
title: "StructDiffCMG: A Commit Message Generation Framework"
date: 2025-06-22 12:00:00 +0800
categories: [Research, AI]
tags: [Commit Message Generation]
---

### Beyond "Fix Bug": Unlocking Smarter Commit Messages with AI

### The Hidden Cost of Vague Commit Messages

Every developer knows the drill: you've just finished a complex piece of code, fixed a tricky bug, or implemented a new feature. The next step? Writing a commit message. Often, in the rush of deadlines, this crucial task becomes an afterthought. We've all seen (or written!) commit messages like "Update" or "Fix bug." While seemingly minor, this common habit has significant implications for software maintenance, team collaboration, and overall project quality. Vague commit messages obscure intent, make debugging a nightmare, and hinder effective communication among team members.

The field of **Automatic Commit Message Generation (CMG)** aims to solve this problem by leveraging computational approaches to summarize code changes automatically and meaningfully. But generating high-quality, human-like commit messages from raw code differences (diffs) is a non-trivial challenge.

---

### The Evolution of CMG: From Retrieval to Hybrid Approaches

Early CMG efforts largely fell into two categories:

1. **Retrieval-Based Methods (e.g., NNGen, CC2Vec):** These methods scoured historical commit repositories for similar code changes and simply reused their corresponding messages. While straightforward, they often struggled with novel changes or unique coding styles, acting more like a "copy-paste" solution than true generation.

2. **Learning-Based Methods (e.g., CommitGen, CoDiSum, PtrGNCMsg, FIRA):** These approaches utilized deep learning (RNNs, Transformers, GNNs) to learn mappings between code diffs and natural language descriptions. They offered greater adaptability and context awareness, capable of generating new messages, but often faced challenges with out-of-vocabulary (OOV) terms and capturing fine-grained structural information.

More recently, **Hybrid Methods** have emerged, attempting to combine the strengths of both. Approaches like ATOM, CoRec, and RACE demonstrated the power of retrieval-augmented generation (RAG) by using similar past commits to guide new message generation. Our work, **StructDiffCMG**, builds upon these advancements, pushing the boundaries further by integrating novel retrieval, representation, and post-processing techniques.

---

### Introducing StructDiffCMG: Our Novel Hybrid Framework

StructDiffCMG is designed to generate precise, informative, and stylistically consistent commit messages. It achieves this through a powerful combination of optimized information retrieval, a unique structured data representation, and an intelligent post-processing pipeline, all powered by Large Language Models (LLMs).

Here's how StructDiffCMG works:

#### 1. Two-Stage Hybrid Retrieval Strategy

Unlike prior methods that might perform semantic and lexical searches in parallel, StructDiffCMG employs a **sequential two-stage retrieval** process to find the most relevant historical commit examples (exemplars):

- **Step 1: Semantic Pre-filtering:** We convert the query code diff into a dense semantic vector using a **Sentence Transformer** model (specifically **all-MiniLM-L6-v2**). This embedding captures the high-level meaning of the code change. We then use **Faiss**, a high-performance similarity search library, to quickly retrieve the top-K (typically 10) semantically similar diffs from our pre-indexed CommitBench dataset. This efficiently narrows down the pool to conceptually relevant candidates.

- **Step 2: Lexical Re-ranking:** From these top-K candidates, we apply a second filter based on **TF-IDF (Term Frequency-Inverse Document Frequency)** cosine similarity. This step prioritizes candidates that also share specific keywords, variable names, and function names with the query diff. By combining semantic and lexical similarity, we ensure the selected exemplars are both conceptually aligned and linguistically relevant, significantly enhancing the quality of the prompt for the LLM.

#### 2. Structured Code Diff Representation with DiffAnalyzer

Raw Git diffs are notoriously hard for LLMs to fully interpret due to their unstructured, line-by-line nature. To address this, we developed **DiffAnalyzer**. This crucial component parses raw Git diff outputs and transforms them into a **custom-designed structured JSON format**.

This structured representation systematically extracts:

- File-level metadata (original and new filenames).
- Hunk structures (contiguous blocks of changes) including starting line numbers and lengths.
- Line-level changes, explicitly categorizing them as additions, deletions, or modifications.
- Contextual lines around the changes.

This rich, machine-readable JSON format allows the LLM to more comprehensively capture the contextual information and intent behind the code changes, going beyond just surface-level text.

#### 3. LLM-Powered Commit Message Generation

With the query diff transformed into structured JSON and highly relevant exemplars (structured diff + their human-written messages) retrieved, StructDiffCMG uses a carefully crafted prompt template to guide the LLM. We evaluated our approach with various open-source LLMs, including **Llama 3 (8B)**, **Gemma 2 (9B)**, and **Qwen2.5-Coder (7B)**. The prompt provides a concrete example from past development, enabling the LLM to generate concise, accurate, and convention-aligned commit messages through in-context learning.

#### 4. Robust Post-Processing Pipeline

To further enhance the clarity, quality, and practical usefulness of the generated messages, StructDiffCMG includes an advanced multi-stage post-processing pipeline:

1. **Normalization:** Standardizes text (lowercase, punctuation removal, underscore replacement, numeric exclusion).
2. **Tokenization & Lemmatization:** Breaks text into words and unifies grammatical variants.
3. **Enhanced Stopword Filtering:** Removes common filler words while preserving domain-specific terms using TF-IDF analysis on a commit message corpus.
4. **Pattern Matching:** A greedy algorithm identifies informative verb-noun structures (e.g., "fix bug," "submit credential") based on statistical analysis from the CommitBench dataset.
5. **Reconstruction:** Reassembles selected patterns into fluent, imperative-form messages adhering to professional standards.
6. **Error Handling:** Fallback mechanisms for malformed inputs ensure robustness.

For instance, a raw input like:

`"FIXED_login_bug: resolved the error 500 issue when users submit invalid credentials (ID#45)"`

might be refined to:

`"Fix authentication bug causing login error when user submits invalid credentials."`

### Impressive Results: Outperforming State-of-the-Art with Smaller Models

Our experiments, conducted on the widely recognized CommitBench dataset (90,661 Java diff-message pairs), demonstrate that StructDiffCMG (our most comprehensive variant, **basicDAPP**) significantly outperforms existing methods across standard metrics like **BLEU**, **ROUGE-L**, and **METEOR**.

Here's a snapshot of our key findings compared to prior state-of-the-art approaches:

| Approach | BLEU | ROUGE-L | METEOR |
|:---------|:-----|:--------|:-------|
| CodeT5 | 9.68 | 27.20 | 23.65 |
| Llama 3 (70B) | 4.84 | 19.88 | 20.58 |
| **StructDiffCMG (Llama 3 - 8B)** | **10.16** | **26.4** | **23.2** |
| **StructDiffCMG (Gemma 2 - 9B)** | **10.32** | **27.5** | **23.9** |
| **StructDiffCMG (Qwen2.5-Coder - 7B)** | **11.38** | **26.3** | **23.2** |

- **Significant Performance Boost:** StructDiffCMG achieves BLEU scores exceeding 10, ROUGE-L scores of 27.5, and METEOR scores of 23.9.
- **Efficiency Advantage:** Remarkably, our approach, using LLMs with **fewer than 10 billion parameters**, consistently outperforms even much larger models like Llama 3 (70B) and fine-tuned CodeT5 models. For example, our **Gemma 2 (9B)** variant surpasses all models reported in previous work for METEOR and ROUGE-L, and achieves a strong BLEU score.
- **Component Effectiveness:** Our ablation study confirms that each component – retrieval augmentation, structured diff representation via DiffAnalyzer, and post-processing – contributes substantially to these performance gains. For instance, **basicDAPP** improved BLEU scores by up to 705.6% on Mistral-Nemo compared to the **basicNR** baseline (no retrieval or processing).

While StructDiffCMG does introduce some computational overhead due to retrieval and processing steps (making it slower than basic LLM generation), the trade-off is justified by the significant boost in message quality and its ability to achieve state-of-the-art results with smaller, more efficient models.

### The Future of Commit Messages

StructDiffCMG represents a significant leap forward in automatic commit message generation. By integrating an intelligent two-stage retrieval mechanism, a robust structured diff representation, and a sophisticated post-processing pipeline, we offer a practical and scalable solution that generates high-quality, relevant, and stylistically consistent commit messages.

This not only promises to **enhance developer productivity** by automating a tedious task but also **improves overall software project maintainability** by ensuring clearer, more informative version histories.

Our future work includes exploring the integration of external context like **issue tracker data** and extending support to a wider range of **programming languages** to further enhance the framework's generalizability and real-world impact.

