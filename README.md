# BERT base uncased — Onboarding Model Card

**Source repo:** [google-bert/bert-base-uncased](https://hf.co/google-bert/bert-base-uncased)
**Facts:** pulled live from the Hugging Face Hub + arXiv abstract page (arXiv:1810.04805) at the time of writing. Downloads and likes are quoted exactly as the Hub reports them — refresh them before citing in a blog post.

## The one-liner

`google-bert/bert-base-uncased` is **the uncased** BERT encoder checkpoint: a 110.1M-parameter bidirectional Transformer (encoder only) pre-trained on English, for the **fill-mask** task. This card tells you everything a new NLP team member needs to know on day one.

## What the "uncased" in the name means

This is the **uncased** variant. All input text is lowercased before tokenization, so `BERT` and `bert` are handled identically. Don't confuse it with `bert-base-cased` — pick **uncased** unless you specifically need case sensitivity.

## Core facts (as reported by the Hugging Face Hub right now)

| Field | Value |
| --- | --- |
| **NLP task** | `fill-mask` (masked language modeling) — served via `AutoModelForMaskedLM` |
| **Framework / library** | Hugging Face `transformers` (also ships: PyTorch, TensorFlow, JAX, Rust, CoreML, ONNX, safetensors) |
| **License** | apache-2.0 |
| **Pretraining corpora** | BookCorpus + English Wikipedia (`language:en`) |
| **Parameters** | 110.1M |
| **Downloads** | 3,292.5M (~3.29 billion) |
| **Likes** | 3,067 |
| **Model class / architecture** | `AutoModelForMaskedLM` / `bert` |
| **Language** | English (`en`) |
| **Last updated on Hub** | 19 Feb 2024 |
| **Inference** | available via [hf-inference](https://hf.co/playground?modelId=google-bert/bert-base-uncased) playground |

## The paper (arXiv:1810.04805)

- **Exact title:** *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*
- **Authors (exact order, from the arXiv abstract page):** Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova
- **arXiv:** [https://arxiv.org/abs/1810.04805](https://arxiv.org/abs/1810.04805) · [v2, submitted 11 Oct 2018, last revised 24 May 2019]
- **What it did:** bidirectional pre-training of a Transformer encoder on unlabeled text (left + right context in all layers), which can be fine-tuned with just one added output layer for state-of-the-art results across a wide range of tasks — question answering, language inference, and more. It set new SOTA on **eleven** NLP tasks, incl. GLUE 80.5% (7.7-point absolute improvement), MultiNLI 86.7%, SQuAD v1.1 F1 93.2, and SQuAD v2.0 F1 83.1.
- **Why this model card exists:** BERT is the workhorse of our stack's encoder layer. `bert-base-uncased` is the base-size checkpoint we recommend for most English pretraining/transfer-learning recipes.

## Quick start (transformers)

```python
from transformers import pipeline

# fill-mask = the task this checkpoint was pre-trained for
masker = pipeline("fill-mask", model="google-bert/bert-base-uncased")
print(masker("The capital of France is [MASK]."))
```

Then fine-tune on top with `Trainer` / `TFTrainer` for your downstream task.

## Links

- Model page: https://hf.co/google-bert/bert-base-uncased
- arXiv: https://arxiv.org/abs/1810.04805
- License: Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0)
- More checkpoints in the same family: `bert-base-cased`, `bert-large-uncased`, `bert-large-cased`, and their distilled variants (`distilbert-base-uncased`).
