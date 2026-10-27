# Text Emotion Classification: RNN vs. Fine-Tuned Transformer vs. LLM Prompting

Classifies text into six emotions (sadness, joy, love, anger, fear, surprise), comparing three fundamentally different approaches on the same dataset and test set — including a data-efficiency study.

## Approaches compared

1. **RNN baseline** — an LSTM classifier (1.37M parameters) trained from scratch on a custom vocabulary.
2. **Fine-tuned transformer** — `distilbert-base-uncased`, fine-tuned on the training set via Hugging Face `Trainer`.
3. **LLM prompting (no training)** — the same test set classified via zero-shot, few-shot (3- and 8-shot), and chain-of-thought prompting against an LLM, with no task-specific training at all.

## Results (as logged by the notebook, 2,000-example test set)

| Model | Accuracy | Macro F1 | Inference time |
|---|---|---|---|
| **DistilBERT (fine-tuned)** | **0.924** | 0.877 | 1.8s |
| RNN (trained from scratch) | 0.901 | 0.850 | 0.3s |
| LLM — few-shot (8 examples) | 0.577 | 0.523 | 86s |
| LLM — zero-shot | 0.557 | 0.530 | 92s |
| LLM — few-shot (3 examples) | 0.532 | 0.491 | 84s |
| LLM — chain-of-thought | 0.350 | 0.092 | 91s |

**Data-efficiency study:** with only 500 training examples, DistilBERT still reached 75.1% accuracy while the RNN dropped to 21.8% — showing the transformer's pretrained representations transfer far better under low-data conditions. Zero-shot LLM prompting (0.557, no training data at all) sits between the two, outperforming both models when they're starved of data but trailing both once they have the full training set.

**Interesting negative result:** chain-of-thought prompting *underperformed* plain zero-shot prompting on this task (0.35 vs. 0.56 accuracy) — reasoning steps didn't help, and in some cases actively hurt, a short-text emotion-classification task. This kind of result is worth keeping precisely because it's counter to the usual "CoT helps" narrative.

## Skills demonstrated

Rigorous model comparison under a controlled test set, correct use of fine-tuning vs. prompting for a classification task, LLM-as-classifier evaluation (including less-common comparisons like CoT prompting and training-data-efficiency curves), and honest reporting of negative/counter-intuitive results.

`emotion_classification.ipynb` is the original, unedited notebook.
