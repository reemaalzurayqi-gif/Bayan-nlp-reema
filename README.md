# Bayan NLP — Reema

Bayan is a bilingual Arabic/English NLP project developed as part of the SDA-AIE-211 Applied NLP course.

## Project Goal

The project builds and evaluates an NLP pipeline across multiple tasks while keeping preprocessing, evaluation, and model decisions measurable and documented.

## Day 1 — Text Processing, Tokenization, and Attention

### Text Processing
- Applied a two-copy preprocessing contract.
- Preserved the original text while preparing `model_text`.
- Applied conservative Arabic preprocessing.
- Applied PII masking.
- Verified preprocessing and tokenization tests.

### Tokenization
- Measured Token Fertility and truncation.
- Evaluated Arabic and English separately.
- Compared the local tokenizer with mBERT on five synthetic texts.
- The local tokenizer produced four [UNK] tokens across two Arabic texts; mBERT produced none in these samples.
- Kept the local tokenizer as the Day 1 teaching baseline and documented its Arabic coverage limitation.

### Attention and Transformers
- Implemented scaled dot-product attention.
- Verified attention weights sum to 1.
- Applied keep-mask semantics.
- Compared NumPy and PyTorch SDPA.
- Verified SDPA numerically across multiple seeds.
- Traced multi-head attention shapes.
- Audited two BERT-family checkpoints.
- Executed an actual Transformer forward pass on Arabic and English text.
- Visualized one attention head with token labels.

## Day 1 Verification

- Preprocessing and tokenization tests: PASS
- Attention tests: PASS
- `DAY1_NOTEBOOK1_CORE=PASS`
- `DAY1_NOTEBOOK2_CORE=PASS`

## Day 2 — Classification, NER, and Extractive QA

Day 2 work covers:

- Text classification with a TF-IDF baseline and Transformer training smoke test.
- Group-based data splitting to prevent leakage.
- NER label alignment using `word_ids()` and `-100`.
- Entity-level NER evaluation.
- Extractive QA with valid-span and no-answer handling.

Day 2 results will be reported as `MEASURED_SMOKE` and should not be interpreted as production-readiness claims.

## Status
- Day 1: Core completed
- Day 2: In progress
- Day 3: Pending
- Day 4: Pending

## Course
SDA-AIE-211 — Applied Natural Language Processing  
SDAIA Academy
