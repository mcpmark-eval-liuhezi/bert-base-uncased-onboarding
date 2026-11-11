# BERT Model Card: google-bert/bert-base-uncased

> **Team onboarding reference — one page.** All facts below were pulled fresh from the Hugging Face Hub and the arXiv abstract page on the date of writing. Numbers are quoted exactly as the Hub reports them; nothing is rounded into vague adjectives.

## ⚠️ Read this first: this is the **uncased** variant

`google-bert/bert-base-uncased` is the **uncased** (case-folded) pre-trained BERT base model. It has been trained on lowercased text — it normalizes all inputs to lowercase before processing. **Do not confuse it with** `google-bert/bert-base-cased`, which preserves case (capital letters are kept as-is). For most general NLP tasks, start with `bert-base-uncased`. Switch to `bert-base-cased` only when case information matters (e.g. named entities like "Apple" vs "apple Inc.").

## The quick facts

| Field | Value (as reported by the HF Hub) |
| --- | --- |
| **Model ID** | `google-bert/bert-base-uncased` |
| **NLP task** | `fill-mask` (masked language modeling / MaskedLM) |
| **Shipped library** | `transformers` (PyTorch, TensorFlow, JAX, Rust, CoreML, ONNX, safetensors) |
| **License** | `apache-2.0` |
| **Pretraining corpora** | BookCorpus + English Wikipedia |
| **Paper** | [arXiv:1810.04805](https://arxiv.org/abs/1810.04805) |
| **Downloads** | **3,292.5M** (~3.29 billion) |
| **Likes** | **3,067** |
| **Parameters** | 110.1M |
| **Architecture** | BERT (`AutoModelForMaskedLM`) |
| **Language** | `en` (English) |
| **Hub page** | https://hf.co/google-bert/bert-base-uncased |
| **Last updated on Hub** | 19 Feb 2024 |

## The paper behind it (from the arXiv abstract page)

**Title:** *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*
**arXiv ID:** [1810.04805](https://arxiv.org/abs/1810.04805) · cs.CL · v1 submitted 11 Oct 2018, v2 revised 24 May 2019
**Authors (in order, taken directly from the arXiv abstract page):**
Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova

The abstract of the paper states that BERT (Bidirectional Encoder Representations from Transformers) is a new language representation model that pre-trains deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context in all layers, so the pre-trained model can be fine-tuned with just one additional output layer to create state-of-the-art models for a wide range of tasks — including question answering and language inference — with no substantial task-specific architecture modifications. It obtained new state-of-the-art results on **eleven** NLP tasks, including a GLUE score of 80.5% (7.7 point absolute improvement), MultiNLI accuracy of 86.7% (4.6 point absolute improvement), SQuAD v1.1 Test F1 of 93.2 (1.5 point absolute improvement) and SQuAD v2.0 Test F1 of 83.1 (5.1 point absolute improvement).

## Pretraining corpora (per the Hub)

- **BookCorpus** — a collection of ~74M words from 11,038 unpublished books
- **English Wikipedia** — ~2,500M words (2.5B words in the Hub's English Wikipedia text corpus)

Hub tags list: `dataset:bookcorpus`, `dataset:wikipedia`, `language:en`, `license:apache-2.0`, `endpoints_compatible`, `deploy:sagemaker`, `deploy:azure`, `region:us`.

## How to use it

1. Load it with `transformers`:
```python
from transformers import AutoTokenizer, AutoModelForMaskedLM

tokenizer = AutoTokenizer.from_pretrained("google-bert/bert-base-uncased")
model = AutoModelForMaskedLM.from_pretrained("google-bert/bert-base-uncased")
```
2. Tokenize with the **matching uncased tokenizer** (`bert-base-uncased`, not `bert-base-cased`) — the model expects all-lowercase input.
3. Fine-tune on your downstream task (NER, QA, classification, etc.) with a single output layer on top of `AutoModelForMaskedLM`.
4. It ships in safetensors format and is deployable via HF inference endpoints.

## Where to go next

- HF Hub model page: https://hf.co/google-bert/bert-base-uncased
- arXiv paper: https://arxiv.org/abs/1810.04805
- Live playground: https://hf.co/playground?modelId=google-bert/bert-base-uncased
