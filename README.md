# Emotion-Driven Music Generation from Vietnamese Text

**Final Project - Artificial Intelligence (INS3080)**  
**Group 10 - Vietnam National University, Hanoi - International School**

## Overview

This project develops an end-to-end deep learning system capable of generating emotionally aligned music based on Vietnamese text input. By bridging Natural Language Processing (NLP) and symbolic music generation, the system creates a personalized auditory experience that reflects the emotional nuance of the user's language.

The core pipeline consists of:
1.  **Emotion Recognition:** Analyzing Vietnamese text to detect emotions (Happiness, Sadness, Anger, Fear, Disgust, Surprise) using a fine-tuned **PhoBERT** model.
2.  **Emotion-to-Music Mapping:** Mapping detected emotions to a Valence-Arousal vector space based on Russell's Circumplex Model.
3.  **Music Generation:** Generating symbolic music (MIDI) conditioned on the emotion vector using a Deep Learning model (LSTM/Transformer-based).

## Key Features

- **Vietnamese Sentiment Analysis:** Specialized text preprocessing handles teencode and stop words, achieving emotion classification with **90% accuracy**.
- **Emotion-Conditioned Music:** Generates unique MIDI tracks corresponding to the input text's mood.
- **Web Interface:** A user-friendly Flask-based web application for real-time interaction.
- **Large-Scale Dataset:** Utilizes a custom dataset of ~37,000 labeled Vietnamese YouTube comments and the VGMIDI dataset for music fine-tuning.

## Tech Stack

- **Language:** Python 3.11+
- **Deep Learning Frameworks:** PyTorch, TensorFlow/Keras, Hugging Face Transformers
- **Web Backend:** Flask
- **Data Collection:** Selenium (Web Scraping)
- **Audio Processing:** Music21, FluidSynth, FFmpeg
- **Environment:** Kaggle Kernels (Tesla T4/P100 GPU), Local Windows Server

## Project Structure

```
├── data/
│   ├── raw_comments/       # Scraped YouTube comments
│   ├── processed/          # Cleaned dataset with 6 emotion labels
│   └── music_midi/         # MAESTRO and VGMIDI datasets
├── models/
│   ├── emotion_recognition/# PhoBERT & Bi-LSTM training scripts
│   └── music_generation/   # LSTM/Transformer training & fine-tuning
├── web_app/
│   ├── static/             # CSS, JS, Audio files
│   ├── templates/          # HTML templates
│   └── app.py              # Flask server entry point
├── preprocessing/
│   ├── teencode_map.py     # Slang normalization dictionary
│   └── text_cleaner.py     # NLP pipeline
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.8+
- FluidSynth (for MIDI to Audio conversion)
- SoundFont file (e.g., `FluidR3_GM.sf2`)

### Installation

1.  Clone the repository:
    ```bash
    git clone https://github.com/your-repo/emotion-music-gen-vn.git
    cd emotion-music-gen-vn
    ```

2.  Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3.  Download Pre-trained Models:
    - Place the fine-tuned PhoBERT weights in `models/emotion_recognition/`.
    - Place the `music_transformer_finetuned.pth` in `models/music_generation/`.

### Running the Web App

1.  Start the Flask server:
    ```bash
    python web_app/app.py
    ```
2.  Access the interface at `http://localhost:5000`.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

```text
MIT License

Copyright (c) 2024 Group 10 - VNU-IS

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
