# Audio Emotion Recognition

This project implements and compares multiple methods for **speech emotion recognition (SER)** on a combined emotional speech dataset. Both classical machine learning and transformer-based deep learning approaches are evaluated under the same experimental setup.

---

## Dataset

Experiments are conducted on a cross-corpus emotional speech dataset created by merging four commonly used SER datasets:

- RAVDESS  
- CREMA-D  
- TESS  
- SAVEE  

### Emotion Classes
- Angry
- Disgusted
- Fearful
- Happy
- Neutral
- Sad
- Surprised

Combining multiple datasets introduces variability in speakers, recording conditions, and speaking styles.

---

## Methods

### MFCC + SVM
- 40 MFCC features extracted using Librosa
- Mean and standard deviation computed across time (80 features total)
- Features standardized
- SVM with RBF kernel used for classification

**Pros:** Fast, simple, strong baseline  
**Cons:** No temporal modeling, sensitive to dataset variability

---

### Zero-Shot Transformer
- Pretrained Wav2Vec2-based emotion recognition model
- No training or fine-tuning performed
- Used to evaluate cross-dataset generalization

**Observation:** Strong bias toward Neutral emotion and low overall accuracy

---

### Fine-Tuned Wav2Vec2
- Model: `facebook/wav2vec2-base`
- Raw audio input (16 kHz)
- End-to-end fine-tuning with a 7-class classification head
- Trained for 5 epochs

**Pros:** Captures temporal and prosodic cues, highest performance  
**Cons:** Requires GPU and longer training time

---

## Results

| Model | Accuracy | Macro F1 |
|------|---------|----------|
| MFCC + SVM | ~72% | ~0.74 |
| Zero-Shot Transformer | ~15% | ~0.13 |
| Fine-Tuned Wav2Vec2 | ~79% | ~0.80 |
