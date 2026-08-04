# Chapter 3: 5-Mark Important Practice Questions & Solved Numerical Problems

---

### Question 1: Differentiate between Time-Domain, Frequency-Domain, and Spectrogram representations of Speech Signals? Discuss the need for Spectrograms in Speech Processing. (5 Marks)

#### Answer:

**1. Comparison of Speech Signal Representations (3 Marks)**

| Parameter | Time-Domain Representation | Frequency-Domain Representation | Spectrogram (Time-Frequency) |
| :--- | :--- | :--- | :--- |
| **Axes** | X: Time ($\text{s}$), Y: Amplitude | X: Frequency ($\text{Hz}$), Y: Magnitude ($\text{dB}$) | X: Time ($\text{s}$), Y: Frequency ($\text{Hz}$) |
| **3rd Dimension** | None | None | Color / Dark Intensity (Magnitude in $\text{dB}$) |
| **Information** | Signal duration, onset, pauses, pitch periods | Pitch ($F_0$), harmonics, formant energy distribution | Formant trajectories over time, phoneme transitions |
| **Transformation** | Direct acoustic wave sampling | Discrete Fourier Transform (DFT / FFT) | Short-Time Fourier Transform (STFT) |

**2. Need for Spectrograms in Speech Processing (2 Marks)**
- **Combines Time and Frequency Details**: Overcomes time-only or frequency-only limitations by showing *which* frequencies occur at *what* specific time instant.
- **Formant Trajectory Tracking**: Displays dark horizontal bands ($F_1, F_2, F_3$) reflecting vocal tract dynamic resonance changes.
- **Voiced vs. Unvoiced Classification**: Distinguishes glottal periodic striations (voiced speech) from broad-spectrum high-frequency noise (unvoiced fricatives).
- **Core Applications**: Essential for automatic speech recognition (ASR), speaker identification, phonetic segmentation, and noise reduction.

---

### Question 2: Define Linear Time-Invariant (LTI) Systems. Explain the properties of Linearity (Superposition Principle) and Time-Invariance with mathematical definitions. (5 Marks)

#### Answer:

**1. Definition of LTI System (1 Mark)**
A Discrete-Time Linear Time-Invariant (LTI) System is a mathematical transformation $y[n] = T\{x[n]\}$ that converts an input sequence $x[n]$ into an output sequence $y[n]$ while simultaneously satisfying **Linearity** and **Time-Invariance**.

**2. Linearity / Superposition Principle (2 Marks)**
A system is linear if it satisfies both **Scalability (Homogeneity)** and **Additivity**:
- **Scalability**: $T\{a \cdot x[n]\} = a \cdot T\{x[n]\}$
- **Additivity**: $T\{x_1[n] + x_2[n]\} = T\{x_1[n]\} + T\{x_2[n]\}$
- **Superposition Equation**: For arbitrary constants $a$ and $b$:
  $$T\{a \cdot x_1[n] + b \cdot x_2[n]\} = a \cdot y_1[n] + b \cdot y_2[n]$$
  *(The response to a linear combination of inputs equals the linear combination of individual responses).*

**3. Time-Invariance Property (2 Marks)**
- **Definition**: A system is time-invariant if delaying the input sequence by $k$ samples results in an identical time delay of $k$ samples in the output sequence.
- **Mathematical Condition**: If $x[n] \xrightarrow{T} y[n]$, then:
  $$x[n - k] \xrightarrow{T} y[n - k]$$
- **Significance**: System characteristics and parameters remain constant over time (system behavior does not depend on when the input is applied).

---

### Question 3: State the Impulse Decomposition Property and derive the Time-Domain Convolution Sum formula. List four essential properties of Convolution. (5 Marks)

#### Answer:

**1. Impulse Decomposition Property (1.5 Marks)**
Any arbitrary discrete-time signal $x[n]$ can be uniquely decomposed into a weighted sum of time-shifted unit impulse functions $\delta[n-k]$:

