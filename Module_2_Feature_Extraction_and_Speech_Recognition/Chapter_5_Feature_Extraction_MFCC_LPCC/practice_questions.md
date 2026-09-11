# Chapter 5: Exam Practice Questions & Model Solutions

> **Course**: Speech and Video Processing (CS30033)  
> **Topic**: Feature Extraction Overview, Real Cepstrum, MFCC, and LPCC  
> **Grading Format**: Standard University 5-Mark Questions with Step-by-Step Solutions

---

### Question 1: Explain the need for feature extraction in speech processing. Discuss the limitations of directly processing raw speech samples and explain the characteristics of a good speech feature. (5 Marks)

#### Model Solution:
**1. Need for Feature Extraction (1.5 Marks):**
- Raw speech waveforms contain massive data redundancy ($16,000\text{ samples/sec}$), speaker-specific idiosyncratic variations, and background channel noise.
- Feature extraction extracts low-dimensional, linguistically relevant parametric vectors ($12–39$ features/frame) that retain phonetic information while removing pitch, loudness, and microphone dependencies.

**2. Limitations of Directly Processing Raw Speech (1.5 Marks):**
1. **High Dimensionality**: Massive sample volume leads to computational intractability in pattern matchers.
2. **Phase Variance**: Slight time shifts alter instantaneous sample amplitudes without altering the spoken phoneme.
3. **Temporal Non-Stationarity**: Speech characteristics change continuously across phonemes.

**3. Four Characteristics of a "Good" Speech Feature (2 Marks):**
1. **High Phonetic Discrimination**: Effectively separates distinct phonemes (e.g., vowels `/a/` vs `/i/`).
2. **Robustness**: Invariant to background acoustic noise, room reverberation, and speaker volume.
3. **Low Dimensionality**: Compact representation for efficient real-time classification.
4. **Statistical Decorrelation**: Orthogonal feature dimensions that facilitate diagonal covariance modeling in HMMs/GMMs.

---

### Question 2: Explain the mathematical framework $s[n] = e[n] * h[n]$. Define what the excitation source $e[n]$ and the vocal tract filter $h[n]$ physically represent in the human body. (5 Marks)

#### Model Solution:
**1. Mathematical Framework (2 Marks):**
Speech production is modeled as a linear convolution of glottal excitation and vocal tract filtering:
$$s[n] = e[n] * h[n]$$
In the frequency domain:
$$S(\omega) = E(\omega) \cdot H(\omega)$$

**2. Physical Representation in the Human Body (3 Marks):**
- **Excitation Source $e[n]$ (1.5 Marks)**:
  - *Voiced Speech*: Quasi-periodic glottal air pulses produced by vocal fold vibrations in the larynx at fundamental frequency $F_0$.
  - *Unvoiced Speech*: Aperiodic turbulent noise produced by forcing air through narrow vocal tract constrictions.
- **Vocal Tract Filter $h[n]$ (1.5 Marks)**:
  - The acoustic resonator formed by the pharyngeal, oral, and nasal cavities.
  - Its geometry is dynamically adjusted by articulators (tongue, jaw, velum, lips) to create resonant frequency peaks (**Formants** $F_1, F_2, F_3$) that define vowel identity.

---

### Question 3: Develop the mathematical framework of the Real Cepstrum and Complex Cepstrum. Explain how magnitude and phase information are handled in each method and compare their reversibility and applications. (5 Marks)

#### Model Solution:
**1. Real Cepstrum Formulation (1.5 Marks):**
$$c_r[n] = \mathcal{F}^{-1} \left\{ \ln |X(e^{j\omega})| \right\} = \frac{1}{2\pi} \int_{-\pi}^{\pi} \ln |X(e^{j\omega})| e^{j\omega n} d\omega$$
- Discards phase information completely.
- **Irreversible**: Cannot reconstruct original time-domain waveform.
- **Application**: Pitch tracking, formant extraction, MFCCs.

