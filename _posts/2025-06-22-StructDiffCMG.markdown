---
title: "StructDiffCMG: Commit Message Generation with Structure and Semantics"
date: 2025-06-22 12:00:00 +0800
categories: [Research, AI, NLP]
tags: [Commit Message Generation, LLM, StructDiffCMG, Software Engineering]
---

# StructDiffCMG: A Hybrid Retrieval-Based Framework for Commit Message Generation

> **Structured Diff Representation and Sequential Hybrid Retrieval for Enhanced LLM-Based Commit Message Generation**

---

## 🧩 Motivation

Commit messages are critical in modern software development. They document code changes, support debugging, and facilitate team collaboration. Yet, due to time constraints or neglect, developers often leave vague or uninformative messages like “update” or “fix,” which harms future maintainability.

### 💡 Solution:

**StructDiffCMG** is a lightweight, training-free framework that generates accurate, stylistically consistent commit messages using structured diffs, exemplar retrieval, and LLMs.

---

## 🧱 System Architecture Overview

StructDiffCMG is composed of four core components:

### 1. 🗂 Structured Diff Representation

* Raw Git diffs are transformed into **structured JSON format** using a custom `DiffAnalyzer`.
* Captures:

  * File paths
  * Line-level additions/deletions/modifications
  * Context via hunk headers

> This structured format enables LLMs to better understand change semantics.

---

### 2. 🔍 Sequential Hybrid Retrieval

A two-stage retrieval strategy selects relevant exemplar commits from a dataset:

* **Stage 1: Semantic Filtering**

  * Uses `all-MiniLM-L6-v2` to embed diffs
  * FAISS is used to retrieve top-K similar diffs by vector distance

* **Stage 2: Lexical Re-ranking**

  * Applies TF-IDF to re-rank semantically similar candidates
  * Ensures both **contextual** and **stylistic alignment**

> The top exemplar diffs and their messages are used to construct LLM prompts.

---

### 3. 📤 Prompt Construction

* Prompts are built by inserting the **structured query diff** and the **retrieved exemplar pair(s)** into predefined templates.
* Two templates are used:

  * **Basic Prompt**: Only the input diff
  * **Advanced Prompt**: Includes retrieved examples for few-shot prompting

---

### 4. 🧼 Post-Processing

Enhances generated messages by:

* Normalizing and lemmatizing text
* Applying TF-IDF-based filtering
* Enforcing imperative tone (e.g., "Add logging", "Fix bug")
* Matching typical developer writing patterns

Example transformation:

```
Input: "FIXED login_bug: resolved the error 500 issue when users submit invalid credentials"
Output: "Fix authentication bug causing login error when user submits invalid credentials"
```

---

## 📊 Experimental Results

Tested on the **CommitBench** dataset (7,661 Java diffs), StructDiffCMG demonstrates **state-of-the-art performance**:

| Model Variant                   | BLEU      | ROUGE-L  | METEOR   |
| ------------------------------- | --------- | -------- | -------- |
| CommitGen                       | 1.36      | 10.59    | 9.17     |
| CodeT5 (fine-tuned)             | 9.68      | 27.20    | 23.65    |
| ChatGPT                         | 3.11      | 18.09    | 19.25    |
| Llama3 (70B) via REACT \[15]    | 4.84      | 19.88    | 20.58    |
| **StructDiffCMG (Qwen2.5, 7B)** | **11.38** | **26.3** | **23.2** |

> ✅ Outperforms fine-tuned and much larger models using only small open-weight LLMs (≤10B parameters).

---

## 🔬 Ablation Study: Component Contributions

| Variant     | Description                                   | BLEU (Llama3) |
| ----------- | --------------------------------------------- | ------------- |
| `basicNR`   | Basic LLM prompting, no retrieval             | 1.68          |
| `basic`     | Retrieval with no structuring/post-processing | 7.52          |
| `basicDA`   | Adds DiffAnalyzer (structured diffs)          | 10.16         |
| `basicDAPP` | Full system with post-processing              | **11.38**     |

> Each component (retrieval, structuring, post-processing) significantly improves output quality.

---

## ⏱ Inference Time

| Model         | `basic` | `basicDAPP` | `basicNR` |
| ------------- | ------- | ----------- | --------- |
| Llama3 (8B)   | 7378ms  | 8247ms      | 1213ms    |
| Qwen2.5-coder | 7000ms  | 7655ms      | 340ms     |
| Gemma2 (9B)   | 10400ms | 11169ms     | 2082ms    |

> While retrieval and post-processing introduce some latency, the accuracy gains justify the tradeoff for most scenarios.

---

## 🏆 Key Contributions

* ✅ Structured diff representation enhances model input clarity
* ✅ Sequential hybrid retrieval ensures contextual and lexical relevance
* ✅ Fully inference-based design—**no training or fine-tuning required**
* ✅ Effective across multiple open-weight LLMs (LLaMA3, Qwen2.5, Gemma2)

---

## 🚀 Future Work

* Integrating issue tracker or PR descriptions for deeper context
* Extending to more languages (e.g., Python, C++)
* Improving post-processing with syntax-aware logic
* Packaging as a GitHub Action or VSCode plugin

---

## 📘 Citation

```
@inproceedings{chen2025structdiffcmg,
  title={Structured Diff Representation and Sequential Hybrid Retrieval for Enhanced LLM-Based Commit Message Generation},
  author={Chen, Guanxuan},
  booktitle={TSC Thesis Symposium},
  year={2025}
}
```

---

## 🧠 Acknowledgments

This project was conducted at the Software Engineering Lab, National Tsing Hua University. Special thanks to the CommitBench authors and open-source LLM communities.

