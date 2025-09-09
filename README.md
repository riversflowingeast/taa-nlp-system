# taa-nlp-system
Research into enabling NLP and translation system for Taa language of the Khoisan family

## Roadmap

This project is in the **early research & prototyping stage**. Planned milestones:

- **Data digitization**
  - Scan and OCR dictionary resources
  - Normalize and structure entries (lemma, POS, senses, examples)
  - Collect and clean transcribed audio clips

- **Annotation & enrichment**
  - Define orthography and tokenization rules
  - Add POS/morphology tags and named entities
  - Use tools like Label Studio, ELAN, and FLEx

- **Core resources**
  - Build a bilingual lexicon (dictionary → EN ↔ Target)
  - Create small monolingual corpora via elicited speech and back-translations
  - Collect interlinear glossed texts (IGT) for analysis

- **Baselines**
  - Improve OCR accuracy with fine-tuning
  - Train a first ASR model (wav2vec2/Whisper) to speed up transcript creation
  - Prototype a rule/lexicon-based MT system

- **Neural models**
  - Train small Transformer MT with transfer + synthetic data
  - Iteratively improve with back-translation and lexicon constraints
  - Add post-processing for morphology and diacritics

- **Evaluation**
  - Track BLEU/chrF/COMET for MT
  - CER/WER for ASR
  - Maintain a frozen test set from day one

- **First demo**
  - End-to-end pipeline: EN → Target text
  - Optional TTS for voice output
  - Serve via a lightweight FastAPI API

- **Data growth**
  - Expand with everyday phrases, micro-stories, and domain packs (health, education, etc.)
  - Build a pronunciation lexicon for ASR/TTS
  - Collect continuous feedback for targeted improvements
