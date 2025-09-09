## Project Plan

taa-nlp-system/
├── README.md
├── .gitignore
├── requirements.txt
├── data/
│   ├── raw/
│   ├── processed/
│   └── external/
├── notebooks/
├── src/
├── models/
├── reports/
│   └── figures/
├── tests/
└── docs/

0. Principles

Orthography: Decide early (spelling, diacritics, punctuation), write it down, and be consistent.

Versioning: Track everything (text, audio, lexicon, code) and keep metadata (speaker, topic, date, source).

1. Digitize & Structure the Data
1.1 Dictionary (book)

Scan: 300–600 dpi.

OCR: Start with Tesseract/Kraken. Fine-tune if script is poorly supported.

Layout parsing: Extract lemma, POS, senses, examples, notes.

Normalize: Unicode NFC/NFKC, diacritics, punctuation.

Schema example:

{
  "lemma": "...",
  "pos": "N/V/ADJ",
  "senses": [
    {"gloss_en": "...", "examples":[{"src":"...","tgt_en":"..."}]}
  ],
  "morph": {"root":"...", "affixes":[...]},
  "notes": "...",
  "source": "DictPage_123"
}


Quality loop: Spot-check, fix systemic errors, re-run.

1.2 Audio (transcribed clips)

Inventory: transcripts, speaker IDs, domain, recording conditions.

Clean: remove noise, standardize orthography.

Segment: utterances/sentences (ELAN/Praat/ASR toolkits).

Align: Montreal Forced Aligner/aeneas (optional).

2. Annotation & Enrichment

Guidelines: Write conventions for tokenization, segmentation, spelling.

Tokenization:

Clear word boundaries → whitespace + punctuation.

No clear boundaries → train SentencePiece (BPE/Unigram).

Linguistic layers (in order of payoff):

POS tags (small set first).

Lemmas + morphology.

Named entities.

Tools: Label Studio/Prodigy (text), ELAN (audio), FLEx/Toolbox (IGT).

3. Core Resources
3.1 Lexicon

Extract lemma ↔ gloss pairs (with sense IDs, POS).

Use dictionary examples as seed parallel data.

Encode affixes/alternations if available.

3.2 Monolingual Corpora

Elicit new text: record & transcribe stories/dialogues.

Back-translations: bilinguals translate English → target.

IGT sessions: morpheme-by-morpheme glossed texts.

4. OCR Improvement (optional)

Manually correct 50–200 pages → fine-tune OCR → re-OCR → repeat.

5. ASR Baseline

Why: speeds up transcript creation.

Recipe:

Encoder: wav2vec 2.0 / Conformer / Whisper.

Units: characters or subwords (SentencePiece).

Evaluate: CER/WER on held-out speakers.

Loop: Use ASR to bootstrap more transcripts with human corrections.

6. Machine Translation
6.1 Lexicon/Rule-Based Seed

Dictionary → phrase table.

Add morphology rules (plural, tense markers).

Minimal reordering rules (e.g., SVO→SOV).

Produces literal but understandable baseline.

6.2 Neural MT

Model: Small Transformer (Marian/Fairseq/OpenNMT).

Transfer: Start from multilingual NMT covering related languages.

Data strategies:

Dictionary-expanded templates.

Back-translation.

Round-trip filtering.

Paraphrased English inputs.

Constraints: Force key dictionary terms at decode time.

6.3 Post-processing

Detokenize.

Morphological generation (rules or FST).

Spell/diacritic restoration.

7. Evaluation

MT: BLEU/chrF (auto); COMET + human ratings (adequacy, fluency).

ASR: CER/WER by speaker/domain.

Best practice: Keep a frozen test set from day one.

8. First Demo (End-to-End Pipeline)

Input: English sentence(s).

Translate: NMT + lexicon constraints, fallback to dictionary rules.

Postprocess: Detokenize, inflect, restore diacritics.

Optional: TTS for a voice demo.

Serve: FastAPI API + lightweight on-device model.

9. Data Growth Plan

Everyday phrases, micro-stories, instructions (5–10k sentences).

Domain packs: health, finance, education (500–1k sentences each).

Pronunciation lexicon (ASR/TTS).

Continuous error logging → targeted collection.

10. Tool Stack

OCR: Tesseract/Kraken, eScriptorium, GROBID/regex.

Annotation: Label Studio, ELAN/Praat, FLEx/Toolbox.

ASR: ESPnet/Fairseq/Kaldi, wav2vec 2.0/Whisper.

MT: MarianNMT/Fairseq/OpenNMT, SentencePiece.

Morphology: HFST/Foma.

Evaluation: sacreBLEU/chrF, COMET, error spreadsheets.

Serving: FastAPI, ONNX export, quantized for mobile.
