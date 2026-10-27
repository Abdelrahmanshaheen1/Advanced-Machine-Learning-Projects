# Advanced Machine Learning Projects

Three course projects spanning unsupervised learning, multimodal deep learning, and NLP/LLM evaluation.

| Project | Task | Approach |
|---|---|---|
| [`01-clustering/`](01-clustering/) | Unsupervised segmentation of wholesale customers | K-Means, Spectral Clustering, GMM — compared with 5 internal validation metrics |
| [`02-image-captioning/`](02-image-captioning/) | Generate natural-language captions for images | CNN (InceptionV3) encoder + multi-task LSTM decoder, trained on MS-COCO |
| [`03-emotion-classification/`](03-emotion-classification/) | Classify text into 6 emotions | RNN baseline vs. fine-tuned DistilBERT vs. zero/few-shot & chain-of-thought LLM prompting |

Each subfolder contains the original notebook, unmodified, plus a README summarizing the approach and the results as logged by the notebook's own output cells.