**2. Complex Cepstrum Formulation (1.5 Marks):**
$$c_c[n] = \mathcal{F}^{-1} \left\{ \ln X(e^{j\omega}) \right\} = \mathcal{F}^{-1} \left\{ \ln |X(e^{j\omega})| + j \arg X(e^{j\omega}) \right\}$$
- Preserves both magnitude and unwrapped continuous phase.
- **Fully Reversible**: Allows complete reconstruction back to the time domain.
- **Application**: Echo cancellation, speech dereverberation, Text-to-Speech (TTS) voice synthesis.

**3. Comparison Table (2 Marks):**

| Parameter | Real Cepstrum | Complex Cepstrum |
| :--- | :--- | :--- |
| **Phase Used** | No ($\text{Phase} = 0$) | Yes (Continuous unwrapped phase) |
| **Invertibility** | Irreversible | Fully Invertible |
| **Primary Domain** | Speech Recognition (ASR) | Audio Restoration & Speech Synthesis |

---

### Question 4: Explain the complete MFCC feature extraction process with a neat sketch. (5 Marks)

#### Model Solution:
**1. Block Diagram (1.5 Marks):**

```mermaid
flowchart LR
    A["Raw Speech s(n)"] --> B["1. Pre-emphasis\n(1 - α z^-1)"]
    B --> C["2. Framing & Windowing\n(Hamming w[n])"]
    C --> D["3. FFT Power Spectrum\n(|X[k]|^2)"]
    D --> E["4. Mel Filterbank\n(20–40 Triangular Filters)"]
    E --> F["5. Logarithm\n(ln S[m])"]
    F --> G["6. DCT-II\n(12–13 Static MFCCs)"]
```

**2. Six Functional Stages (3.5 Marks):**
1. **Pre-emphasis (0.5 Mark)**: High-pass filter $H(z) = 1 - 0.97 z^{-1}$ boosts high frequencies by $+6\text{ dB/octave}$ to offset glottal spectral tilt.
2. **Frame Blocking & Windowing (0.5 Mark)**: Divides speech into $25\text{ ms}$ frames with $10\text{ ms}$ shift; applies Hamming window to eliminate boundary spectral leakage.
3. **FFT (0.5 Mark)**: Converts windowed frames into short-time power spectra $|X[k]|^2$.
4. **Mel Filterbank Integration (1 Mark)**: Passes power spectrum through $M$ overlapping triangular filters spaced on the Mel scale ($m = 2595 \log_{10}(1 + f/700)$).
5. **Logarithmic Energy Compression (0.5 Mark)**: Applies natural logarithm to match human non-linear loudness perception.
6. **Discrete Cosine Transform (DCT) (0.5 Mark)**: Decorrelates filterbank energies into orthogonal, compact static MFCCs ($c_0$ to $c_{12}$).

---

### Question 5: Differentiate between MFCC and LPCC as speech features. (5 Marks)

#### Model Solution:

| Comparison Attribute | MFCC (Mel-Frequency Cepstral Coefficients) | LPCC (Linear Prediction Cepstral Coefficients) | Marks |
| :--- | :--- | :--- | :---: |
| **1. Underlying Biological Model** | **Perceptual Auditory Model**: Models human cochlear frequency resolution (Mel scale). | **Production Acoustic Model**: Models human vocal tract all-pole resonant tube. | **1.25 Marks** |
| **2. Spectral Assumption** | Non-parametric; makes no assumptions about all-pole filtering. | Parametric; assumes purely all-pole vocal tract transfer function. | **1.25 Marks** |
| **3. Sound Class Performance** | Excellent for both voiced vowels and unvoiced/nasal fricatives. | Accurate for vowels; degraded for nasals/fricatives (due to zeros). | **1.25 Marks** |
| **4. Noise Robustness & ASR Usage** | High noise robustness; standard feature in modern ASR engines. | Sensitive to noise; used primarily in clinical voice pathology. | **1.25 Marks** |
