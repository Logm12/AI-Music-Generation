# Project Report: A Deep Learning Approach to Emotion-Driven Music Generation from Vietnamese Text

**Course:** Artificial Intelligence (INS3080)  
**Instructor:** PhD. Ha Manh Hung  
**Group:** 10  
**Date:** June 23rd, 2025

---

## 1. Executive Summary

This project presents an end-to-end Artificial Intelligence system designed to translate the emotional content of Vietnamese text into instrumental music. Addressing the challenge of processing the rich context of the Vietnamese language, the team constructed a labeled dataset of over 37,000 social media comments and fine-tuned a **PhoBERT** model to achieve **90% accuracy** in emotion classification. The system utilizes a generative deep learning model conditioned on Valence-Arousal vectors to compose music. The result is a deployed web application that successfully bridges linguistic analysis and creative musical expression.

## 2. Introduction

### 2.1 Problem Statement

Music is a universal language for emotion, yet automated generation of music based on specific textual sentiments remains challenging, particularly for low-resource languages like Vietnamese. Existing systems often lack the ability to:
1.  Accurately interpret complex Vietnamese linguistic nuances (slang, teencode, diacritics).
2.  Generate diverse, structurally coherent music that aligns with specific emotional inputs.

### 2.2 Objectives

- Build a modular framework: Text → Emotion Vector → Music.
- Construct a high-quality Vietnamese emotion dataset (Ekman’s 6 emotions).
- Develop an NLP model with >90% accuracy.
- Implement a conditional music generation model (LSTM/Transformer).

## 3. Methodology

### 3.1 System Architecture

The pipeline consists of four main modules:
1.  **Text Preprocessing:** Cleaning raw text, normalizing "teencode" (teen slang), and tokenization.
2.  **Emotion Extraction:** Using Deep Learning (PhoBERT, Bi-LSTM) to classify text into: *Happiness, Sadness, Anger, Fear, Disgust, Surprise*.
3.  **Vector Mapping:** Converting discrete emotion labels into continuous **Valence-Arousal** vectors (based on Russell's Circumplex Model) to serve as conditions for the music generator.
4.  **Music Generation:** A neural network generates MIDI sequences based on the input vector.

### 3.2 Data Collection & Preparation

- **Text Data:** Scraped ~37,000 comments from YouTube videos using Selenium. Data was manually labeled into 6 emotion categories.
    - *Preprocessing:* Removal of HTML tags, URLs; normalization of 30+ common teencode variations (e.g., "ko" -> "không"); removal of non-diacritic text.
- **Music Data:**
    - **MAESTRO Dataset:** Used for pre-training the model on musical grammar.
    - **VGMIDI Dataset:** 200 labeled video game soundtracks used for fine-tuning with Valence-Arousal tags.

### 3.3 Model Architectures

#### Emotion Recognition: PhoBERT
We selected **PhoBERT** (VinAI) due to its state-of-the-art performance on Vietnamese NLP tasks.
- **Architecture:** Transformer-based, 12 layers, 12 attention heads, 768 hidden units.
- **Fine-tuning:** Added a classification head (Dropout + Linear Layer). Trained with CrossEntropyLoss and AdamW optimizer.

#### Music Generation
The system employs a Transfer Learning strategy. A model (Transformer/LSTM-based) was pre-trained on classical piano performances to learn structure, then fine-tuned on the emotion-labeled VGMIDI dataset using conditional inputs (Note Sequence + Emotion Vector).

## 4. Experimental Results

### 4.1 Emotion Recognition (PhoBERT)

The PhoBERT model demonstrated superior performance compared to Bi-LSTM and Logistic Regression baselines.

- **Overall Accuracy:** **90%**
- **Macro F1-Score:** **0.89**

**Per-Class Performance:**

| Emotion | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- |
| **Anger** | 90% | 93% | 91% |
| **Happiness** | 91% | 87% | 89% |
| **Sadness** | 89% | 92% | 90% |
| **Fear** | 90% | 90% | 90% |
| **Surprise** | 90% | 88% | 89% |
| **Disgust** | 85% | 86% | 86% |

*Analysis:* The confusion matrix shows high diagonal dominance. The most frequent misclassifications occurred between emotionally similar states (e.g., Happy vs. Fear, Sadness vs. Anger), which is common in sentiment analysis.

### 4.2 Music Generation

- **Training:** The model showed a consistent decrease in loss during the fine-tuning phase (down to ~0.011), indicating effective learning of the conditional probability distribution.
- **Qualitative Assessment:**
    - *Low Temperature (0.8):* Coherent but repetitive music.
    - *High Temperature (1.4):* Chaotic, atonal.
    - *Optimal Temperature (1.0-1.2):* Balanced creativity and structure.
- **Limitation:** While structurally correct, the emotional distinctiveness of the generated music is sometimes subtle, likely due to the small size of the VGMIDI fine-tuning dataset.

## 5. Deployment

A web application was built using **Flask** to demonstrate the capability.
- **Workflow:** User inputs text -> Backend processes emotion -> Generates MIDI -> Converts to Audio (FluidSynth) -> Plays in browser.
- **UI:** Displays the detected emotion, confidence score, and an audio player.

## 6. Conclusion & Future Work

The project successfully established a complete "Text-to-Music" pipeline for Vietnamese. PhoBERT proved highly effective for emotion extraction. Future work will focus on:
1.  Expanding the Vietnamese emotion-music dataset to improve musical expressiveness.
2.  Implementing advanced generative architectures (e.g., Transformer-GANs) to handle longer and more complex compositions.
3.  Containerizing the application (Docker) for easier deployment.

## 7. References

1.  Nguyen, D. Q. & Nguyen, A. T. (2020). *PhoBERT: Pre-trained language models for Vietnamese*.
2.  Dong, H.-W., et al. (2018). *MuseGAN: Multi-track sequential generative adversarial networks*.
3.  Huang, C.-Z. A., et al. (2018). *Music Transformer*.
4.  Ekman, P. (1992). *An argument for basic emotions*.
