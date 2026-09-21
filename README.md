# BERT base model (**uncased**) — `google-bert/bert-base-uncased`

> One-page onboarding card for our NLP stack. Every fact below was pulled fresh from the
> [Hugging Face Hub](https://hf.co/google-bert/bert-base-uncased) and the
> [arXiv abstract page](https://arxiv.org/abs/1810.04805) at the time this card was generated —
> nothing from memory.

## ⚠️ Read this first: this is the **uncased** variant

This model is **uncased**: it does not make a difference between `english` and `English`. All input
text is lowercased, and the uncased BERT models also **strip out accent markers**. If you need
capitalization or accents to matter (e.g., NER on proper nouns), you likely want the cased sibling
[`bert-base-cased`](https://hf.co/google-bert/bert-base-cased) instead — don't mix the two up when
comparing results.

## At a glance

| | |
|---|---|
| **Hub repo** | [`google-bert/bert-base-uncased`](https://hf.co/google-bert/bert-base-uncased) |
| **NLP task** | `fill-mask` — masked language modeling (MLM); a bidirectional **encoder**, not a text generator |
| **Framework** | Ships as a Hugging Face **`transformers`** model (`AutoModelForMaskedLM` / `BertModel`) |
| **Weight formats** | PyTorch, TensorFlow, JAX (repo is also tagged `rust`, `coreml`, `onnx`, `safetensors`) |
| **License** | **Apache 2.0** (`apache-2.0`) |
| **Parameters** | 110M |
| **Language** | English (`en`) |
| **Downloads (live, as the Hub reports)** | **3,237.2M** (≈ 3.24 billion) |
| **Likes (live, as the Hub reports)** | **3,365** |
| **Hub repo last updated** | 19 Feb 2024 |

## What it's built for

BERT is pretrained with a **masked language modeling (MLM)** objective: take a sentence, randomly
mask 15% of the input words, run the whole masked sentence through the model, and predict the masked
words. Unlike RNNs or autoregressive models such as GPT, it sees **both left and right context in
every layer**, so it learns a bidirectional representation. It was also pretrained with **Next
Sentence Prediction (NSP)**: given two concatenated sentences, predict whether they were adjacent in
the original text.

These are the **pretrained base weights** — not a task-tuned model. The intended workflow is to
**fine-tune** it on a downstream task that uses the whole sentence to make decisions: sequence
classification, token classification, question answering, and so on. For text *generation*, use an
autoregressive model like GPT-2 instead.

Day-one sanity check:

```python
from transformers import pipeline

unmasker = pipeline("fill-mask", model="bert-base-uncased")
unmasker("Hello I'm a [MASK] model.")
# [{'token_str': 'fashion'}, {'token_str': 'role'}, {'token_str': 'new'}, ...]
```

Feature extraction in PyTorch or TensorFlow:

```python
from transformers import BertTokenizer, BertModel            # PyTorch
from transformers import BertTokenizer, TFBertModel          # TensorFlow

tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")
model = BertModel.from_pretrained("bert-base-uncased")       # or TFBertModel.from_pretrained(...)
encoded_input = tokenizer("Replace me by any text you'd like.", return_tensors="pt")
output = model(**encoded_input)
```

## Pretraining corpora

Pretrained **self-supervised on raw English text only** — no human labeling — using two corpora:

- **BookCorpus** — a dataset of 11,038 unpublished books
- **English Wikipedia** — excluding lists, tables, and headers

## The paper behind it

- **arXiv ID:** [1810.04805](https://arxiv.org/abs/1810.04805) — submitted 11 Oct 2018, last revised 24 May 2019 (v2), in *Computation and Language (cs.CL)*
- **Exact title (verbatim from the arXiv abstract page):**
  **BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding**
- **Full author list, in order (verbatim from the arXiv abstract page):**
  1. Jacob Devlin
  2. Ming-Wei Chang
  3. Kenton Lee
  4. Kristina Toutanova

Original code release: [google-research/bert](https://github.com/google-research/bert). Note that the
team releasing BERT did not write a model card for this model — the Hub card was written by the
Hugging Face team.

## Caveats to know before you fine-tune

- **Societal bias is baked in.** The training corpora encode gender and other stereotypes, and that
  bias propagates into every fine-tuned version of this model. Check your outputs before shipping.
  Documented example from the Hub card: `unmasker("The woman worked as a [MASK].")` returns
  *nurse*, *waitress*, *maid*… among top predictions, while the "man" prompt returns *carpenter*,
  *waiter*, *barber*…
- **Check for existing fine-tuned versions first** on the
  [Hub](https://hf.co/models?filter=bert) — for standard tasks someone may have already done the work.
- **Other variants exist** (base/large × cased/uncased, whole-word masking, multilingual). The full
  release history is in the [google-research/bert README](https://github.com/google-research/bert/blob/master/README.md).

---

*Downloads and likes above are quoted exactly as the Hugging Face Hub reported them when this card
was generated; re-verify at <https://hf.co/google-bert/bert-base-uncased> before citing them
elsewhere. Paper title and author order verified against <https://arxiv.org/abs/1810.04805>.*
