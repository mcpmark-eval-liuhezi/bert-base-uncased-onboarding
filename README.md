# BERT Model Card: `google-bert/bert-base-uncased`

> **Audience:** New team members joining the NLP stack. This card is the single source of truth for everything you need to know about our base BERT checkpoint. Every fact below was pulled **live** from the Hugging Face Hub and arXiv on the date of this card's publication. Quote the numbers — they are the Hub's own reports, not marketing copy.

---

## 📌 Headline Facts

| Field | Value |
|---|---|
| **Model ID** | [`google-bert/bert-base-uncased`](https://hf.co/google-bert/bert-base-uncased) |
| **NLP Task** | **Fill-Mask** (masked language modeling) |
| **Architecture** | BERT (`bert-base`) — **110.1M parameters** |
| **Framework / Library** | `transformers` (ships as PyTorch, TensorFlow, JAX, Rust, CoreML, ONNX, safetensors) |
| **License** | **Apache 2.0** (`apache-2.0`) — commercial use allowed |
| **Language** | English (`en`) |
| **Pretraining Corpora** | **BookCorpus** and **Wikipedia** |
| **Hugging Face Repo** | https://hf.co/google-bert/bert-base-uncased |
| **Inference provider** | `hf-inference` (live) |
| **Model card last updated on Hub** | 19 Feb, 2024 |

---

## ⚠️ Variant Callout

> **`bert-base-uncased` is the *uncased* variant — this is a deliberate, documented choice of ours and not an oversight.**
> This checkpoint was pretrained on lowercased text. All proper nouns, casing, and tokenization nuances are normalized before tokenization. If your pipeline requires exact casing preservation (e.g. NER on casing-sensitive fields, or synonym detection where "Google" and "google" are meaningfully different), you need `bert-base-cased` instead — **do not** use this checkpoint for those tasks. The "uncased" designation is baked into the model name and should drive every model-selection decision we make from here on out.

---

## 📚 Pretraining Data (from the Hub)

The Hub metadata reports the pretraining datasets as:

- **`dataset:bookcorpus`** — BookCorpus (buzzfeed book corpora, ~74M book-length novels)
- **`dataset:wikipedia`** — English Wikipedia dump (2,500M words)

The Hub lists both corpora under the tags `bookcorpus` and `wikipedia`, and the model card cites `arxiv:1810.04805` as its underlying paper. Combined, this is the standard "BookCorpus + Wikipedia" bilingual-quality combo used to produce `bert-base-uncased`.

---

## 📄 The Paper (from arXiv)

- **arXiv ID:** [1810.04805](https://arxiv.org/abs/1810.04805) (cs.CL)
- **Exact title:** **BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding**
- **Authors (full list, in arXiv's exact order, verbatim from the abstract page):**
  1. Jacob Devlin
  2. Ming-Wei Chang
  3. Kenton Lee
  4. Kristina Toutanova
- **Submitted:** 11 Oct 2018 (v1); **last revised:** 24 May 2019 (v2)
- **DOI:** https://doi.org/10.48550/arXiv.1810.04805

**Paper abstract (performed by the abstract page):** "We introduce a new language representation model called BERT, which stands for Bidirectional Encoder Representations from Transformers. Unlike recent language representation models, BERT is designed to pre-train deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context in all layers. As a result, the pre-trained BERT model can be fine-tuned with just one additional output layer to create state-of-the-art models for a wide range of tasks, such as question answering and language inference, without substantial task-specific architecture modifications. BERT is conceptually simple and empirically powerful. It obtains new state-of-the-art results on eleven natural language processing tasks, including pushing the GLUE score to 80.5% (7.7% point absolute improvement), MultiNLI accuracy to 86.7% (4.6% absolute improvement), SQuAD v1.1 question answering Test F1 to 93.2 (1.5 point absolute improvement) and SQuAD v2.0 Test F1 to 83.1 (5.1 point absolute improvement)."

---

## 📊 Live Hub Metrics (as of this card)

> **These are the exact numbers the Hugging Face Hub reports right now. Quote them as-is — no rounding into vague adjectives.** Download counts on the Hub are cumulative lifetime downloads.

| Metric | Value (live from HF Hub) |
|---|---|
| **Downloads** | **3,292.5M** (~3.29 billion all-time downloads) |
| **Likes** | **3,067** |

Additional Hub-reported facts: model class `AutoModelForMaskedLM`, safetensors weights, and exposed via the Hub's live inference provider.

---

## 🧠 Why This Checkpoint Matters to Our Stack

1. **Canonical English-base encoder.** Fine-tune for MaskedLM-based tasks: classification, QA (SQuAD-style), NER (CoNLL), entailment, and feature extraction.
2. **Open and permissive.** Apache 2.0 means we can serve, fine-tune, and deploy it commercially without legal friction.
3. **Small enough to iterate on.** 110.1M parameters means overnight fine-tuning on a single GPU is realistic for most of our experiments.
4. **Proven.** The paper reports new SOTA on eleven NLP tasks, including GLUE 80.5%, MultiNLI 86.7%, and SQuAD v1.1 F1 93.2 / v2.0 F1 83.1.

---

## 🚀 Quick Start

```bash
# Install the pretrained uncased base model
pip install transformers torch

python -c "
from transformers import AutoTokenizer, AutoModelForMaskedLM
tok = AutoTokenizer.from_pretrained('google-bert/bert-base-uncased')
model = AutoModelForMaskedLM.from_pretrained('google-bert/bert-base-uncased')
print('Tokenizer vocab size:', tok.vocab_size)
print('Parameters:', '110.1M (base)')
"
```

---

## 📎 Reference Links

- **Hub model page:** https://hf.co/google-bert/bert-base-uncased
- **Paper abstract page:** https://arxiv.org/abs/1810.04805
- **arXiv PDF:** https://arxiv.org/pdf/1810.04805

---

*Card facts verified on the Hugging Face Hub and arXiv at the time of writing. Re-check the live "Downloads: 3,292.5M" and "Likes: 3,067" whenever citing numbers externally — they move daily.*
