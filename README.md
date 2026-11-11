# BERT Base Uncased — Model Card

## https://huggingface.co/google-bert/bert-base-uncased

> One-page card for the new NLP stack. Every fact below was pulled fresh from the Hugging Face Hub and arXiv on the day this card was generated. Live numbers may drift — re-verify before citing.

## At a glance

| Fact | Value |
| --- | --- |
| **Model ID** | `google-bert/bert-base-uncased` |
| **Task** | `fill-mask` (masked language modeling) — the pretrain task; fine-tune it for classification, QA, NER, etc. |
| **Framework / Library** | `transformers` (pip package) — ships with PyTorch, TensorFlow, JAX, Rust, CoreML, ONNX, and safetensors weights |
| **License** | Apache-2.0 (`apache-2.0`) |
| **Parameters** | 110.1M |
| **Language** | English (`en`) |
| **Link** | https://hf.co/google-bert/bert-base-uncased |

## ⚠️ Variant call-out: this is the uncased model

**`bert-base-uncased` is the uncased variant, not the cased one.** All text is lowercased before tokenization (sentence case is preserved via WordPiece token IDs, but spelling and case distinction between words is thrown away). If your pipeline needs to distinguish case (e.g. acronyms like "NASA" vs "nasa", or consider casing as a signal for telemetry), use `bert-base-cased` instead. The `uncased` model is the default starting point for most English NLP fine-tuning.

## Pretraining corpora

Trained on two unlabeled English corpora (per the Hub): **BookCorpus** (11,038 unpublished books) and **English Wikipedia** (~2.5B words).

| Corpus | Content |
| --- | --- |
| `dataset:bookcorpus` | BookCorpus: 11,038 unpublished books |
| `dataset:wikipedia` | English Wikipedia (~2.5B words) |

## Paper

- **arXiv:** [1810.04805](https://arxiv.org/abs/1810.04805) — **"BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding"**
- **Authors (exactly as listed on arXiv):** Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova
- **arXiv ID:** arXiv:1810.04805 [cs.CL], submitted 11 Oct 2018 (v1), last revised 24 May 2019 (v2). Original submission from Ming-Wei Chang.
- **Abstract highlights:** BERT pre-trains deep bidirectional representations from unlabeled text by jointly conditioning on left and right context in all layers; it obtains new state-of-the-art results on eleven NLP tasks, including GLUE to 80.5%, MultiNLI accuracy to 86.7%, SQuAD v1.1 Test F1 93.2, and SQuAD v2.0 Test F1 83.1.

## Live numbers (as reported by the Hub right now)

- **Downloads:** **3,292.5M** (~3.29 billion)
- **Likes:** **3,067**
- **Model class:** `AutoModelForMaskedLM`
- **Last updated on Hub:** 19 Feb 2024
- **Demo spaces:** live (playground): https://hf.co/playground?modelId=google-bert/bert-base-uncased

## Model card usage notes for the stack

1. It is the **uncased** variant — lowercasing is baked in; pick `-cased` if casing matters.
2. Primary use case is **fill-mask** (masked language modeling); downstream tasks fine-tune with one added output layer.
3. Apache-2.0 license — permissive, commercial use permitted.
4. Uses safetensors weights for safe, fast loading.
