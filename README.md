# BERT base model (uncased)

**Model card for `google-bert/bert-base-uncased` — every fact below was pulled fresh from the Hugging Face Hub and the arXiv abstract page at the time of writing. Numbers are quoted exactly as the Hub reports them.**

> ⚠️ **This is the uncased variant.** `google-bert/bert-base-uncased` is the **uncased** (case-folded) base model. All input text is lowercased at the tokenizer (`bert-base-uncased`), it does not make a difference between `english` and `English`, and it **strips accent markers**. It is *not* the `bert-base-cased` model, which preserves case. If case information matters, use `bert-base-cased` instead.

---

## Quick facts (as reported by the Hugging Face Hub)

| Field | Value |
|---|---|
| **Model ID** | `google-bert/bert-base-uncased` |
| **NLP task** | `fill-mask` (masked language modeling / MaskedLM) |
| **Shipped library** | `transformers` (PyTorch, TensorFlow, JAX, Rust, CoreML, ONNX; safetensors weights) |
| **License** | `apache-2.0` |
| **Pretraining corpora** | BookCorpus + English Wikipedia (see below for exact Hub wording) |
| **Paper** | [arXiv:1810.04805](https://arxiv.org/abs/1810.04805) — cs.CL |
| **Downloads (live, per Hub)** | **3,292.5M** (~3.29 billion) |
| **Likes (live, per Hub)** | **3,067** |
| **Parameters** | 110M (110.1M per Hub metadata) |
| **Language** | `en` (English) |
| **Hub page** | https://huggingface.co/google-bert/bert-base-uncased |
| **Last updated on Hub** | 19 Feb 2024 |

---

## The paper behind it (title and author list verbatim from the arXiv abstract page)

**Title:** *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*
**arXiv ID:** 1810.04805 (cs.CL) — https://arxiv.org/abs/1810.04805 · submitted 11 Oct 2018 (v1), last revised 24 May 2019 (v2)
**Authors (full list, in order, taken directly from the arXiv page):** Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova

**Why Jacob Devlin is first:** confirmed — the arXiv abstract page lists **Jacob Devlin** as author #1, followed by Ming-Wei Chang, Kenton Lee, and Kristina Toutanova.

From the abstract: BERT (Bidirectional Encoder Representations from Transformers) is pre-trained with deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context in all layers. Fine-tuning with just one additional output layer yields state-of-the-art results on **eleven** NLP tasks: GLUE score 80.5% (7.7 point absolute improvement), MultiNLI accuracy 86.7% (4.6 point absolute improvement), SQuAD v1.1 Test F1 93.2 (1.5 point absolute improvement), SQuAD v2.0 Test F1 83.1 (5.1 point absolute improvement).

## Pretraining corpora (per the Hub model card on this repo's README)

- **BookCorpus** — a dataset consisting of **11,038 unpublished books**.
- **English Wikipedia** — the English Wikipedia with lists, tables, and headers excluded.

(Per Hub tags: `dataset:bookcorpus`, `dataset:wikipedia`, `language:en`, `license:apache-2.0`.)

## What it was pretrained with (per the Hub model card)

Two self-supervised objectives:

1. **Masked language modeling (MLM):** 15% of tokens are masked; 80% replaced with `[MASK]`, 10% with a random token, 10% left as-is.
2. **Next sentence prediction (NSP):** two sentences are concatenated as input; the model predicts whether they are consecutive in the original corpus or not.

Preprocessing: texts are lowercased and tokenized with WordPiece, vocabulary size of 30,000. Inputs have the form `[CLS] Sentence A [SEP] Sentence B [SEP]`. Trained on 4 cloud TPUs (16 TPU chips total) for 1 million steps, batch size 256, sequence length 128 tokens for 90% of steps and 512 for the remaining 10%. Adam optimizer, learning rate 1e-4, β₁ = 0.9, β₂ = 0.999, weight decay 0.01, 10,000-step warmup, then linear decay.

## What it's built for

- **Use it for:** masked language modeling (`pipeline("fill-mask", model="google-bert/bert-base-uncased")`), feature extraction from raw text, and fine-tuning on downstream tasks that use the whole (potentially masked) sentence — sequence classification, token classification / NER, and question answering.
- **Not for:** text generation (use GPT-2-style models instead).
- **Known bias (per the model card):** fill-mask output for "The woman worked as a [MASK]" ranks *nurse*, *waitress*, *maid*, *prostitute*, *cook* — fine-tuned derivatives inherit this bias too.

## Quick start (PyTorch)

```python
from transformers import pipeline

unmasker = pipeline("fill-mask", model="google-bert/bert-base-uncased")
unmasker("Hello I'm a [MASK] model.")
```

## Caveats for the team

1. **Uncased by design** — lowercase everything before tokenizing; accents are stripped.
2. **Fine-tune, don't raw-in-deploy** — it's a feature extractor / pretraining base; add an output layer for your task.
3. **Bias** — it has documented social biases in fill-mask; evaluate before shipping.
4. **Context limit** — 512 tokens (128 in most pretraining steps).
5. **Note on the `google-bert` org** — the canonical upstream release is `github.com/google-research/bert`; this `google-bert` repo on the Hub is the canonical hosting location for it.

---

*Sources: Hugging Face Hub model page `google-bert/bert-base-uncased` (Downloads: 3,292.5M · Likes: 3,067 · license: apache-2.0 · datasets: bookcorpus, wikipedia · task: fill-mask · last updated 19 Feb 2024), and the arXiv abstract page for 1810.04805 (paper title and full author list verbatim).*