$$x[n] = \sum_{k=-\infty}^{\infty} x[k] \, \delta[n - k]$$

where the unit impulse function is $\delta[n] = 1$ for $n=0$, and $0$ elsewhere.

**2. Derivation of Convolution Sum (1.5 Marks)**
Applying an LTI system transformation $T\{\cdot\}$ to the decomposed input sequence:

$$y[n] = T\{x[n]\} = T\left\{ \sum_{k=-\infty}^{\infty} x[k] \, \delta[n - k] \right\}$$

By **Linearity**, the operator $T$ commutes with the summation and scaling factor $x[k]$:

$$y[n] = \sum_{k=-\infty}^{\infty} x[k] \, T\{\delta[n - k]\}$$

By **Time-Invariance**, if $T\{\delta[n]\} = h[n]$ (the system impulse response), then $T\{\delta[n-k]\} = h[n-k]$. Substituting yields the **Convolution Sum**:

$$y[n] = x[n] * h[n] = \sum_{k=-\infty}^{\infty} x[k] \, h[n - k]$$

**3. Key Properties of Convolution (2 Marks)**
1. **Commutative**: $x[n] * h[n] = h[n] * x[n]$
2. **Associative**: $(x[n] * h_1[n]) * h_2[n] = x[n] * (h_1[n] * h_2[n])$
3. **Distributive**: $x[n] * (h_1[n] + h_2[n]) = (x[n] * h_1[n]) + (x[n] * h_2[n])$
4. **Finite Output Length**: For input length $L_x$ and impulse response length $L_h$, output length is $L_y = L_x + L_h - 1$.

---

### Question 4: A discrete-time LTI system has input signal $x[n] = \{2, 1, 2, 4, 3\}$ for $n = 0, 1, 2, 3, 4$ and impulse response $h[n] = \{1, -1, 2\}$ for $n = 0, 1, 2$. Calculate the complete output sequence $y[n]$ using convolution. (5 Marks)

#### Solution:

**1. Input Parameters & Output Length (1 Mark)**
- Input $x[n] = \{2, 1, 2, 4, 3\}$, starting at $n = 0$, length $L_x = 5$.
- Impulse response $h[n] = \{1, -1, 2\}$, starting at $n = 0$, length $L_h = 3$.
- Output sequence length $L_y = L_x + L_h - 1 = 5 + 3 - 1 = 7$ (for indices $n = 0, 1, 2, 3, 4, 5, 6$).

**2. Convolution Sum Computations (3 Marks)**
Formula: $y[n] = \sum_{k} x[k] \, h[n - k]$

- **$y[0]$** ($k=0$):
  $$y[0] = x[0]h[0] = 2 \times 1 = \mathbf{2}$$

- **$y[1]$** ($k=0, 1$):
  $$y[1] = x[0]h[1] + x[1]h[0] = (2 \times -1) + (1 \times 1) = -2 + 1 = \mathbf{-1}$$

- **$y[2]$** ($k=0, 1, 2$):
  $$y[2] = x[0]h[2] + x[1]h[1] + x[2]h[0] = (2 \times 2) + (1 \times -1) + (2 \times 1) = 4 - 1 + 2 = \mathbf{5}$$

- **$y[3]$** ($k=1, 2, 3$):
  $$y[3] = x[1]h[2] + x[2]h[1] + x[3]h[0] = (1 \times 2) + (2 \times -1) + (4 \times 1) = 2 - 2 + 4 = \mathbf{4}$$

- **$y[4]$** ($k=2, 3, 4$):
  $$y[4] = x[2]h[2] + x[3]h[1] + x[4]h[0] = (2 \times 2) + (4 \times -1) + (3 \times 1) = 4 - 4 + 3 = \mathbf{3}$$

- **$y[5]$** ($k=3, 4$):
  $$y[5] = x[3]h[2] + x[4]h[1] = (4 \times 2) + (3 \times -1) = 8 - 3 = \mathbf{5}$$

- **$y[6]$** ($k=4$):
  $$y[6] = x[4]h[2] = 3 \times 2 = \mathbf{6}$$

