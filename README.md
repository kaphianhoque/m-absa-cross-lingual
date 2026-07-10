# Cross-Lingual ABSA: XLM-RoBERTa vs mT5 on M-ABSA

This repo contains the experimental code accompanying the systematic literature
review *"Cross-Lingual Aspect-Based Sentiment Analysis on Low-Resource Languages:
XLM-RoBERTa vs mT5 on M-ABSA."*

## Project goal

Compare a discriminative multilingual model (XLM-RoBERTa) against a generative
multilingual model (mT5) on aspect-based sentiment triplet extraction, using the
[M-ABSA dataset](https://huggingface.co/datasets/Multilingual-NLP/M-ABSA), with a
focus on zero-shot transfer to low-resource languages (Arabic, Hindi, Swahili,
Vietnamese).

## Research questions

1. Does XLM-RoBERTa outperform mT5 on M-ABSA for aspect sentiment triplet extraction?
2. How effective is XLM-RoBERTa at zero-shot transfer to low-resource languages?
3. Does cross-domain training improve XLM-RoBERTa's cross-lingual transfer performance?

## Repo structure

```
├── data/            # scripts/notebooks for loading & subsetting M-ABSA (raw data not committed)
├── notebooks/        # Colab notebooks for fine-tuning and evaluation
├── src/               # reusable Python modules (data prep, training, eval)
├── results/          # output tables, metrics, plots (generated, not raw data)
├── LICENSE
├── CITATION.cff
└── README.md
```

## Dataset

M-ABSA (Wu et al., 2025): 21 languages, 7 domains, aspect-category-sentiment
triplets. Not committed to this repo — loaded directly from HuggingFace at
runtime. See `data/` for loading scripts.

## Models

- **XLM-RoBERTa** (`xlm-roberta-base`) — fine-tuned as a token classification /
  tagging model.
- **mT5** (`mt5-base` or `mt5-small`) — fine-tuned as a text-to-text model,
  generating triplets directly in the dataset's native format.

Both are fine-tuned on English only, then evaluated zero-shot on low-resource
target languages.

## Status

🚧 Work in progress — literature review complete, experiments in progress.

## Citation

If you use this code, please cite the accompanying paper (see `CITATION.cff`)
and the original M-ABSA dataset paper:

```
@misc{wu2025mabsa,
      title={M-ABSA: A Multilingual Dataset for Aspect-Based Sentiment Analysis},
      author={Chengyan Wu and Bolei Ma and Yihong Liu and Zheyu Zhang and Ningyuan Deng and Yanshu Li and Baolan Chen and Yi Zhang and Yun Xue and Barbara Plank},
      year={2025},
      eprint={2502.11824},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```

## License

MIT — see `LICENSE`.
