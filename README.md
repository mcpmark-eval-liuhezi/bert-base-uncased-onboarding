# BERT base uncased — Onboarding Model Card

> **Welcome to the NLP stack.** This is a one-page cheat sheet for `google-bert/bert-base-uncased`. Every fact below was pulled **fresh from the Hugging Face Hub** and the **arXiv abstract page** on the day this card was written — no vague adjectives, just the live numbers as the Hub reports them.

---

## ⚠️ First thing to know: this is the **uncased** variant

`bert-base-uncased` is **not** the same as `bert-base-cased`. With the uncased variant, **all text is lowercased before tokenization** (`Everything` → `everything`). This means:

- The model **does not retain any case information** — capitalization is stripped before it ever sees the text.
- It is the **recommended default** for most English NLP tasks (GLUE benchmark, SQuAD, etc.) because ~95% of English text is already lowercase.
- If your task depends on casing (named entities like "Apple" vs "apple Inc.", acronyms, negation cues), use `bert-base-cased` instead.

---

## What this model is

| Field | Value (as reported by the Hub right now) |
|---|---|
| **Model ID** | `google-bert/bert-base-uncased` |
| **Hugging Face URL** | https://hf.co/google-bert/bert-base-uncased |
| **NLP task** | `fill-mask` (masked language modeling) — a masked-LM pre-trained encoder |
| **Shipped library / framework** | `transformers` (model class `AutoModelForMaskedLM`, architecture `bert`) |
| **Shipped formats** | PyTorch, TensorFlow, JAX, Rust, CoreML, ONNX, safetensors checkpoints |
| **License** | Apache 2.0 (`apache-2.0`) |
| **Parameters** | 110.1M |
| **Language** | English (`en`) |
| **Pretraining corpora** | BookCorpus + English Wikipedia (`dataset:bookcorpus`, `dataset:wikipedia`) |
| **Downloads** | **3,292.5M** (~3.29 billion, as reported on the Hub) |
| **Likes** | **3,067** (as reported on the Hub right now) |
| **Model card last updated** | 19 Feb 2024 |

The Hub also tags it `endpoints_compatible`, `deploy:sagemaker`, `deploy:azure`, `region:us`, and it is available via the HF inference provider and playground.

---

## The paper behind it

- **Title (exact, quoted from the arXiv abstract page):** *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*
- **arXiv ID:** [1810.04805](https://arxiv.org/abs/1810.04805) — cs.CL; v1 submitted 11 Oct 2018; current version v2, 24 May 2019. DOI: 10.48550/arXiv.1810.04805
- **Authors (exact order, straight from the arXiv abstract page):**
  1. **Jacob Devlin**
  2. **Ming-Wei Chang**
  3. **Kenton Lee**
  4. **Kristina Toutanova**

  (Submitted by Ming-Wei Chang, Google AI Language.)

- **What it does:** BERT (Bidirectional Encoder Representations from Transformers) pre-trains deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context in all layers. A single pre-trained BERT + one added output layer can be fine-tuned to create state-of-the-art models for a wide range of NLP tasks without task-specific architecture changes.
- **Headline results (from the abstract):** new state-of-the-art on **eleven NLP tasks** — GLUE score 80.5% (7.7-point absolute improvement), MultiNLI accuracy 86.7% (4.6-point absolute improvement), SQuAD v1.1 Test F1 93.2 (1.5-point absolute improvement), SQuAD v2.0 Test F1 83.1 (5.1-point absolute improvement).

---

## Quick start (copy-paste)

```python
from transformers import pipeline

# Masked LM — the model's native task
masker = pipeline("fill-mask", model="google-bert/bert-base-uncased")
print(masker("The capital of France is [MASK]."))
```

Fine-tuning on downstream tasks (NER, QA, classification) is the standard recipe: load with `AutoModelForMaskedLM` / `AutoTokenizer`, then fine-tune with one extra classification head. The Hub's [fill-mask](https://hf.co/google-bert/bert-base-uncased) demo Space and the [HF playground](https://hf.co/playground?modelId=google-bert/bert-base-uncased) are good sandboxes for experiments.

---

## TL;DR for Monday morning

1. **Uncased = lowercased input** — no case information retained. Reach for `bert-base-cased` when casing matters.
2. It's a **fill-mask** (masked language modeling) model: ~110.1M params, Apache 2.0, English.
3. Pretrained on **BookCorpus + Wikipedia**.
4. It ships via the **`transformers`** library in **PyTorch / TensorFlow / JAX / Rust / CoreML / ONNX / safetensors**.
5. Backed by the paper **"BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding"** (Devlin, Chang, Lee, Toutanova — arXiv:1810.04805).
6. Live stats as of card date: **~3.29B downloads, 3,067 likes** on the Hub.