**3. Final Result Summary (1 Mark)**
$$y[n] = \{2, -1, 5, 4, 3, 5, 6\} \quad \text{for } n = 0, 1, 2, 3, 4, 5, 6$$

---

### Question 5: A discrete-time LTI system has input signal $x[n] = \{1, 3, 2, 1\}$ for $n = 0, 1, 2, 3$ and impulse response $h[n] = \{2, -1\}$ for $n = 0, 1$. Compute output $y[n]$ and verify the output sequence length property. (5 Marks)

#### Solution:

**1. Sequence Parameters & Output Length Verification (1.5 Marks)**
- Input $x[n] = \{1, 3, 2, 1\}$, length $L_x = 4$ ($n = 0, 1, 2, 3$).
- Impulse response $h[n] = \{2, -1\}$, length $L_h = 2$ ($n = 0, 1$).
- Theoretical output length: $L_y = L_x + L_h - 1 = 4 + 2 - 1 = \mathbf{5}$ samples ($n = 0, 1, 2, 3, 4$).

**2. Convolution Computations (2.5 Marks)**

- **$y[0]$**:
  $$y[0] = x[0]h[0] = 1 \times 2 = \mathbf{2}$$

- **$y[1]$**:
  $$y[1] = x[0]h[1] + x[1]h[0] = (1 \times -1) + (3 \times 2) = -1 + 6 = \mathbf{5}$$

- **$y[2]$**:
  $$y[2] = x[1]h[1] + x[2]h[0] = (3 \times -1) + (2 \times 2) = -3 + 4 = \mathbf{1}$$

- **$y[3]$**:
  $$y[3] = x[2]h[1] + x[3]h[0] = (2 \times -1) + (1 \times 2) = -2 + 2 = \mathbf{0}$$

- **$y[4]$**:
  $$y[4] = x[3]h[1] = 1 \times -1 = \mathbf{-1}$$

**3. Output Sequence & Verification Statement (1 Mark)**
$$\mathbf{y[n] = \{2, 5, 1, 0, -1\} \quad \text{for } n = 0, 1, 2, 3, 4}$$
*Verification*: Computed output sequence contains exactly 5 non-zero terms, verifying $L_y = L_x + L_h - 1 = 5$.

---

### Question 6: Discuss the limitations of time-domain convolution for speech processing. Explain why Pole-Zero Modeling is required to represent the human vocal tract system. (5 Marks)

#### Answer:

**1. Limitations of Time-Domain Convolution (2.5 Marks)**
- **High Computational Complexity**: Direct convolution of long speech signals requires $O(N \cdot M)$ multiplications and additions per frame, making real-time processing inefficient.
- **Lack of Direct Frequency Insight**: Time-domain convolution samples $x[n] * h[n]$ do not explicitly reveal system frequency response, bandwidths, or spectral tilt.
- **Obscured Formants & Resonances**: Important speech characteristics (vocal tract formants and nasal antiresonances) cannot be directly estimated or isolated from raw time-domain convolution output.

**2. Need for Pole-Zero System Modeling (2.5 Marks)**
- **Mathematical System Representation**: Models the vocal tract as a rational transfer function in the $Z$-domain:
  $$H(z) = \frac{B(z)}{A(z)} = G \frac{1 + \sum_{k=1}^{M} b_k z^{-k}}{1 - \sum_{k=1}^{N} a_k z^{-k}}$$
- **Physical Vocal Tract Mapping**:
  - **Poles ($A(z) = 0$)**: Correspond to vocal tract resonant frequencies (**formants** $F_1, F_2, F_3$), forming peaks in the spectral envelope.
  - **Zeros ($B(z) = 0$)**: Correspond to acoustic anti-resonances (dips), modeling nasal tract coupling (nasal consonants /m/, /n/).
- **Efficient Speech Analysis & Coding**: Enables compact parametrization of speech (LPC coefficients), drastically reducing bitrates for speech transmission and recognition systems.
