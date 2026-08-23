# Chapter 3: Time-Frequency Analysis & Speech System Modeling

---

## Chapter Overview
A continuous speech signal can be analyzed across multiple domains to reveal different physical and mathematical characteristics. While time-domain representation captures acoustic amplitude variations over time, frequency-domain analysis identifies constituent pitch, harmonics, and formant energies. Combining both approaches yields the **spectrogram**, a time-frequency representation essential for tracking formant trajectories and phoneme transitions. Furthermore, speech production systems and vocal tract filtering operations are mathematically modeled using **Discrete-Time Linear Time-Invariant (LTI) systems**, analyzed via **impulse decomposition**, **time-domain convolution**, and **pole-zero system modeling**.

---

## Learning Outcomes
After completing this chapter, students will be able to:
- Interpret speech signals across time-domain, frequency-domain, and spectrogram time-frequency representations.
- Explain spectral energy distribution across fundamental pitch frequencies, formants, and consonant fricatives.
- Formulate discrete-time LTI system properties (Linearity, Superposition, Time-Invariance).
- Compute time-domain convolution $y[n] = x[n] * h[n]$ using tabular/graphical flip-and-slide methods.
- Analyze the limitations of time-domain convolution and explain the necessity of Pole-Zero System Modeling.

---

## 1. Time-Domain Representation of Speech Signals

### 1.1 Definition & Graphical Structure
A time-domain representation is the simplest and most direct method of observing a speech signal. It plots instantaneous sound pressure (amplitude variations) against time.

```mermaid
flowchart LR
    A["🗣️ Acoustic Wave (Air Pressure)"] --> B["🎙️ Microphone Sensor"]
    B --> C["📈 Time-Domain Waveform s(t)"]
```

- **X-axis (Time)**: Represents continuous or discrete time in seconds ($\text{s}$) or milliseconds ($\text{ms}$). Indicates speech event occurrences (word onset, vowel duration, pauses, silence, and speech offset).
- **Y-axis (Amplitude)**: Represents instantaneous signal strength. Measured as sound pressure ($\text{Pa}$), electrical voltage ($\text{V}$), or normalized digital amplitude ($[-1, +1]$ or digital integer range).

![Time-Domain Speech Waveform](../../assets/ch03/slide_06_img_02.png)
*Figure 1.1: Time-Domain Waveform of Spoken Utterance "Sunday"*

### 1.2 Waveform Analysis & Interpretation
In a typical time-domain speech recording (e.g., the spoken word *"Sunday"* over $3.5\text{ s}$):
1. **Silence Regions ($0 - 1.1\text{ s}$ & $2.9 - 3.5\text{ s}$)**: Near-zero flat baseline showing background noise without vocal tract excitation.
2. **Main Speech Burst ($1.1 - 1.7\text{ s}$)**: High-amplitude quasi-periodic oscillations corresponding to voiced vowel sound production.
3. **Inter-Syllabic Pause ($1.7 - 2.6\text{ s}$)**: Amplitude returns close to zero between spoken components.
4. **Secondary Speech Segment ($2.6 - 2.9\text{ s}$)**: Lower amplitude waveform representing softer consonant/syllable articulation.

---

## 2. Frequency-Domain Representation of Speech Signals

### 2.1 Spectral Energy Distribution
While time-domain signals show *when* sound events happen, frequency-domain representation reveals *which frequencies are present and how much energy they carry*. By applying the Discrete Fourier Transform (DFT) or Fast Fourier Transform (FFT), the time waveform is decomposed into sinusoidal components:

- **X-axis (Frequency)**: Measured in Hertz ($\text{Hz}$), ranging from $0\text{ Hz}$ up to the Nyquist frequency $F_s/2$.
- **Y-axis (Magnitude)**: Measured in linear amplitude, power, or logarithmic decibels ($\text{dB}$).

![Frequency-Domain Spectrum](../../assets/ch03/slide_10_img_05.png)
*Figure 2.1: Frequency-Domain Magnitude Spectrum (0 to 8000 Hz)*

### 2.2 Frequency Band Breakdown in Speech
For a speech signal sampled at $F_s = 16\text{ kHz}$ (Nyquist limit $F_{Nyq} = 8\text{ kHz}$):

| Frequency Range | Acoustic Component | Speech Significance |
| :--- | :--- | :--- |
| **$0 - 1000\text{ Hz}$** | Fundamental Frequency ($F_0$) & Low Harmonics | Determines speaker pitch and glottal excitation rate. |
| **$1000 - 4000\text{ Hz}$** | Vocal Tract Formants ($F_1, F_2, F_3$) | Primary acoustic cues for identifying vowels and resonant phonemes. |
| **$4000 - 8000\text{ Hz}$** | Fricative Noise & High Consonants | Provides clarity and distinction for sibilants (/s/, /z/, /ʃ/). |

