# Tamil-to-Telugu-Speech-to-Speech-Translation-Model
This project develops a Speech-to-Speech Translation system to convert Tamil speech to Telugu. It integrates ASR, MT, and TTS technologies, using Whisper for ASR, AI4Bharat’s IndicTrans for translation, and Facebook MMS for TTS. The project improves multilingual communication, with future work aiming to reduce latency and enhance accuracy.

---

## Introduction

Tamil and Telugu are prominent Dravidian languages spoken primarily in the southern part of India. Despite their rich literary traditions, there are limited resources available for developing advanced language technologies for these languages. With the increasing need for multilingual communication in India, there is a significant demand for effective translation systems that cater to regional languages.

Speech-to-Speech Translation (S2ST) is an interdisciplinary field combining:
1. **Automatic Speech Recognition (ASR)**: Converts spoken Tamil into written text.
2. **Machine Translation (MT)**: Translates the text from Tamil to Telugu.
3. **Text-to-Speech (TTS)**: Synthesizes the translated text into spoken Telugu.

---

## Reference Studies and Key Findings

### Multilingual Automatic Speech Recognition (ASR) using Common Voice Corpus (Ardila et al., 2019)
- Emphasized community participation in building robust speech corpora and demonstrated the performance of ASR systems across different languages.

### Speech-to-Speech Machine Translation (Mujadia and Sharma, 2023)
- Developed a system utilizing ASR, MT, Subtitling (SRT), and TTS for accurate video translation across languages.

### Text Processing for TTS in Indian Languages (Raj et al., 2007)
- Addressed challenges in Font-to-Akshara mapping, pronunciation rules, and text normalization to ensure natural speech synthesis.

---

## Dataset: Common Voice 11

- **Audio Recordings**: This dataset consists of Tamil audio clips contributed by volunteers. The clips contain sentences read aloud by various speakers.
- **Transcriptions**: Each audio recording has a corresponding text transcription.
- **Metadata**: Speaker demographics, recording quality, and clip duration are included.

| Data Split | Rows  |
|------------|-------|
| Train      | 2000  |
| Validation | 400   |
| Test       | 200   |

---

## Methodology

### Models Used
1. **ASR**: `vasista22/whisper-tamil-medium`
2. **Text-to-Text**: `ai4bharat/indictrans2-indic-indic-dist-320M`
3. **TTS**: `facebook/mms-tts-kff-script_telugu`

### ASR Model Preprocessing
- Unnecessary metadata columns were removed.
- Audio was uniformly sampled at 16,000 Hz.
- **WhisperFeatureExtractor** and **WhisperTokenizer** were initialized using a pre-trained model specific to Tamil.

### Training Parameters
The models were trained and evaluated using the **Common Voice 11** dataset. Word Error Rate (WER) results for different models are as follows:

| Model                           | WER   |
|----------------------------------|-------|
| Vignesh-M/Whisper-tamil-medium   | 38.60 |
| vasista22/whisper-tamil-medium   | 41.81 |
| AI4Bharat/Indic-Whisper          | 44.54 |
| FaceBook/Wav2Vec                 | 71.58 |

---

## Results

### Text-to-Text Model

The Indic-trans model architecture (Gala, Jay, et al., 2023) was used to evaluate translation performance using BLEU, Cosine Similarity, and Rouge-L scores:

| Evaluation Metric | Score   |
|-------------------|---------|
| BLEU              | 0.57    |
| Cosine Similarity | 0.69597 |
| Rogue L Score     | 0.55453 |

### Text-to-Speech (TTS) Model

Massively Multilingual Speech (MMS) models were used for TTS, employing adversarial learning and variational inference techniques. The final synthesis results were evaluated with the Mean Opinion Score (MOS):

| Model                      | MOS   |
|-----------------------------|-------|
| Ground Truth                | 4.46  |
| Tacotron 2                  | 4.25  |
| VITS-based MMS              | 4.43  |

---

## Conclusion

Our project has delivered a robust speech processing system encompassing ASR, translation, and synthesis. We've achieved accurate transcription, seamless translation, and natural-sounding speech synthesis. Through meticulous data preprocessing and model training, this tool has improved multilingual communication and accessibility.

---

## Future Work and Enhancements

1. **Direct Speech-to-Speech Translation**: We aim to reduce inefficiencies by implementing direct speech-to-speech translation models like Google's Translatotron 3.
2. **Reduced Latency**: Eliminating intermediate text processing will help improve translation speed and accuracy.
3. **Enhanced Naturalness**: Retaining the prosody and intonation of original speech will further improve natural-sounding translations.

---

## References

- Kim, Jaehyeon, Jungil Kong, and Juhee Son. *"Conditional Variational Autoencoder with Adversarial Learning for End-to-End Text-to-Speech"*. International Conference on Machine Learning, 2021.
- Bhogale, Kaushal Santosh, et al. *"Vistaar: Diverse Benchmarks and Training Sets for Indian Language ASR"*. arXiv preprint arXiv:2305.15386, 2023.
- Chowdary, Divi Eswar, et al. *"Transformer‐Based Multilingual Automatic Speech Recognition (ASR) Model for Dravidian Languages"*. Automatic Speech Recognition and Translation for Low Resource Languages, 2024.

For additional results, check the [translated audio samples](https://drive.google.com/drive/folders/1NeuGFZlLyw8jjl9_fxtDLWFKZ9sBscST?usp=sharing).
