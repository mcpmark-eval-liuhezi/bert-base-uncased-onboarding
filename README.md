# BERT-base-uncased — Onboarding Model Card

> ** Philips research model pulled from the Hugging Face Hub.** All facts below were read
> live from [google-bert/bert-base-uncased](https://huggingface.co/google-bert/bert-base-uncased)
> and from the paper's arXiv abstract page ([arXiv:1810.04805](https://arxiv.org/abs/1810.04805))
> at the time this card was written.

---

## ⚠️ Read this first: this is the *uncased* variant

`bert-base-uncased` is the **uncased** checkpoint. All text is lowercased before
tokenization (and it handles approximate word matching, e.g., `T Training` → `training`).
This is **not** the cased variant — for case-sensitive use cases, prefer
`google-bert/bert-base-cased` (and similarly `bert-large-uncased`, `bert-large-cased`).
This card documents `bert-base-uncased` only.

---

## At a glance

| Field | Value (live from HF Hub) |
| --- | --- |
| **Model ID** | `google-bert/bert-base-uncased` |
| **Hugging Face link** | https://huggingface.co/google-bert/bert-base-uncased |
| **NLP task** | `fill-mask` (masked language modeling / masked LM pretraining) |
| **Framework / library** | `transformers` (ships as PyTorch, TensorFlow, JAX, Rust, CoreML, ONNX, safetensors) |
| **Model class** | `AutoModelForMaskedLM` |
| **Architecture** | `bert` (encoder-only Transformer) |
| **Parameters** | 110.1M |
| **License** | `apache-2.0` |
| **Language** | `en` (English) |
| **Pretraining corpora** | BookCorpus + Wikipedia (English) |
| **Downloads (live)** | **3,292.5M** (≈ 3.29 billion) |
| **Likes (live)** | **3,067** |
| **Last updated on Hub** | 19 Feb 2024 |
| **Inference provider** | `hf-inference` (live) ✅ Try it in the Hub playground |

---

## The paper behind this model

**Title (exact, from arXiv):** *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*
**arXiv ID:** [1810.04805](https://arxiv.org/abs/1810.04805) (cs.CL) · v1 submitted 11 Oct 2018, v2 revised 24 May 2019 · DOI: 10.48550/arXiv.1810.04805

**Authors (full list, in order, from the arXiv abstract page):**

1. Jacob Devlin
2. Ming-Wei Chang
3. Kenton Lee
4. Kristina Toutanova

Jacob Devlin is indeed the first author — confirmed from the arXiv page, not memory.

**Abstract in one sentence:** BERT pre-trains deep **bidirectional** representations from
unlabeled text by jointly conditioning on left and right context in all layers, so a
single added output layer can be fine-tuned for a wide range of NLP tasks; it set new
state-of-the-art results on **11** NLP tasks (GLUE 80.5%, MultiNLI 86.7%, SQuAD v1.1 F1
93.2, SQuAD v2.0 F1 83.1).

---

## Pretraining data

`bert-base-uncased` was pretrained on two English corpora:

- **BookCorpus** (≈ 748M words from unpublished books)
- **Wikipedia** (English Wikipedia, ~2.5B words per the paper)

For fine-tuning, this model is typically matched with GLUE, SQuAD, and other NLP task datasets.

---

## Quick start (Hugging Face `transformers`)

```python
from transformers import AutoTokenizer, AutoModelForMaskedLM

tokenizer = AutoTokenizer.from_pretrained("google-bert/bert-base-uncased")
model = AutoModelForMaskedLM.from_pretrained("google-bert/bert-base-uncased")

text = "The capital of France is [MASK]."
inputs = tokenizer(text, return_tensors="pt")
mask_idx = inputs["input_ids"][0].argmax()  # find the [MASK] position

with torch.no_grad():
    logits = model(**inputs).logits

predicted_id = logits[0, mask_idx].argmax()
print(tokenizer.decode(predicted_id))  # e.g. "paris"
```

---

## Checklist for new team members

- [ ] Clone/inspect the model: https://huggingface.co/google-bert/bert-base-uncased
- [ ] Remember: **uncased** → lowercase your inputs first
- [ ] Downloads: **3,292.5M** · Likes: **3,067** (as reported by the Hub today)
- [ ] Paper: Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova (arXiv:1810.04805)
- [ ] License: Apache 2.0 — fine for internal and commercial use
- [ ] Pretraining corpora: BookCorpus + English Wikipedia

---

## Sources

- Model card on the Hugging Face Hub: https://huggingface.co/google-bert/bert-base-uncased
- arXiv abstract page: https://arxiv.org/abs/1810.04805
- Repository: https://github.com/mcpmark-eval-liuhezi/bert-base-uncased-onboarding
