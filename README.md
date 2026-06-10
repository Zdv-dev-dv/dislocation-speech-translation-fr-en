# dislocation-speech-translation-fr-en

Data and code companion to the M2 thesis *Dislocation under Translation: A Corpus
Study of Whisper and XLS-R on Spontaneous Spoken French* (Zoé de Vries, Université
Paris Cité, 2026; supervised by Prof. Ballier).

## Pipeline

`01_whisper` → `02_xlsr` → `03_align` → `04_score`

1. **01** transcribes/translates the CFPP2000 recording with Whisper and defines the
   874-segment canonical grid (`segment_translations.csv`, columns `whisper_en_per_seg`,
   `whisper_en_cont`).
2. **02** runs XLS-R (CTC ASR + direct FR→EN ST) on the same grid, adding `xlsr_en`.
3. **03** aligns the 79 annotated dislocations to their segment span.
4. **04** scores each output against the CALQUE and IDIOMATIC references
   (BLEU, chrF, TER via sacrebleu; COMET via `Unbabel/wmt22-comet-da`).

## Data (`data/`)

| File | Rows | Content |
|---|---|---|
| `dislocation_test_set.csv` | 79 | annotated dislocations + references (gold) |
| `segment_translations.csv` | 874 | canonical grid + Whisper/XLS-R per-segment outputs |
| `dislocation_translations.csv` | 79 | dislocations + model outputs over their span |
| `dislocation_scores.csv` | 79 | 24 metric scores (3 hyps × 2 refs × 4 metrics) |

**Provenance.** `dislocation_translations.csv` and `dislocation_scores.csv` are the
hand-verified, thesis-canonical artefacts. Notebook 03 documents the alignment
*method*; re-running it reproduces the spans but may differ from the committed
dislocation-level outputs (notably `whisper_en_cont`), finalised in a spreadsheet
workflow. The committed CSVs are canonical.

The audio is **not** redistributed; notebooks download it at run time from the public
CFPP2000 URL.

## AI-assistance disclosure

Explanatory comments and markdown were drafted with
LLM assistance and reviewed by the author.
