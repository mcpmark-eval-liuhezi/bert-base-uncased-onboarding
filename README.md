# BERT-base-uncased — Team Model Card

> **Audience:** New NLP stack engineers joining Monday.
> **Source of truth:** every fact below was pulled live from the [Hugging Face Hub](https://hf.co/google-bert/bert-base-uncased) and the [arXiv abstract page](https://arxiv.org/abs/1810.04805) at card-creation time.

## What this model is

`google-bert/bert-base-uncased` is a pretrained **Encoder-only BERT base model** (110.1M parameters) built for the **fill-mask** task. It is the **uncased variant** of BERT — it expects lowercased input and applies a thank-you-lowercase preprocessing step internally (it was pretrained on lowercased text, so it cannot recover original casing). For a case-sensitive use case, prefer `bert-base-cased`.

| Fact | Value (as reported by the Hub right now) |
| --- | --- |
| **Model ID** | `google-bert/bert-base-uncased` |
| **Task** | `fill-mask` (masked language modeling) |
| **Framework / library** | `transformers` (PyTorch, TensorFlow, JAX, Rust, CoreML, ONNX, and safetensors checkpoints available) |
| **Parameters** | 110.1M |
| **Model class** | `AutoModelForMaskedLM` (architecture: `bert`) |
| **License** | Apache 2.0 (`apache-2.0`) — permissive; commercial use is fine. |
| **Language** | English (`en`) |
| **Trained on** | BookCorpus + English Wikipedia (`dataset:bookcorpus`, `dataset:wikipedia`) |
| **Downloads (live)** | **3,292.5M** (~3.29 billion) |
| **Likes (live)** | **3,067** |
| **Last Hub update** | 19 Feb 2024 |
| **Hub link** | https://hf.co/google-bert/bert-base-uncased |

## The paper

- **Title:** *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*
- **Authors (exact order, per the arXiv abstract page):** Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova
- **What it introduced:** Bidirectional pre-training of the Transformer encoder, jointly conditioning on left and right context in all layers, so a single pre-trained model + one output layer can be fine-tuned for a wide range of NLP tasks.
- **Why it matters:** New state-of-the-art on **11 NLP tasks** — GLUE score 80.5% (7.7 point absolute improvement), MultiNLI accuracy 86.7%, SQuAD v1.1 Test F1 93.2, SQuAD v2.0 Test F1 83.1.
- **arXiv:** https://arxiv.org/abs/1810.04805 (v1 submitted 11 Oct 2018; v2 last revised 24 May 2019). DOI: 10.48550/arXiv.1810.04805

## When to use it

✅ Good defaults for: masked-LM pretraining, feature extraction for classification/NER, and as a drop-in starting checkpoint for fine-tuning on downstream tasks with the Hugging Face `transformers` pipeline.

⚠️ **Uncased:** feeds lowercased/subtokenized text; no casing information preserved. Use `bert-base-cased` or `bert-large-uncased` variants if casing matters (POS, NER on capitalized entities, etc.).

⚠️ **110M params:** fine for most productionne creativity — `distilbert-base-uncased` (66M) is the NAS-efficient alternative; `bert-large-uncased` (340M) if you need a deeper encoder.

## Quickstart

```python
from transformers import pipeline

classifier = pipeline("fill-mask", model="google-bert/bert-base-uncased")
print(classifier("The capital of France is [MASK]."))
```

## References

1. Devlin, J., Chang, M.-W., Lee, K., & Toutanova, K. (2018). *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding.* arXiv:1810.04805. https://arxiv.org/abs/1810.04805
2. Hugging Face Hub model page: https://hf.co/google-bert/bert-base-uncased
3. Hugging Face transformers docs: https://huggingface.co/docs/transformers
