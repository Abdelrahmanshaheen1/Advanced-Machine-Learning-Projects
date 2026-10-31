# Image Captioning (CNN + Multi-Task LSTM)

Generates natural-language captions for images, trained on a subset of the [MS-COCO](https://cocodataset.org/) captioning dataset.

## Architecture

- **Image encoder:** InceptionV3 (ImageNet-pretrained), used as a fixed feature extractor.
- **Text decoder:** LSTM-based sequence generator over a tokenized caption vocabulary.
- **Multi-task setup:** trained jointly on two objectives — caption generation and an auxiliary image-classification head — sharing the encoded image representation.
- Captions are cleaned and filtered (minimum length) before tokenization; a custom data generator streams (image feature, partial caption) pairs in batches during training.

## Results (as logged by the notebook)

| Metric | Value |
|---|---|
| BLEU-1 | 0.283 |
| BLEU-2 | 0.168 |
| BLEU-3 | 0.094 |
| BLEU-4 | 0.046 |
| Auxiliary classification accuracy | 0.26 |

These are modest scores for an image-captioning model trained from scratch on a reduced COCO subset with limited compute (no pretrained captioning weights) — the project's value is in the end-to-end multi-task architecture (shared encoder, two decoder heads, custom batch generator) rather than state-of-the-art caption quality. The notebook includes qualitative examples of generated captions on held-out test images alongside the BLEU scores.

**Limitations:** training ran for a single epoch (`EPOCHS = 1`, as set in the notebook, which notes that training was limited by compute). The qualitative examples show generic captions (for example "a man in a suit and tie") that often miss the image content and repeat tokens (trailing `end end end`) instead of terminating cleanly, so the scores above describe an early-stage model. More epochs, a larger subset and an attention mechanism are the obvious next steps.

## Skills demonstrated

Multimodal model design (vision + language), transfer learning with a pretrained CNN encoder, custom Keras data generators for memory-efficient training on image-caption pairs, and multi-task loss design.

`image_captioning.ipynb` is the original, unedited notebook (large COCO annotation/image downloads are fetched at runtime, not committed to the repo).