---

## 3. Comparative Summary: Time-Domain vs. Frequency-Domain

| Feature | Time-Domain Representation | Frequency-Domain Representation |
| :--- | :--- | :--- |
| **Primary Plot** | Amplitude vs. Time | Magnitude/Power (dB) vs. Frequency (Hz) |
| **Information** | Signal onset, duration, pauses, pitch periods | Pitch ($F_0$), harmonic structures, formant peaks |
| **Mathematical Basis** | Direct raw waveform $x[n]$ | Discrete Fourier Transform $X(e^{j\omega}) = \text{DFT}\{x[n]\}$ |
| **Key Advantage** | Simple signal capture and segmentation | Reveals vocal tract filter resonances and spectral energy |
| **Primary Applications** | Endpoint detection, silence removal, energy thresholding | Speech/Speaker recognition, pitch estimation, noise filtering |

---

## 4. Spectrogram: Time-Frequency Representation

### 4.1 Concept & Computation via STFT
A **spectrogram** combines time and frequency analysis into a single two-dimensional plot. It displays how the spectral content of a signal evolves over time.

$$\text{STFT}\{x[n]\}(m, \omega) = \sum_{n=-\infty}^{\infty} x[n] w[n-m] e^{-j\omega n}$$

- **X-axis**: Time ($\text{seconds}$).
- **Y-axis**: Frequency ($\text{Hz}$ or $\text{kHz}$).
- **Color Intensity / Dark Scale**: Logarithmic magnitude (dB). Darker/warmer regions indicate high energy concentrations.

![Speech Spectrogram](../../assets/ch03/slide_16_img_06.png)
*Figure 4.1: Time-Frequency Spectrogram of Spoken Utterance "Sunday"*

### 4.2 Diagnostic Value of Spectrograms
- **Formant Tracking**: Prominent horizontal dark bands mark formant trajectories ($F_1, F_2, F_3$) moving as articulators change shape.
- **Voiced vs. Unvoiced Distinction**: Voiced speech exhibits clear vertical striations (glottal pulses) and horizontal formant bands; unvoiced speech displays a diffuse high-frequency noise pattern.
- **Phonetic Segmentation**: Visualizes precise boundary transitions between phonemes and syllables.

---

## 5. Discrete-Time & Linear Time-Invariant (LTI) Systems

### 5.1 System Representation
In speech processing, the human vocal tract filter, acoustic microphones, and transmission channels are modeled as **Discrete-Time Systems**:

```mermaid
flowchart LR
    X["Input Signal x[n]"] --> S["System Operator T{•}"] --> Y["Output Signal y[n]"]
```

$$y[n] = T\{x[n]\}$$

### 5.2 LTI System Properties

#### 1. Linearity (Principle of Superposition)
A system is linear if it satisfies both **Scalability (Homogeneity)** and **Additivity**:
- **Scalability**: $T\{a \cdot x[n]\} = a \cdot T\{x[n]\} = a \cdot y[n]$
- **Additivity**: $T\{x_1[n] + x_2[n]\} = T\{x_1[n]\} + T\{x_2[n]\} = y_1[n] + y_2[n]$
- **Superposition Equation**:
  $$T\{a \cdot x_1[n] + b \cdot x_2[n]\} = a \cdot y_1[n] + b \cdot y_2[n]$$

#### 2. Time Invariance
A system is time-invariant if a time shift in the input causes an identical time shift in the output:
$$\text{If } x[n] \xrightarrow{T} y[n], \quad \text{then } x[n - k] \xrightarrow{T} y[n - k]$$

---

## 6. Impulse Decomposition & Time-Domain Convolution

### 6.1 Impulse Decomposition
Any discrete-time speech signal $x[n]$ can be uniquely represented as a linear combination of weighted, time-shifted unit impulses $\delta[n-k]$:

$$x[n] = \sum_{k=-\infty}^{\infty} x[k] \, \delta[n - k]$$

where the unit impulse function $\delta[n]$ is defined as:

$$\delta[n] = \begin{cases} 1, & n = 0 \\ 0, & n \neq 0 \end{cases}$$

### 6.2 The Convolution Sum Equation
If an LTI system has an **impulse response** $h[n] = T\{\delta[n]\}$, then the output $y[n]$ for any arbitrary input $x[n]$ is given by the **Time-Domain Convolution Sum**:

$$y[n] = x[n] * h[n] = \sum_{k=-\infty}^{\infty} x[k] \, h[n - k]$$

