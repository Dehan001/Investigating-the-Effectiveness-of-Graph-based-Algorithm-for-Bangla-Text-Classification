# Investigating-the-Effectiveness-of-Graph-based-Algorithm-for-Bangla-Text-Classification
<!--
﻿# [**TinyLLM Efficacy in Low-Resource Language: An Experiment on Bangla Text Classification Task**](#)

This release contains the official code for downstream fine-tuning and prompt-based classification, as detailed in the paper [**TinyLLM Efficacy in Low-Resource Language: An Experiment on Bangla Text Classification Task**](#), published in the *27th International Conference on Pattern Recognition (ICPR), 2024*.

### Table of Contents

- [Introduction](#introduction)
- [Datasets](#datasets)
- [Benchmarks](#benchmarks)
- [Acknowledgements](#acknowledgements)
- [Citation](#citation)

### Introduction

Our study explores the effectiveness of large and tiny language models in Bangla text classification, covering tasks like sentiment analysis, sarcasm detection, emotion recognition, hate speech identification, and fake news detection. In a resource-scarce linguistic landscape, we find that Gemma-2B and Bangla-BERT excel in various tasks, with Gemma-2B leading in hate speech and sarcasm detection and BanglaBERT in sentiment and emotion analysis. TinyLlama also stands out for its accuracy in fake news detection. We highlight the importance of model selection tailored to Bangla's unique challenges, noting that Bangla language models are particularly adept at capturing social media sentiments, while large language models are more effective in identifying misinformation and abusive language in formal sources. Our comparison with ChatGPT’s zero-shot prompting further underscores the need for advanced NLP techniques, showcasing TinyLLM's potential in advancing Bangla text classification.

### Datasets

This study utilizes five distinct datasets, each tailored to specific Bangla text classification tasks, including sentiment analysis, sarcasm detection, fake news detection, hate speech analysis, and emotion detection.

- [SentNoB](https://github.com/Abu-Kowcher-Rmstu/SentNoB)
- [Bangla Sarcasm Detection Dataset](https://www.kaggle.com/datasets/sakibapon/banglasarc)
- [BanFakeNews](https://www.kaggle.com/datasets/cryptexcode/banfakenews)
- [Hate Speech Dataset](https://github.com/rezacsedu/Bengali-Hate-Speech-Dataset)
- [YouTubeCommentsEmotion](https://www.kaggle.com/datasets/nit003/bangla-youtube-sentiment-and-emotion-datasets)

### Benchmarks

#### Bangla Language Models (BLMs)

| Dataset              | Model                          | Accuracy | Macro F1 | Weighted F1 |
|----------------------|--------------------------------|----------|----------|-------------|
| SentNoB              | BanglaBERT                     | **74.46**| **69.55**| **73.03**   |
|                      | BanglaBERT-Large               | 72.82    | 68.87    | 72.05       |
|                      | BanglaBERT (Sagor Sarker)      | 69.42    | 64.54    | 68.01       |
| Sarcasm Detection    | BanglaBERT                     | **95.67**| **95.51**| **95.68**   |
|                      | BanglaBERT-Large               | 94.55    | 94.23    | 94.50       |
|                      | BanglaBERT (Sagor Sarker)      | 90.46    | 90.13    | 90.48       |
| Hate Speech Detection| BanglaBERT                     | **69.33**| 41.65    | 65.41       |
|                      | BanglaBERT-Large               | 66.11    | 58.59    | **66.96**   |
|                      | BanglaBERT (Sagor Sarker)      | 67.11    | **61.43**| 66.81       |
| BanFakeNews          | BanglaBERT                     | 96.65    | 92.99    | 96.51       |
|                      | BanglaBERT-Large               | **97.51**| **94.69**| **97.43**   |
|                      | BanglaBERT (Sagor Sarker)      | 96.15    | 91.76    | 96.03       |
| Emotion Detection    | BanglaBERT                     | **70.78**| 41.26    | **65.52**   |
|                      | BanglaBERT-Large               | 68.07    | **42.87**| 65.08       |
|                      | BanglaBERT (Sagor Sarker)      | 63.86    | 40.10    | 61.09       |

#### Multilingual Language Models (MLMs)

| Dataset              | Model          | Accuracy | Macro F1 | Weighted F1 |
|----------------------|----------------|----------|----------|-------------|
| SentNoB              | XLM-Roberta    | **70.37**| **67.94**| **70.67**   |
|                      | M-BERT         | 67.97    | 65.21    | 68.13       |
|                      | M-deBerta      | 60.72    | 55.23    | 58.91       |
|                      | M-deBerta-V3   | 67.28    | 63.80    | 66.75       |
| Sarcasm Detection    | XLM-Roberta    | **93.60**| **93.30**| **93.30**   |
|                      | M-BERT         | 88.68    | 87.92    | 88.52       |
|                      | M-deBerta      | 90.22    | 89.90    | 90.25       |
|                      | M-deBerta-V3   | 90.63    | 90.01    | 90.50       |
| Hate Speech Detection| XLM-Roberta    | **69.44**| **62.19**| **67.95**   |
|                      | M-BERT         | 66.22    | 60.65    | 66.09       |
|                      | M-deBerta      | 55.22    | 40.95    | 53.05       |
|                      | M-deBerta-V3   | 60.00    | 41.54    | 58.21       |
| BanFakeNews          | XLM-Roberta    | **97.65**| **94.96**| **97.57**   |
|                      | M-BERT         | 89.27    | 88.81    | 89.26       |
|                      | M-deBerta      | 91.95    | 81.74    | 91.43       |
|                      | M-deBerta-V3   | 92.98    | 86.43    | 93.12       |
| Emotion Detection    | XLM-Roberta    | **67.77**| **41.39**| **63.71**   |
|                      | M-BERT         | 59.64    | 34.04    | 55.53       |
|                      | M-deBerta      | 51.20    | 24.48    | 44.03       |
|                      | M-deBerta-V3   | 56.63    | 29.83    | 51.74       |

#### Tiny Large Language Models (TinyLLMs)

| Dataset              | Model        | Accuracy | Macro F1 | Weighted F1 |
|----------------------|--------------|----------|----------|-------------|
| SentNoB              | Gemma-2B     | **66.90**| **63.02**| **66.06**   |
|                      | TinyLlama    | 66.02    | 58.93    | 63.38       |
|                      | Falcon-1.3B  | 58.83    | 46.82    | 52.89       |
|                      | Opt-1.3B     | 63.18    | 58.13    | 61.70       |
| Sarcasm Detection    | Gemma-2B     | **96.86**| **96.72**| **96.85**   |
|                      | TinyLlama    | 94.13    | 93.87    | 94.12       |
|                      | Falcon-1.3B  | 80.26    | 77.64    | 79.14       |
|                      | Opt-1.3B     | 92.41    | 92.14    | 92.43       |
| Hate Speech Detection| Gemma-2B     | **70.89**| **63.08**| **70.30**   |
|                      | TinyLlama    | 67.78    | 54.60    | 66.13       |
|                      | Falcon-1.3B  | 53.56    | 35.43    | 50.51       |
|                      | Opt-1.3B     | 56.44    | 32.21    | 51.78       |
| BanFakeNews          | Gemma-2B     | **97.83**| 95.50    | 97.80       |
|                      | TinyLlama    | **97.83**| **95.54**| **97.81**   |
|                      | Falcon-1.3B  | 95.26    | 90.98    | 95.39       |
|                      | Opt-1.3B     | 92.55    | 84.01    | 92.31       |
| Emotion Detection    | Gemma-2B     | **62.65**| **36.92**| **58.62**   |
|                      | TinyLlama    | 57.83    | 32.50    | 53.25       |
|                      | Falcon-1.3B  | 49.10    | 17.45    | 36.22       |
|                      | Opt-1.3B     | 48.49    | 15.63    | 34.43       |

#### ChatGPT Zero-Shot Prompting

| Dataset              | Precision | Recall | Macro F1 |
|----------------------|-----------|--------|----------|
| SentNoB              | 56.28     | 49.97  | 44.85    |
| Sarcasm Detection    | 62.17     | 57.59  | 48.65    |
| Hate Speech Detection| 54.65     | 50.42  | 46.22    |
| BanFakeNews          | 46.35     | 48.92  | 46.67    |
| Emotion Detection    | 39.58     | 37.86  | 33.09    |

### Acknowledgements

We are thankful to Independent University, Bangladesh, for their support of this project. We would also like to express our gratitude to the Center for Computational & Data Sciences (CCDS Lab) for providing computational facilities and supervising this project.

### Citation

If you use this code, please cite our paper:

-->

```bibtex
@inproceedings{dehan-etal-2023-investigating,
    title = "Investigating the Effectiveness of Graph-based Algorithm for {B}angla Text Classification",
    author = "Dehan, Farhan  and
      Fahim, Md  and
      Ali, Amin Ahsan  and
      Amin, M Ashraful  and
      Rahman, Akmmahbubur",
    editor = "Alam, Firoj  and
      Kar, Sudipta  and
      Chowdhury, Shammur Absar  and
      Sadeque, Farig  and
      Amin, Ruhul",
    booktitle = "Proceedings of the First Workshop on Bangla Language Processing (BLP-2023)",
    month = dec,
    year = "2023",
    address = "Singapore",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.banglalp-1.12",
    doi = "10.18653/v1/2023.banglalp-1.12",
    pages = "104--116",
    abstract = "In this study, we examine and analyze the behavior of several graph-based models for Bangla text classification tasks. Graph-based algorithms create heterogeneous graphs from text data. Each node represents either a word or a document, and each edge indicates relationship between any two words or word and document. We applied the BERT model and different graph-based models including TextGCN, GAT, BertGAT, and BertGCN on five different datasets including SentNoB, Sarcasm detection, BanFakeNews, Hate speech detection, and Emotion detection datasets for Bangla text. BERT{'}s model bested the TextGCN and the GAT models by a large difference in terms of accuracy, Macro F1 score, and weighted F1 score. BertGCN and BertGAT are shown to outperform standalone graph models and BERT model. BertGAT excelled in the Emotion detection dataset and achieved a 1{\%}-2{\%} performance boost in Sarcasm detection, Hate speech detection, and BanFakeNews datasets from BERT{'}s performance. Whereas, BertGCN outperformed BertGAT by 1{\%} for SetNoB, and BanFakeNews datasets while beating BertGAT by 2{\%} for Sarcasm detection, Hate Speech, and Emotion detection datasets. We also examined different variations in graph structure and analyzed their effects.",
}
```

