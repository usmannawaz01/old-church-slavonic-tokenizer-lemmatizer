# Old Church Slavonic Lemmatization Benchmark

This repository contains reproducibility scripts for Old Church Slavonic tokenization and lemmatization experiments with Stanza.

The trained tokenizer and lemmatizer model weights are available on Hugging Face:

```text
https://huggingface.co/usmannawaz/old-church-slavonic-tokenizer-lemmatizer
```

## Overview

This repository provides scripts for:

- raw-text prediction;
- gold-tokenized lemmatization evaluation;
- CoNLL-U evaluation using the official UD evaluation script.

The training dataset is not redistributed in this repository.

## Installation

```bash
pip install -r requirements.txt
```

Recommended `requirements.txt`:

```text
stanza
huggingface_hub
```

## Model weights

The model weights are downloaded from Hugging Face during script execution.

Available model variants:

```text
models/new-data/   tokenizer and lemmatizer trained on the newly annotated OCS dataset
models/combined/   tokenizer and lemmatizer trained on the new dataset + UD Old Church Slavonic PROIEL
```

## Experiment modes

### Raw-text mode

Raw-text mode evaluates the full pipeline:

```text
raw text → retrained tokenizer → official Stanza POS → retrained lemmatizer → CoNLL-U
```

Run:

```bash
python scripts/run_raw_stanza.py
```

### Gold-tokenized mode

Gold-tokenized mode evaluates lemmatization with fixed gold token boundaries:

```text
gold CoNLL-U tokens → official Stanza POS → retrained lemmatizer → predicted CoNLL-U
```

Run:

```bash
python scripts/run_goldtok_stanza.py
```

## Evaluation

Use the official CoNLL-U 2018 evaluation script:

```bash
python scripts/conll18_ud_eval.py -v gold.conllu prediction.conllu
```



## Repository structure

```text
ocs-lemmatization-benchmark/
├── README.md
├── requirements.txt
├── .gitignore
├── scripts/
│   ├── run_raw_stanza.py
│   ├── run_goldtok_stanza.py
│   └── evaluate_conllu.py
├── data/
│   └── README.md
├── results/
│   └── README.md
└── configs/
    └── paths.example.json
```

## Data availability

The training dataset is not redistributed in this repository.

Users should place local input files under `data/` or update paths in the scripts.

Official Stanza pretrained POS models are not redistributed. They are downloaded by Stanza during execution.

## License

Code in this repository is released under Apache-2.0.

Model weights are hosted on Hugging Face under CC BY-NC-SA 4.0.

## Citation

If you use this repository or the model weights, please cite the associated Old Church Slavonic lemmatization benchmark paper, Stanza, and UD Old Church Slavonic PROIEL where applicable.

```bibtex
@inproceedings{nawaz2025ocslemmatization,
  title = {Towards Benchmarking Old Church Slavonic Lemmatization},
  author = {Nawaz, Usman and others},
  year = {2025}
}
```

```bibtex
@inproceedings{qi2020stanza,
  title = {Stanza: A Python Natural Language Processing Toolkit for Many Human Languages},
  author = {Qi, Peng and Zhang, Yuhao and Zhang, Yuhui and Bolton, Jason and Manning, Christopher D.},
  booktitle = {Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics: System Demonstrations},
  pages = {101--108},
  year = {2020}
}
```
