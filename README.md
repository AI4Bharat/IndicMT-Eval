# IndicMT-Eval

This repository contains the code for the paper "IndicMT Eval: A Dataset to Meta-Evaluate Machine Translation Metrics for Indian Languages" to appear at ACL 2023

## Contents

- [Overview](#overview)
- [MQM Dataset](#mqm)
- [Setup](#setup)
- [Indic Comet](#indiccomet)
- [Metrics](#metircs)
- [Citation](#citation)

## Overview

We contribute a Multidimensional Quality Metric (MQM) dataset for Indian languages created by taking outputs generated by 7 popular MT systems and asking human annotators to judge the quality of the translations using the MQM style guidelines. Using this rich set of annotated data, we show the performance of 16 metrics of various types on evaluating en-xx translations for 5 Indian languages. We provide an updated metric called Indic-COMET which not only shows stronger correlations with human judgement on Indian languages, but is also more robust to perturbations. 

Please find more details of this work in our paper (link coming soon).

## MQM Dataset

The MQM annotated dataset collected with the help of language experts for the 5 Indian lamguages (Hindi, Tamil, Marathi, Malayalam, Gujarati) can be downloaded from here (link coming soon).

## Setup

### Install Dependencies

Our code is based on python 3.7 and to install all the dependencies run the following command. <br>

```
pip install -r requirements.txt
```
### Load the data

All the original datasets used in our experiments can be directly downloaded by running the following command.

```
cd data
bash download.sh
```

## Indic Comet
We load the pretrained encoder and initialize it with either XLM-Roberta, COMET-DA or COME-MQM weights. During training, we divide the model parameters into two groups: the encoder parameters, that include the encoder model and the regressor parameters, that include the parameters from the top feed-forward network. We apply gradual unfreezing and discriminative learning rates, meaning that the encoder model is frozen for one epoch while the feed-forward is optimized with a learning rate. After the first epoch, the entire model is fine-tuned with a different learning rate. Since we are fine-tuning on a small dataset, we make use of early stopping with a patience of 3. The best saved checkpoint is decided using the overall Kendall-tau correlation on the test set. The training hyper-parameters used are given in table below.

<br> 

| Task| Link(s) |
 | Hyperparameters | Value |
 | ----------------| ------| 
  | batch size | 16 |
  | dropout | 0.1 |
  | encoder learning rate | 1.0e-05 |
  | encoder model | XLM-RoBERTa |
  | hidden sizes | 3072, 1536 |
  |  layer | mix |
  | layerwise decay | 0.95 |
  | learning rate | 3.0e-05 |
  | no. of frozen epochs | 1 |
  | optimizer | AdamW |
  | pool | avg |
  
  <br> 

  Download the best checkpoint here (link coming soon)

## Other Metrics

We followed the implementation of metrics with the help of the following repositories:
 For BLEU, METEOR, ROUGE-L, CIDEr, Embedding Averaging, Greedy Matching, and Vector Extrema, we use the implementation provided by [Sharma et al. (2017)](https://github.com/Maluuba/nlg-eval). For chrF++, TER, BERTScore, and BLEURT, we use the repository of [Castro Ferreira et al. (2020)](https://github.com/WebNLG/GenerationEval).  For SMS, WMDo, and Mover-Score, we use the implementation provided by [Fabbri et al. (2020)](https://github.com/Yale-LILY/SummEval). For all the remaining task-specific metrics, we use the official codes from the respective papers.

## Citation
Coming soon