```mermaid
flowchart TD
    A["Decompose Input x[n] into Weighted Impulses x[k]δ[n-k]"] --> B["Excite System Impulse Response h[n-k]"]
    B --> C["Sum All Scaled & Shifted Responses to Obtain y[n]"]
```

### 6.3 Mathematical Properties of Convolution
1. **Commutative**: $x[n] * h[n] = h[n] * x[n]$
2. **Associative**: $(x[n] * h_1[n]) * h_2[n] = x[n] * (h_1[n] * h_2[n])$
3. **Distributive**: $x[n] * (h_1[n] + h_2[n]) = (x[n] * h_1[n]) + (x[n] * h_2[n])$
4. **Impulse Property**: $x[n] * \delta[n] = x[n]$
5. **Shift Property**: $x[n - k_1] * h[n - k_2] = y[n - k_1 - k_2]$
6. **Output Length Property**: If sequence $x[n]$ has length $L_x$ and $h[n]$ has length $L_h$, the convolved output sequence $y[n]$ has length:
   $$L_y = L_x + L_h - 1$$

---

## 7. Step-by-Step Tabular Convolution Method

To compute $y[n] = x[n] * h[n]$ manually:
1. **Index Alignment**: Identify non-zero indices for $x[k]$ and $h[k]$.
2. **Time Reversal (Flip)**: Reflect impulse response $h[k]$ about origin to form $h[-k]$.
3. **Shift and Multiply**: For each output index $n$, shift $h[n-k]$ by $n$ steps, multiply overlapping samples with $x[k]$, and sum the products.

### Solved Example:
Let input $x[n] = \{1, 2, 1\}$ for $n = 0, 1, 2$ ($L_x = 3$) and impulse response $h[n] = \{1, -1\}$ for $n = 0, 1$ ($L_h = 2$).  
Output length $L_y = 3 + 2 - 1 = 4$ (indices $n = 0, 1, 2, 3$).

- **$n = 0$**: $y[0] = x[0]h[0] = 1 \times 1 = 1$
- **$n = 1$**: $y[1] = x[0]h[1] + x[1]h[0] = (1 \times -1) + (2 \times 1) = 1$
- **$n = 2$**: $y[2] = x[1]h[1] + x[2]h[0] = (2 \times -1) + (1 \times 1) = -1$
- **$n = 3$**: $y[3] = x[2]h[1] = 1 \times -1 = -1$

**Final Output**: $y[n] = \{1, 1, -1, -1\}$ for $n = 0, 1, 2, 3$.

---

## 8. Limitations of Time-Domain Convolution & Transition to Pole-Zero Modeling

While time-domain convolution fully describes LTI system outputs, it presents significant practical limitations in speech system analysis:

1. **High Computational Complexity**: Direct convolution of long speech signals requires $O(N \cdot M)$ multiplications and additions.
2. **Hidden Spectral Structure**: Time-domain coefficients do not explicitly disclose resonant frequencies (formants), bandwidths, or attenuation.
3. **Obscured System Stability & Resonances**: System poles (vocal tract resonances) and zeros (nasal tract antiresonances) cannot be directly identified from time-domain sample sequences.

---

## 9. Pole-Zero System Modeling of Speech Systems

### 9.1 Physical Speech Production & Vocal Tract System Representation
In digital speech processing, the human speech production mechanism is modeled as an acoustic source exciting a linear system (vocal tract filter):

```mermaid
flowchart LR
    A["🫁 Lungs & Vocal Cords (Excitation Source X(z))"] --> B["🗣️ Vocal Tract Filter H(z)"] --> C["🔊 Output Speech Signal Y(z)"]
```

$$Y(z) = X(z) \cdot H(z) \implies H(z) = \frac{Y(z)}{X(z)}$$

Rather than modeling every physical articulator movement (tongue, lips, jaw, velum), Digital Signal Processing (DSP) parametrizes the vocal tract as a rational transfer function $H(z)$ composed of **poles** and **zeros**.

### 9.2 Mathematical Transfer Function, Poles, and Zeros
The general discrete-time rational system transfer function is expressed as:

$$H(z) = \frac{B(z)}{A(z)} = G \frac{\sum_{k=0}^{M} b_k z^{-k}}{1 - \sum_{k=1}^{N} a_k z^{-k}} = G \frac{z^{N-M} \prod_{k=1}^{M} (z - z_k)}{\prod_{k=1}^{N} (z - p_k)}$$

- **Poles ($A(z) = 0$)**: The complex values of $z$ for which denominator $A(z) = 0$, causing transfer function magnitude $|H(z)| \to \infty$.
  - *Acoustic Role*: Poles amplify specific frequencies, forming resonant peaks in the speech spectrum known as **vocal tract formants** ($F_1, F_2, F_3$).
  - *Vowel Example*: Spoken vowel `/a/` has prominent formants around $700\text{ Hz}$, $1200\text{ Hz}$, and $2500\text{ Hz}$, modeled by complex-conjugate pole pairs near the unit circle in the $z$-plane.
