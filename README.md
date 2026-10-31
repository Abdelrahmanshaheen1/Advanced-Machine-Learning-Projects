<div align="center">

# Advanced Machine Learning Projects

**Three projects across unsupervised learning, multimodal deep learning, and NLP with LLM prompting, each with the numbers its own notebook logged.**

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?logo=tensorflow&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?logo=scikitlearn&logoColor=white)
![Transformers](https://img.shields.io/badge/DistilBERT-fine--tuned-8a3ffc)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

## At a glance

| Project | Task | Approach | Headline result |
|---|---|---|---|
| [`01-clustering/`](01-clustering/) | Segment wholesale customers (UCI Wholesale Customers) | K-Means, Spectral Clustering, GMM, compared with 5 internal validation metrics | K-Means (K = 3): Silhouette 0.548, Davies-Bouldin 0.928 |
| [`02-image-captioning/`](02-image-captioning/) | Generate captions for images | InceptionV3 encoder + multi-task LSTM decoder, MS-COCO subset | BLEU-1 0.283 after a **1-epoch** run (limited compute) |
| [`03-emotion-classification/`](03-emotion-classification/) | Classify text into 6 emotions | RNN vs fine-tuned DistilBERT vs zero-shot, few-shot and chain-of-thought LLM prompting | DistilBERT 92.4% accuracy; RNN 90.1%; best LLM prompt 57.7% |

Each subfolder holds the original notebook, unmodified, and a README with the approach and the results as the notebook logged them.

## Contents

[Key results](#key-results) · [Highlights](#highlights) · [What I would do next](#what-i-would-do-next) · [Honest limitations](#honest-limitations) · [Layout](#repository-layout)

## Key results

**Emotion classification** (same 2,000-example test set for every approach):

| Approach | Accuracy | Macro F1 |
|---|---:|---:|
| **Fine-tuned DistilBERT** | **0.924** | 0.877 |
| RNN trained from scratch | 0.901 | 0.850 |
| LLM, few-shot (8 examples) | 0.577 | 0.523 |
| LLM, zero-shot | 0.557 | 0.530 |
| LLM, few-shot (3 examples) | 0.532 | 0.491 |
| LLM, chain-of-thought | 0.350 | 0.092 |

With only 500 training examples DistilBERT keeps 75.1% accuracy while the RNN falls to 21.8%.

**Image captioning** (1 epoch): BLEU-1 / 2 / 3 / 4 = 0.283 / 0.168 / 0.094 / 0.046.

**Clustering** (K-Means, K = 3): Silhouette 0.5483, Davies-Bouldin 0.9279, Calinski-Harabasz 140.14, Dunn 0.0288, Gap 3.4709.

## Highlights

**Clustering: every (algorithm, K) combination compared on Silhouette Score.** K-Means is ahead of Spectral Clustering and GMM; the other four validation metrics are in the notebook and the [report](01-clustering/AML-REPORT-proj1.pdf).

![Silhouette score for K-Means, Spectral Clustering and GMM at K = 2, 3, 4](docs/figures/clustering-silhouette-comparison.png)

**Emotion classification: accuracy vs. macro F1 for six approaches on the same 2,000-example test set.** Fine-tuned DistilBERT leads; chain-of-thought prompting scores lowest, a counter-intuitive result that is kept in the write-up.

![Accuracy and macro F1 for RNN, DistilBERT and LLM prompting strategies](docs/figures/emotion-accuracy-vs-macro-f1.png)

**Data efficiency: with only 500 training examples** DistilBERT still reaches 75.1% accuracy while the RNN drops to 21.8%.

![Test accuracy with 500 training examples vs. the full training set](docs/figures/emotion-data-efficiency.png)

## Honest limitations

- **Image captioning** was trained for a single epoch (`EPOCHS = 1`) on a reduced COCO subset because of limited compute, and its generated captions are still repetitive. The BLEU scores describe an early-stage model, not a tuned one; see [`02-image-captioning/`](02-image-captioning/).

## What I would do next

- **Captioning:** more epochs on a larger COCO subset and an attention mechanism, as the notebook itself notes; today's captions are generic and repetitive.
- **Emotion classification:** a stronger LLM baseline and a closer look at why chain-of-thought hurt on short texts.
- **Clustering:** check that the K = 3 choice is stable across random seeds and a different scaling.

## Repository layout

```text
.
├── 01-clustering/            # project1_AML.ipynb + AML-REPORT-proj1.pdf
├── 02-image-captioning/      # image_captioning.ipynb
├── 03-emotion-classification/# emotion_classification.ipynb
├── docs/figures/             # figures used in this README
└── LICENSE
```

## License

[MIT](LICENSE) © 2026 Abdelrahman Shaheen
