# Cross-Lingual ABSA: XLM-RoBERTa vs mT5 on M-ABSA

This repository contains the experimental code and results accompanying our study:

**"Cross-Lingual Aspect-Based Sentiment Analysis on Low-Resource Languages: XLM-RoBERTa vs mT5 on M-ABSA."**

The project investigates multilingual Aspect-Based Sentiment Analysis (ABSA), with a focus on model architecture, zero-shot cross-lingual transfer, and domain generalization in lower-resource languages.

## Project Goal

The main objective of this project is to compare a discriminative multilingual transformer, **XLM-RoBERTa**, with a generative multilingual transformer, **mT5**, on multilingual aspect-based sentiment analysis.

The study also examines:

- zero-shot transfer from English to typologically diverse languages,
- the influence of language similarity and language family,
- the effect of cross-domain training,
- and whether combining model predictions through an ensemble can improve performance.

## Research Questions

1. How do XLM-RoBERTa and mT5 compare on multilingual ABSA tasks?
2. How effectively do multilingual models transfer zero-shot from English to lower-resource languages?
3. How do linguistic similarity and language family affect cross-lingual transfer?
4. Does domain-diverse training improve cross-lingual generalization?
5. Can an ensemble of XLM-RoBERTa and mT5 improve performance over individual models?

## Dataset

We use the **M-ABSA dataset** (Wu et al., 2025), a multilingual benchmark containing:

- 21 languages
- 7 domains
- aspect-category-sentiment annotations

Dataset source:

https://huggingface.co/datasets/Multilingual-NLP/M-ABSA

The raw dataset is not committed to this repository and is loaded directly from Hugging Face at runtime.

## Models

### XLM-RoBERTa

`xlm-roberta-base`

Fine-tuned as a discriminative token-classification/tagging model for aspect-based sentiment extraction.

### mT5

`mt5-base` / `mt5-small`

Fine-tuned as a generative text-to-text model that generates aspect-category-sentiment outputs directly.

## Tasks

The experiments cover:

- **TASD — Target-Aspect-Sentiment Detection**
- **UABSA — Unified Aspect-Based Sentiment Analysis**
- **Zero-Shot Cross-Lingual Transfer**
- **Cross-Domain Generalization**
- **Confidence-Weighted Ensemble Evaluation**

## Key Results

### Model Comparison

mT5 outperformed XLM-RoBERTa in our experimental setting.

| Model | TASD F1 | UABSA F1 |
|---|---:|---:|
| XLM-RoBERTa | 0.5159 | 0.5334 |
| mT5 | 0.6169 | 0.6809 |

### Ensemble

A confidence-weighted ensemble combining XLM-RoBERTa and mT5 achieved:

**TASD F1: 0.6645**

This outperformed either standalone model on the TASD task.

## Zero-Shot Cross-Lingual Transfer

Models were trained on English restaurant-domain data and evaluated without additional fine-tuning on multiple languages, including:

- Croatian
- Arabic
- Hindi
- Swahili
- Thai
- Vietnamese

The results showed substantial variation across languages.

Transfer performance was stronger for some linguistically closer languages, while lower-resource and typologically distant languages generally presented greater challenges.

However, linguistic family alone did not fully explain performance differences.

## Domain Generalization

We compared:

- restaurant-only training
- restaurant + hotel + food training

Domain diversity significantly affected transfer performance for only a subset of languages.

Notably:

- performance improved for Vietnamese,
- performance decreased for Swahili and Hindi,
- several other languages showed no statistically significant change.

Paired bootstrap significance testing with **1,000 resamples** was used to evaluate the reliability of these differences.

## Main Findings

- mT5 outperformed XLM-RoBERTa on both TASD and UABSA.
- Generative modeling was more effective than token classification in our experimental setting.
- The ensemble achieved the strongest TASD performance.
- Zero-shot cross-lingual transfer performance varied substantially across languages.
- Linguistic similarity influenced transfer, but did not fully explain the results.
- Domain-diverse training did not consistently improve multilingual transfer.
- Cross-lingual ABSA performance depends on the interaction between model architecture, language characteristics, and domain similarity.

## Research Gap & Limitations

This study addresses the limited exploration of how **linguistic distance and domain variation jointly affect zero-shot multilingual ABSA**, particularly for lower-resource languages.

However, the study is limited by the languages and domains available in M-ABSA, relies primarily on English as the source language for zero-shot transfer, and shows uneven performance across target languages. Further work could explore multilingual source training, additional low-resource languages, larger models, and deeper qualitative error analysis.

## Repository Structure

```text
├── data/
│   └── scripts/notebooks for loading and preprocessing M-ABSA
├── notebooks/
│   └── model training and evaluation notebooks
├── src/
│   └── reusable Python modules
├── results/
│   └── evaluation tables, metrics, and plots
├── figures/
│   └── visualizations used in the analysis
├── README.md
├── LICENSE
└── CITATION.cff