- **Zeros ($B(z) = 0$)**: The complex values of $z$ for which numerator $B(z) = 0$, causing transfer function magnitude $|H(z)| = 0$.
  - *Acoustic Role*: Zeros attenuate or completely suppress specific frequency components, creating spectral dips or anti-resonances.
  - *Nasal Example*: Nasal consonants (/m/, /n/, /ŋ/) introduce zeros into the vocal tract transfer function due to acoustic coupling with the nasal cavity.

### 9.3 Pole-Zero Plot & Stability Analysis ($s$-Plane vs. $z$-Plane)
A pole-zero plot displays the spatial locations of system poles (marked with an **X**) and zeros (marked with an **O**) in the complex frequency plane.

![Pole-Zero Diagrams](../../assets/ch03/slide_48_img_12.png)
*Figure 9.1: Pole-Zero Plots in $s$-plane (Continuous-Time Laplace Transform) and $z$-plane (Discrete-Time Z-Transform)*

- **Continuous-Time Systems ($s$-plane)**: Evaluated using the Laplace transform. System stability requires all poles to lie in the **Left Half-Plane** ($\text{Re}(s) < 0$).
- **Discrete-Time Systems ($z$-plane)**: Evaluated using the Z-transform. An LTI discrete-time system is **BIBO Stable** if and only if **all poles lie strictly inside the unit circle**:
  $$|p_k| < 1 \quad \forall k = 1, 2, \dots, N$$

### 9.4 Solved Examples from Lecture Slides

#### Example 1: Second-Order System Analysis
Find the poles and zeros of the discrete-time transfer function:
$$H(z) = \frac{z - 0.5}{z^2 - 0.8z + 0.25}$$

- **Zeros Calculation**: Set numerator to zero:
  $$z - 0.5 = 0 \implies \mathbf{z = 0.5}$$
  *(One real zero at $z = 0.5$, completely suppressing response at this point).*
- **Poles Calculation**: Set denominator to zero ($z^2 - 0.8z + 0.25 = 0$):
  $$z = \frac{0.8 \pm \sqrt{(-0.8)^2 - 4(1)(0.25)}}{2} = \frac{0.8 \pm \sqrt{0.64 - 1.0}}{2} = \frac{0.8 \pm j0.6}{2} = \mathbf{0.4 \pm j0.3}$$
- **Stability Verification**:
  $$|p| = \sqrt{0.4^2 + 0.3^2} = \sqrt{0.16 + 0.09} = \sqrt{0.25} = 0.5 < 1$$
  Since $|p| = 0.5 < 1$, both poles lie inside the unit circle; the system is **BIBO Stable**.

#### Example 2: Higher-Order System Analysis
Determine the poles and zeros of:
$$H(z) = \frac{z^2(z - 0.9)}{(z - (0.5 - j0.7))(z - (0.5 + j0.7))(z - 0.8)}$$

- **Zeros Calculation**:
  - $z^2 = 0 \implies \mathbf{z = 0, 0}$ *(Double/repeated zeros at the origin)*.
  - $z - 0.9 = 0 \implies \mathbf{z = 0.9}$ *(Real zero at $z = 0.9$)*.
- **Poles Calculation**:
  - $z - (0.5 - j0.7) = 0 \implies \mathbf{p_1 = 0.5 - j0.7}$
  - $z - (0.5 + j0.7) = 0 \implies \mathbf{p_2 = 0.5 + j0.7}$
  - $z - 0.8 = 0 \implies \mathbf{p_3 = 0.8}$
- **Stability Verification**:
  - $|p_{1,2}| = \sqrt{0.5^2 + 0.7^2} = \sqrt{0.25 + 0.49} = \sqrt{0.74} \approx 0.8602 < 1$.
  - $|p_3| = 0.8 < 1$.  
  All poles lie inside the unit circle; the system is **BIBO Stable**.

### 9.5 Significance of Pole-Zero Placement in Digital Filter Design
1. **Resonance Peak Shaping**: The closer a pole $p_k$ is to the unit circle ($|p_k| \to 1$), the sharper and narrower the corresponding spectral formant resonance peak.
2. **Frequency Notch Filtering**: Placing a zero directly on the unit circle ($|z_k| = 1$) creates an exact notch filter that completely eliminates an unwanted frequency.
3. **Filter Design Backbone**: Pole-zero placement forms the foundation for designing Infinite Impulse Response (IIR) digital filters, Linear Predictive Coding (LPC) speech synthesizers, and acoustic noise cancellers.

