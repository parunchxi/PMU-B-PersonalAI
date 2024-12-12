# Learning from Biosignal

**Biosignals** are vital for medical diagnostics, with examples like EEG for brain activity and ECG for heart activity. These signals, typically interpreted by doctors, face delays when patient loads are high. AI and ML now enable remote analysis, improving efficiency.\
**TinySleepNet**, part of the **Learning from Biosignals** project, uses deep learning to analyze sleep stages via EEG signals. It addresses sleep issues like insomnia and sleep apnea, offering faster, more accurate diagnostics.

## Biosignal Analysis

### 1. Preprocessing

- Remove noise or artifacts from signals to clean the data, ensuring it is suitable for model training.

### 2. Feature Extraction

- Derive meaningful features specific to the problem from the preprocessed signals.
  This process is often hand-engineered by domain-specific experts familiar with features relevant to particular issues.

### 3. Model Construction

- Employ machine learning algorithms to train models.
  Understand the relationships between input features and their desired output, such as labels or annotations.

### Application Specific

Preprocessing and feature extraction depend on the type of biosignal and the targeted condition. For example, brain signals vary during activities like thinking or sleeping. Developing models that can detect patterns across all biosignals remains a challenge, as no universal solution exists.

### Deep Learning

Utilizes multiple layers of non-linear transformation to convert raw biosignal inputs into meaningful representations for tasks like classification, reducing the need for manual preprocessing and feature extraction.

## Sleep Stage Scoring

### Sleep Stages

- Non-REM Sleep
  - N1: Sleep onset
  - N2: Light sleep (K-complex, sleep spindles)
  - N3: Deep sleep (most restorative)
- REM Sleep: Dream stage, essential for memory and creativity.
- Awake (W): Periods of wakefulness.

**Sleep Cycle:** Repeated cycles of Non-REM and REM sleep, with longer REM periods toward morning.

### Sleep Quality Metrics

- **Total Sleep Time (TST)** = Total time in N1 + N2 + N3 + REM.
- **Time in Bed (TIB)** = Time from lights off to lights on.
- **Sleep Efficiency (%)** = (TST / TIB) × 100% — Higher is better.

### Problem

- **Manual Scoring**: Labor-intensive, requires human review.
- **Signal Complexity**: Requires multiple signals (EEG, EOG, EMG, ECG).
- **Non-portability**: Bulky equipment, hard to use at home.

### Solution

- **Single-Channel EEG**: Use only EEG to simplify data collection.
- **Deep Learning Model**: Automatic sleep stage classification (W, N1, N2, N3, REM).
- **Portable Device**: In-ear EEGs or headbands for home use.

### Sleep Dataset

- **Dataset**: SleepEDF (v1)
- **Subjects**: 20 healthy participants (Age: 28.7 ± 2.9)
- **Signals**: 2 EEG, 1 EOG, 1 EMG, respiration
- **Data**:
  - **Signal files**: \*.PSG.edf (raw signals)
  - **Hypnogram files**: \*.Hypnogram.edf (sleep stage labels)

## Model

### DeepSleepNet

- **Purpose**: Sleep stage scoring using single-channel EEG.
- **Components**:
  - **Representation Learning**: Dual-branch 1D CNNs (**CNN-Small** for high-frequency, **CNN-Large** for low-frequency features).
  - **Sequence Learning**: **Bi-directional RNN** with shortcut connections to learn stage transition rules.
- **How it Works**:
  1. Input: 30-second EEG.
  2. Extract features via CNN-Small & CNN-Large, then combine.
  3. RNN predicts sleep stage (W, N1, N2, N3, REM).
- **Training**:
  - **Loss**: Cross-entropy.
  - **Optimizer**: Adam.
  - **Stage Transition Rules**: Based on **AASM Manual** — e.g., if N2, continue N2 even without K-complex or sleep spindle.

### TinySleepNet

- **Purpose**: Lightweight sleep scoring for portable devices.
- **Improvements**:
  - **Single-branch CNN** (reduced complexity).
  - **Uni-directional RNN** (less computational overhead).
  - No pre-training required.
- **How it Works**:
  1. Input: 30-second EEG.
  2. Extract features via single-branch CNN.
  3. Use RNN to predict sleep stage (W, N1, N2, N3, REM).
- **Training Enhancements**:
  - **Data Augmentation**:
    - **Signal Augmentation**: Random shift of EEG signals (0-3s).
    - **Sequence Augmentation**: Randomly skip initial epochs.
  - **Loss**: Weighted cross-entropy to prioritize rare stages (e.g., N1).

## Differences Between DeepSleepNet and TinySleepNet

| **Feature**           | **DeepSleepNet**                  | **TinySleepNet**               |
| --------------------- | --------------------------------- | ------------------------------ |
| **CNN Architecture**  | 2 branches (CNN-Small, CNN-Large) | 1 single-branch CNN            |
| **RNN Type**          | Bi-directional RNN                | Uni-directional RNN            |
| **Pre-training**      | Class-balanced oversampling       | No pre-training required       |
| **Data Augmentation** | None                              | Signal & sequence augmentation |
| **Portability**       | Less portable                     | Portable and lightweight       |

## Evaluation

### Experimental Setup

- **k-fold Cross-Validation**: Non-overlapping patient split (patients appear only in training, validation, or test set, not in multiple).

### Performance Metrics

- **Overall Metrics**:

  - **Accuracy (ACC)**: Measures overall correctness.
  - **Macro-averaged F1-Score (MF1)**: Averages F1-scores for each class.
  - **Cohen’s Kappa (κ)**: Measures agreement beyond chance.

- **Confusion Matrix**:  
  | **TP** | **FP** |
  |--------|--------|
  | **TN** | **FN** |

  - **TP**: True Positive (Hit)
  - **FP**: False Positive (False Alarm)
  - **TN**: True Negative (Correct Rejection)
  - **FN**: False Negative (Miss)

- **Per-class Metrics**:
  - **Precision (PR)**: \( PR = \frac{TP}{TP + FP} \)
  - **Recall (RE)**: \( RE = \frac{TP}{TP + FN} \)
  - **F1-Score (F1)**: \( F1 = \frac{2 \cdot PR \cdot RE}{PR + RE} \)

### Visualization

- **Hypnogram**: A graph showing sleep stages as a function of time.
- **Confusion Matrix**: Visualizes model performance, showing actual vs. predicted sleep stages.

### Model Evaluation

- **Performance**: TinySleepNet achieves performance comparable to state-of-the-art methods.
- **Key Focus**: Prioritizes N1 classification (most difficult stage) without sacrificing accuracy on other stages.
- **Cross-Validation**: k-fold cross-validation with non-overlapping patient split to avoid patient leakage.

## Conclusion

### Deep Learning Applications

- Effective for supervised biosignal cases but not suitable for all scenarios.
- Alternative: Transform raw signals into spectrograms or image-based representations, allowing the use of CNNs for image processing. However, this approach is not ideal for end-to-end training.
- Few successful cases directly apply deep learning on raw signals, usually limited to domains with clear signal patterns and ample training data.

### Future Directions

- Promising research in remote monitoring using wearable devices.
- Leveraging knowledge learned in clinical settings to adapt models for wearable technologies.

## Future Work

### For Doctors

- Enable monitoring of key metrics such as sleep hours, walking performance, body temperature, and blood pressure.

### For Patients

- Save time and money by reducing hospital visits.
- Early detection of harmful diseases, potentially saving lives.

### Model Development

- Transfer learning techniques to adapt models for smart devices.
- Focus on early-stage disease signs to benefit both patients and doctors.
