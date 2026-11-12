# BERT Model Card: google-bert/bert-base-uncased

> **NLP stack onboarding — one page.** Every fact below was pulled **fresh from the Hugging Face Hub** ([https://hf.co/google-bert/bert-base-uncased](https://hf.co/google-bert/bert-base-uncased)) and the **arXiv abstract page** ([https://arxiv.org/abs/1810.04805](https://arxiv.org/abs/1810.04805)) at the time of writing. Numbers are quoted exactly as the Hub reports them right now — nothing is rounded into vague adjectives.

---

## ⚠️ Read this first: this is the **uncased** variant

`google-bert/bert-base-uncased` is the **uncased (case-folded) BERT base model**. It was pretrained on **lowercased text** — all inputs are normalized to lowercase before processing. **Do not confuse it with** [`google-bert/bert-base-cased`](https://hf.co/google-bert/bert-base-cased), which preserves case (capital letters are kept as-is). For most general NLP tasks, start with `bert-base-uncased`. Switch to `bert-base-cased` only when case information matters (e.g. "Apple" vs "apple Inc.").

---

## The quick facts (as reported by the HF Hub right now)

| Field | Value |
| --- | --- |
| **Model ID** | `google-bert/bert-base-uncased` |
| **NLP task** | `fill-mask` (masked language modeling / MaskedLM) |
| **Shipped library / framework** | `transformers` |
| **License** | `apache-2.0` |
| **Pretraining corpora** | BookCorpus + English Wikipedia (Hub tags: `dataset:bookcorpus`, `dataset:wikipedia`, `language:en`) |
| **Paper** | [arXiv:1810.04805](https://arxiv.org/abs/1810.04805) — "BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding" |
| **Downloads** | **3293.6M** (~3.29 billion, as reported by the Hub right now) |
| **Likes** | **3070** (as reported by the Hub right now) |
| **Parameters** | 110.1M |
| **Architecture** | BERT (`bert`), model class `AutoModelForMaskedLM` |
| **Language** | `en` (English) |
| **Hub page** | https://hf.co/google-bert/bert-base-uncased |
| **Hub last updated** | 19 Feb, 2024 |

*Verified-live tags on the Hub page: `transformers`, `pytorch`, `tf`, `jax`, `rust`, `coreml`, `onnx`, `safetensors`, `bert`, `fill-mask`, `exbert`, `en`, `dataset:bookcorpus`, `dataset:wikipedia`, `arxiv:1810.04805`, `license:apache-2.0`, `endpoints_compatible`, `deploy:sagemaker`, `deploy:azure`, `region:us`.*

---

## The paper behind it (title + authors taken directly from the arXiv abstract page)

**Title:** *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*

**arXiv ID:** [1810.04805](https://arxiv.org/abs/1810.04805) · cs.CL · v1 submitted 11 Oct 2018, v2 revised 24 May 2019 · DOI: 10.48550/arXiv.1810.04805

**Authors (in order, exactly as listed on the arXiv abstract page):**

1. Jacob Devlin
2. Ming-Wei Chang
3. Kenton Lee
4. Kristina Toutanova

**Abstract (summary from the paper):** BERT (Bidirectional Encoder Representations from Transformers) is a new language representation model that pre-trains deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context in all layers. As a result, the pre-trained BERT model can be fine-tuned with just one additional output layer to create state-of-the-art models for a wide range of tasks (such as question answering and language inference) without substantial task-specific architecture modifications. BERT is conceptually simple and empirically powerful — it obtained new state-of-the-art results on **eleven** NLP tasks, including pushing the GLUE score to 80.5% (7.7% point absolute improvement), MultiNLI accuracy to 86.7% (4.6% absolute improvement), SQuAD v1.1 question answering Test F1 to 93.2 (1.5 point absolute improvement) and SQuAD v2.0 Test F1 to 83.1 (5.1 point absolute improvement).

---

## Pretraining corpora (per the Hub)

- **BookCorpus** — one of the two corpora the model card lists for pretraining (Hub tag: `dataset:bookcorpus`)
- **English Wikipedia** — the other pretraining corpus (Hub tag: `dataset:wikipedia`, language: `en`)

The Hub's metadata for this repo lists the datasets as `bookcorpus` and `wikipedia`, language `en`, license `apache-2.0`.

---

## How to use it

1. Load it with `transformers`:
```python
from transformers import AutoTokenizer, AutoModelForMaskedLM

tokenizer = AutoTokenizer.from_pretrained("google-bert/bert-base-uncased")
model = AutoModelForMaskedLM.from_pretrained("google-bert/bert-base-uncased")
```
2. Use the **matching uncased tokenizer** (`bert-base-uncased`, not `bert-base-cased`) — the model expects all-lowercase input.
3. Fine-tune on your downstream task (NER, QA, classification, etc.) with a single output layer on top of `AutoModelForMaskedLM`.
4. It ships in `safetensors` format and is deployable via Hugging Face inference endpoints.

---

## Where to go next

- HF Hub model page: https://hf.co/google-bert/bert-base-uncased
- arXiv paper: https://arxiv.org/abs/1810.04805
- Live playground: https://hf.co/playground?modelId=google-bert/bert-base-uncased
