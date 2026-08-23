# Chapter 3: 5-Mark Important Practice Questions & Solved Numerical Problems

---

### Question 1: Define Time-Domain representation of a speech signal. Explain the significance of X-axis and Y-axis with an example waveform. (5 Marks)

#### Answer:

**1. Definition of Time-Domain Representation (1 Mark)**
A time-domain representation of a speech signal is the simplest and most direct plot showing how instantaneous speech amplitude (air pressure variation or voltage) changes continuously or discretely over time.

**2. Detailed Axes Significance (2 Marks)**
- **X-axis (Time)**: Measured in seconds ($\text{s}$) or milliseconds ($\text{ms}$). Indicates total duration of observation, exact timing of speech events (word onset, vowel duration, pauses, silence intervals, and speech offset).
- **Y-axis (Amplitude)**: Measures instantaneous signal strength. Represented as sound pressure in Pascals ($\text{Pa}$), electrical voltage ($\text{V}$) in analog circuits, or normalized range ($[-1, +1]$) in digital audio systems.
  - *Positive amplitude*: Represents positive air pressure compression.
  - *Negative amplitude*: Represents negative air pressure rarefaction.
  - *Larger peak-to-peak amplitude*: Corresponds to louder speech; smaller amplitude corresponds to softer speech or silence.

**3. Example Waveform Interpretation (2 Marks)**

![Time-Domain Speech Waveform](../../assets/ch03/slide_06_img_02.png)
*Figure 1.1: Time-Domain Waveform of Spoken Utterance "Sunday"*

In a typical $3.5\text{ s}$ speech recording (e.g., the word *"Sunday"*):
- **$0 - 1.1\text{ s}$**: Initial silence / flat baseline showing near-zero ambient noise.
- **$1.1 - 1.7\text{ s}$**: High-amplitude periodic oscillations representing voiced speech sound.
- **$1.7 - 2.6\text{ s}$**: Pause where amplitude returns near zero.
- **$2.6 - 2.9\text{ s}$**: Low-amplitude secondary speech segment.
- **$2.9 - 3.5\text{ s}$**: Ending silence region.

---

### Question 2: Explain Frequency-Domain representation of a speech signal. Describe how energy is distributed across different frequency bands. (5 Marks)

#### Answer:

**1. Definition of Frequency-Domain Representation (1.5 Marks)**
The frequency-domain representation describes how speech signal energy is distributed across constituent frequencies. By applying the Fourier Transform (FT) or Fast Fourier Transform (FFT), complex time-domain waveforms are decomposed into pure sinusoidal frequency components.

![Frequency Spectrum](../../assets/ch03/slide_10_img_05.png)
*Figure 2.1: Frequency-Domain Magnitude Spectrum (0 to 8000 Hz)*

**2. Graph Axes (1 Mark)**
- **X-axis (Frequency in Hz)**: Ranges from $0\text{ Hz}$ up to the Nyquist frequency ($F_s/2$). For $16\text{ kHz}$ sampling, $F_{Nyq} = 8000\text{ Hz}$.
- **Y-axis (Magnitude in dB)**: Represents energy strength of each frequency component (typically $40\text{ dB}$ to $140\text{ dB}$).

**3. Energy Distribution across Frequency Bands (2.5 Marks)**
- **$0 - 1000\text{ Hz}$ (Low Frequency Region)**: Energy concentration is highest here. Contains the fundamental frequency ($F_0$ / pitch) and primary glottal harmonics.
- **$1000 - 4000\text{ Hz}$ (Mid Frequency Region)**: Contains major vocal tract formants ($F_1, F_2, F_3$), essential for identifying vowels and spoken message content.
- **$4000 - 8000\text{ Hz}$ (High Frequency Region)**: Energy gradually decays, carrying unvoiced consonant and fricative noise information (/s/, /z/, /f/) to enhance speech clarity.

---

### Question 3: Differentiate between Time-Domain and Frequency-Domain representations of Speech Signals across key parameters. (5 Marks)

#### Answer:

| Comparison Parameter | Time-Domain Representation | Frequency-Domain Representation |
| :--- | :--- | :--- |
| **Primary Definition** | Shows how signal amplitude varies continuously over time | Shows how speech energy is distributed across different frequencies |
| **Plot Axes** | **X-axis**: Time ($\text{s}$ or $\text{ms}$)<br>**Y-axis**: Amplitude ($\text{V}$, $\text{Pa}$, or $[-1, +1]$) | **X-axis**: Frequency ($\text{Hz}$)<br>**Y-axis**: Magnitude / Power ($\text{dB}$) |
| **Information Conveyed** | Signal onset, word duration, pauses, loudness, silence intervals | Pitch ($F_0$), glottal harmonics, vocal tract formants ($F_1, F_2$), spectral tilt |
| **Generation Method** | Captured directly via microphone sensor & ADC sampling | Computed by applying Fourier Transform (FT/FFT) on time-domain signal |
| **Primary Applications** | Speech endpoint detection, silence removal, time-frame framing | Speech recognition, speaker identification, pitch extraction, noise filtering |

---

### Question 4: What is a Spectrogram? Explain how it is generated using STFT and discuss its importance in speech processing. (5 Marks)

#### Answer:

![Speech Spectrogram](../../assets/ch03/slide_16_img_06.png)
*Figure 4.1: Time-Frequency Spectrogram of Spoken Utterance "Sunday"*

**1. Definition of Spectrogram (1 Mark)**
A **spectrogram** is a time-frequency representation of a speech signal that displays how frequency content and spectral energy evolve over time, combining time-domain and frequency-domain information into a single plot.

**2. Generation via Short-Time Fourier Transform (STFT) (1.5 Marks)**
1. The continuous speech signal $x[n]$ is divided into short, overlapping frames (typically $20 - 30\text{ ms}$) using a window function $w[n]$.
2. The Discrete Fourier Transform (DFT/FFT) is computed for each windowed frame:
   $$\text{STFT}\{x[n]\}(m, \omega) = \sum_{n=-\infty}^{\infty} x[n] w[n-m] e^{-j\omega n}$$
3. The squared magnitude spectra $|\text{STFT}|^2$ are plotted side-by-side over time.

**3. Spectrogram Axes & Interpretation (1.5 Marks)**
- **X-axis**: Duration in seconds ($\text{s}$).
- **Y-axis**: Frequency range in Hertz ($0 - 8000\text{ Hz}$).
- **Color / Dark Intensity**: Logarithmic energy magnitude ($\text{dB}$). Darker/warmer regions represent high energy; lighter regions indicate low energy/silence.
- **Formant Bands**: Horizontal dark bands represent resonant vocal tract formants ($F_1, F_2, F_3$).

**4. Applications in Speech Processing (1 Mark)**
Used in Automatic Speech Recognition (ASR), speaker identification, text-to-speech synthesis, phoneme segmentation, formant tracking, emotion recognition, and noise suppression.

---

### Question 5: Define Linear Time-Invariant (LTI) Systems. Explain the properties of Linearity (Superposition Principle) and Time-Invariance with mathematical conditions. (5 Marks)

#### Answer:

**1. Definition of LTI System (1 Mark)**
A Discrete-Time Linear Time-Invariant (LTI) System is a system operator $T\{\cdot\}$ that transforms an input sequence $x[n]$ into an output sequence $y[n] = T\{x[n]\}$ while satisfying both **Linearity** and **Time-Invariance**. In speech processing, LTI systems model vocal tract filtering and transmission channels.

**2. Linearity / Superposition Principle (2 Marks)**
A system is linear if it satisfies **Scalability (Homogeneity)** and **Additivity**:
- **Scalability**: $T\{a \cdot x[n]\} = a \cdot T\{x[n]\} = a \cdot y[n]$
- **Additivity**: $T\{x_1[n] + x_2[n]\} = T\{x_1[n]\} + T\{x_2[n]\} = y_1[n] + y_2[n]$
- **Superposition Equation**: For constants $a$ and $b$:
  $$T\{a \cdot x_1[n] + b \cdot x_2[n]\} = a \cdot y_1[n] + b \cdot y_2[n]$$
  *(The response to a linear combination of inputs equals the linear combination of individual responses).*

**3. Time-Invariance Property (2 Marks)**
- **Definition**: A system is time-invariant if delaying the input sequence by $k$ samples produces an identical delay of $k$ samples in the output sequence.
- **Mathematical Condition**: If $x[n] \xrightarrow{T} y[n]$, then:
  $$x[n - k] \xrightarrow{T} y[n - k]$$
- **Significance**: System characteristics do not change over time; input signal shape remains identical, shifting only in time location.

---

### Question 6: State the Impulse Decomposition property. Explain mathematically how any discrete-time speech signal is built from unit impulses. (5 Marks)

#### Answer:

**1. Impulse Decomposition Property (2 Marks)**
The **Impulse Decomposition Property** states that any discrete-time signal $x[n]$ can be uniquely represented as a linear combination of weighted, time-shifted unit impulse functions (delta functions) $\delta[n-k]$:

$$x[n] = \sum_{k=-\infty}^{\infty} x[k] \, \delta[n - k]$$

**2. Unit Impulse Function Definition (1.5 Marks)**
The unit impulse function $\delta[n]$ is defined as:

$$\delta[n] = \begin{cases} 1, & n = 0 \\ 0, & n \neq 0 \end{cases}$$

A delayed unit impulse $\delta[n - k]$ occurs exclusively at index $n = k$:

$$\delta[n - k] = \begin{cases} 1, & n = k \\ 0, & n \neq k \end{cases}$$

**3. Signal Reconstruction Example (1.5 Marks)**
Consider discrete sequence $x[n] = \{3, 2, 1\}$ for $n = 0, 1, 2$. Applying impulse decomposition:
$$x[n] = x[0]\delta[n] + x[1]\delta[n-1] + x[2]\delta[n-2] = 3\delta[n] + 2\delta[n-1] + 1\delta[n-2]$$
- At $n = 0$: $x[0] = 3(1) + 2(0) + 1(0) = 3$
- At $n = 1$: $x[1] = 3(0) + 2(1) + 1(0) = 2$
- At $n = 2$: $x[2] = 3(0) + 2(0) + 1(1) = 1$  
The signal $x[n]$ is perfectly reconstructed.

---

### Question 7: Derive the Time-Domain Convolution Sum formula from LTI system properties. List six essential properties of Convolution. (5 Marks)

#### Answer:

**1. Mathematical Derivation of Convolution Sum (2 Marks)**
1. Represent input signal $x[n]$ using impulse decomposition:
   $$x[n] = \sum_{k=-\infty}^{\infty} x[k] \, \delta[n - k]$$
2. Pass $x[n]$ through an LTI system $T\{\cdot\}$ to obtain output $y[n]$:
   $$y[n] = T\{x[n]\} = T\left\{ \sum_{k=-\infty}^{\infty} x[k] \, \delta[n - k] \right\}$$
3. By **Linearity**, swap the operator $T$ with the summation and scaling factor $x[k]$:
   $$y[n] = \sum_{k=-\infty}^{\infty} x[k] \, T\{\delta[n - k]\}$$
4. By **Time-Invariance**, if $T\{\delta[n]\} = h[n]$ (the system impulse response), then $T\{\delta[n-k]\} = h[n-k]$. Substituting yields the **Convolution Sum**:
   $$y[n] = x[n] * h[n] = \sum_{k=-\infty}^{\infty} x[k] \, h[n - k]$$

**2. Six Essential Properties of Convolution (3 Marks)**
1. **Commutative Property**: $x[n] * h[n] = h[n] * x[n]$
2. **Associative Property**: $(x[n] * h_1[n]) * h_2[n] = x[n] * (h_1[n] * h_2[n])$
3. **Distributive Property**: $x[n] * (h_1[n] + h_2[n]) = (x[n] * h_1[n]) + (x[n] * h_2[n])$
4. **Impulse Property**: $x[n] * \delta[n] = x[n]$
5. **Shift Property**: $x[n - k_1] * h[n - k_2] = y[n - k_1 - k_2]$
6. **Finite Duration Output Length Property**: If $x[n]$ has length $L_x$ and $h[n]$ has length $L_h$, output $y[n]$ has length:
   $$L_y = L_x + L_h - 1$$

---

### Question 8: Demonstrate the step-by-step graphical/tabular convolution method to compute $y[n] = x[n] * h[n]$ for input $x[n] = \{1, 2, 1\}$ ($n=0,1,2$) and impulse response $h[n] = \{1, -1\}$ ($n=0,1$). (5 Marks)

#### Solution:

**Step 1: Signal Identification & Length Calculation (1 Mark)**
- Input $x[k] = \{1, 2, 1\}$ at $k = 0, 1, 2$ ($L_x = 3$).
- Impulse response $h[k] = \{1, -1\}$ at $k = 0, 1$ ($L_h = 2$).
- Output length $L_y = L_x + L_h - 1 = 3 + 2 - 1 = 4$ samples (indices $n = 0, 1, 2, 3$).

**Step 2: Time Reversal (Flip Impulse Response $h[-k]$) (1 Mark)**
- Original $h[k]$ at $k = 0, 1 \implies h[0]=1, h[1]=-1$.
- Flipped $h[-k]$ at $k = -1, 0 \implies h[-(-1)]=h[1]=-1$ at $k=-1$, and $h[0]=1$ at $k=0$.

**Step 3: Sliding and Sum of Products Computations (3 Marks)**

- **For $n = 0$**: Shift $h[-k]$ by 0 steps $\rightarrow h[0-k]$.
  $$\begin{array}{rccc}
  k: & 0 & 1 & 2 \\
  x[k]: & 1 & 2 & 1 \\
  h[0-k]: & 1 & -1 & \\
  \end{array}$$
  $$y[0] = x[0]h[0] = 1 \times 1 = \mathbf{1}$$

- **For $n = 1$**: Shift $h[-k]$ by 1 step right $\rightarrow h[1-k]$.
  $$\begin{array}{rccc}
  k: & 0 & 1 & 2 \\
  x[k]: & 1 & 2 & 1 \\
  h[1-k]: & -1 & 1 & \\
  \end{array}$$
  $$y[1] = (x[0]h[1]) + (x[1]h[0]) = (1 \times -1) + (2 \times 1) = -1 + 2 = \mathbf{1}$$

- **For $n = 2$**: Shift $h[-k]$ by 1 step right $\rightarrow h[2-k]$.
  $$\begin{array}{rccc}
  k: & 0 & 1 & 2 \\
  x[k]: & 1 & 2 & 1 \\
  h[2-k]: & & -1 & 1 \\
  \end{array}$$
  $$y[2] = (x[1]h[1]) + (x[2]h[0]) = (2 \times -1) + (1 \times 1) = -2 + 1 = \mathbf{-1}$$

- **For $n = 3$**: Shift $h[-k]$ by 1 step right $\rightarrow h[3-k]$.
  $$\begin{array}{rccc}
  k: & 0 & 1 & 2 \\
  x[k]: & 1 & 2 & 1 \\
  h[3-k]: & & & -1 \quad 1 \\
  \end{array}$$
  $$y[3] = x[2]h[1] = 1 \times -1 = \mathbf{-1}$$

**Final Output Sequence**:
$$\mathbf{y[n] = \{1, 1, -1, -1\} \quad \text{for } n = 0, 1, 2, 3}$$

---

### Question 9: A discrete-time LTI system has input signal $x[n] = \{2, 1, 2, 4, 3\}$ for $n = 0, 1, 2, 3, 4$ and impulse response $h[n] = \{1, -1, 2\}$ for $n = 0, 1, 2$. Calculate the complete output sequence $y[n]$ using convolution. (5 Marks)

#### Solution:

**1. Input Parameters & Output Length (1 Mark)**
- Input $x[n] = \{2, 1, 2, 4, 3\}$, starting at $n = 0$, length $L_x = 5$.
- Impulse response $h[n] = \{1, -1, 2\}$, starting at $n = 0$, length $L_h = 3$.
- Output sequence length $L_y = L_x + L_h - 1 = 5 + 3 - 1 = 7$ (indices $n = 0, 1, 2, 3, 4, 5, 6$).

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
$$\mathbf{y[n] = \{2, -1, 5, 4, 3, 5, 6\} \quad \text{for } n = 0, 1, 2, 3, 4, 5, 6}$$

---

### Question 10: A discrete-time LTI system has input signal $x[n] = \{1, 3, 2, 1\}$ for $n = 0, 1, 2, 3$ and impulse response $h[n] = \{2, -1\}$ for $n = 0, 1$. Compute output $y[n]$ and verify the output sequence length property. (5 Marks)

#### Solution:

**1. Sequence Parameters & Output Length Verification (1.5 Marks)**
- Input $x[n] = \{1, 3, 2, 1\}$, length $L_x = 4$ ($n = 0, 1, 2, 3$).
- Impulse response $h[n] = \{2, -1\}$, length $L_h = 2$ ($n = 0, 1$).
- Theoretical output length: $L_y = L_x + L_h - 1 = 4 + 2 - 1 = \mathbf{5}$ samples ($n = 0, 1, 2, 3, 4$).

**2. Convolution Computations (2.5 Marks)**

- **$y[0]$**: $y[0] = x[0]h[0] = 1 \times 2 = \mathbf{2}$
- **$y[1]$**: $y[1] = x[0]h[1] + x[1]h[0] = (1 \times -1) + (3 \times 2) = -1 + 6 = \mathbf{5}$
- **$y[2]$**: $y[2] = x[1]h[1] + x[2]h[0] = (3 \times -1) + (2 \times 2) = -3 + 4 = \mathbf{1}$
- **$y[3]$**: $y[3] = x[2]h[1] + x[3]h[0] = (2 \times -1) + (1 \times 2) = -2 + 2 = \mathbf{0}$
- **$y[4]$**: $y[4] = x[3]h[1] = 1 \times -1 = \mathbf{-1}$

**3. Output Sequence & Verification Statement (1 Mark)**
$$\mathbf{y[n] = \{2, 5, 1, 0, -1\} \quad \text{for } n = 0, 1, 2, 3, 4}$$
*Verification*: Output sequence contains exactly 5 non-zero terms, verifying $L_y = L_x + L_h - 1 = 5$.

---

### Question 11: For input sequence $x[n] = \{1, 3, 2, 1\}$ and impulse response $h[n] = \{2, -1\}$, verify the Commutative Property of Convolution by computing $y_2[n] = h[n] * x[n]$. (5 Marks)

#### Solution:

**1. Commutative Property Statement (1 Mark)**
The commutative property states that $x[n] * h[n] = h[n] * x[n]$. Reversing the roles of input and impulse response yields an identical output sequence.

**2. Computing $y_2[n] = h[n] * x[n]$ (3 Marks)**
Here $h[n] = \{2, -1\}$ ($L_h = 2$, indices $k=0,1$) and $x[n] = \{1, 3, 2, 1\}$ ($L_x = 4$, indices $k=0,1,2,3$).
Formula: $y_2[n] = \sum_{k} h[k] \, x[n - k]$

- **$y_2[0]$**: $h[0]x[0] = 2 \times 1 = \mathbf{2}$
- **$y_2[1]$**: $h[0]x[1] + h[1]x[0] = (2 \times 3) + (-1 \times 1) = 6 - 1 = \mathbf{5}$
- **$y_2[2]$**: $h[0]x[2] + h[1]x[1] = (2 \times 2) + (-1 \times 3) = 4 - 3 = \mathbf{1}$
- **$y_2[3]$**: $h[0]x[3] + h[1]x[2] = (2 \times 1) + (-1 \times 2) = 2 - 2 = \mathbf{0}$
- **$y_2[4]$**: $h[1]x[3] = -1 \times 1 = \mathbf{-1}$

**3. Comparison & Verification (1 Mark)**
- From Question 10: $y_1[n] = x[n] * h[n] = \{2, 5, 1, 0, -1\}$.
- Computed $y_2[n] = h[n] * x[n] = \{2, 5, 1, 0, -1\}$.  
Since $y_1[n] = y_2[n]$ for all $n$, the **Commutative Property** is verified.

---

### Question 12: Express $x[n] = \{1, 3, 2, 1\}$ as a sum of impulses and evaluate convolution using Linearity and the Shift Property. Prove that $x[n] * \delta[n-k] = x[n-k]$. (5 Marks)

#### Solution:

**1. Proof of Shift Property $x[n] * \delta[n-k] = x[n-k]$ (2 Marks)**
By definition of convolution:
$$x[n] * \delta[n-k] = \sum_{m=-\infty}^{\infty} x[m] \, \delta[n - k - m]$$
The delta function $\delta[n - k - m]$ is non-zero only when $n - k - m = 0 \implies m = n - k$.  
Substituting $m = n - k$ into the summation yields:
$$x[n] * \delta[n-k] = x[n - k]$$ *(Shift Property Proved)*.

**2. Impulse Decomposition of $x[n]$ (1 Mark)**
For $x[n] = \{1, 3, 2, 1\}$ ($n = 0, 1, 2, 3$):
$$x[n] = 1\delta[n] + 3\delta[n-1] + 2\delta[n-2] + 1\delta[n-3]$$

**3. Convolution via Linearity & Impulse Response $h[n] = \{2, -1\}$ (2 Marks)**
Convolving $x[n]$ with $h[n]$:
$$y[n] = x[n] * h[n] = [1\delta[n] + 3\delta[n-1] + 2\delta[n-2] + 1\delta[n-3]] * h[n]$$
Applying Distributive and Shift Properties:
$$y[n] = 1h[n] + 3h[n-1] + 2h[n-2] + 1h[n-3]$$

Evaluating sample values:
- $h[n] = \{\mathbf{2}, -1\}$ at $n=0, 1$
- $3h[n-1] = \{0, \mathbf{6}, -3\}$ at $n=1, 2$
- $2h[n-2] = \{0, 0, \mathbf{4}, -2\}$ at $n=2, 3$
- $1h[n-3] = \{0, 0, 0, \mathbf{2}, -1\}$ at $n=3, 4$

Summing all shifted sequences sample-by-sample:
- $n = 0$: $2 + 0 + 0 + 0 = \mathbf{2}$
- $n = 1$: $-1 + 6 + 0 + 0 = \mathbf{5}$
- $n = 2$: $0 - 3 + 4 + 0 = \mathbf{1}$
- $n = 3$: $0 + 0 - 2 + 2 = \mathbf{0}$
- $n = 4$: $0 + 0 + 0 - 1 = \mathbf{-1}$

$$\mathbf{y[n] = \{2, 5, 1, 0, -1\}}$$

---

### Question 13: Discuss the limitations of time-domain convolution for speech processing. Explain why Pole-Zero Modeling is required to represent the human vocal tract system. (5 Marks)

#### Answer:

**1. Limitations of Time-Domain Convolution (2.5 Marks)**
- **High Computational Complexity**: Direct convolution of long speech sequences requires $O(N \cdot M)$ multiplications and additions per frame, creating heavy computational overhead for real-time applications.
- **Hidden Filter / Frequency Behavior**: Looking only at time-domain convolution samples $y[n] = x[n] * h[n]$ makes it difficult to see how a filter shapes specific frequency bands.
- **Absence of Direct Spectral Information**: Time-domain samples do not directly indicate fundamental pitch ($F_0$), resonant bandwidths, or spectral energy distribution.
- **Obscured Vocal Tract Resonances**: Internal system characteristics like vocal tract poles (resonances) and zeros (anti-resonances) cannot be directly isolated or observed from time-domain sample sequences alone.

**2. Need for Pole-Zero System Modeling (2.5 Marks)**
- **Mathematical System Transfer Function**: Describes the vocal tract using a rational system transfer function $H(z)$ in the $Z$-domain:
  $$H(z) = \frac{B(z)}{A(z)} = G \frac{1 + \sum_{k=1}^{M} b_k z^{-k}}{1 - \sum_{k=1}^{N} a_k z^{-k}}$$
- **Physical Vocal Tract Representation**:
  - **Poles ($A(z) = 0$)**: Represent vocal tract resonant frequencies (**formants** $F_1, F_2, F_3$), producing magnitude spectrum peaks for vowels.
  - **Zeros ($B(z) = 0$)**: Represent acoustic anti-resonances (spectral dips), modeling nasal cavity coupling in nasal sounds (/m/, /n/, /ŋ/).
- **Efficient Speech Coding & Synthesis**: Compactly parametrizes speech using Linear Predictive Coding (LPC) coefficients, enabling massive data compression for speech transmission, recognition, and synthesis.

---

### Question 14: Define Poles and Zeros of a Discrete-Time System. Explain how they shape the spectral envelope of speech signals and state the BIBO stability condition in the $z$-plane. (5 Marks)

#### Answer:

**1. Definitions of Poles and Zeros (2 Marks)**
- **Transfer Function**: $H(z) = \frac{B(z)}{A(z)} = G \frac{\prod_{k=1}^{M} (z - z_k)}{\prod_{k=1}^{N} (z - p_k)}$
- **Poles ($p_k$)**: Values of $z$ for which $A(z) = 0 \implies |H(z)| \to \infty$. Represent resonant frequencies of the system.
- **Zeros ($z_k$)**: Values of $z$ for which $B(z) = 0 \implies |H(z)| = 0$. Represent frequencies where system response is completely attenuated.

**2. Acoustic Role in Speech Systems (2 Marks)**
- **Poles $\leftrightarrow$ Formants**: Poles produce prominent sharp peaks in the spectral envelope. In vocal tract modeling, poles correspond directly to acoustic formants ($F_1, F_2, F_3$) created by vocal tract resonances during vowel production.
- **Zeros $\leftrightarrow$ Anti-Resonances**: Zeros produce spectral dips/notches. In speech, zeros model acoustic anti-resonances introduced by nasal cavity coupling (in nasal consonants `/m/`, `/n/`) or vocal tract constrictions in fricatives.

**3. BIBO Stability Condition in $z$-Plane (1 Mark)**
A discrete-time LTI system is Bounded-Input Bounded-Output (BIBO) stable **if and only if all system poles lie strictly inside the unit circle** in the $z$-plane:
$$|p_k| < 1 \quad \forall k = 1, 2, \dots, N$$

---

### Question 15: Determine the poles, zeros, and BIBO stability for the transfer functions: (A) $H_1(z) = \frac{z - 0.5}{z^2 - 0.6z + 0.25}$, (B) $H_2(z) = \frac{z^2 - 1}{z^2 - 0.9z + 0.81}$. (5 Marks)

#### Solution:

**Part A: $H_1(z) = \frac{z - 0.5}{z^2 - 0.6z + 0.25}$ (2.5 Marks)**
1. **Zeros**: Set numerator $z - 0.5 = 0 \implies \mathbf{z = 0.5}$.
2. **Poles**: Set denominator $z^2 - 0.6z + 0.25 = 0$:
   $$z = \frac{0.6 \pm \sqrt{(-0.6)^2 - 4(1)(0.25)}}{2} = \frac{0.6 \pm \sqrt{0.36 - 1.0}}{2} = \frac{0.6 \pm j0.8}{2} = \mathbf{0.3 \pm j0.4}$$
3. **Stability**: Magnitude $|p| = \sqrt{0.3^2 + 0.4^2} = \sqrt{0.09 + 0.16} = \sqrt{0.25} = 0.5$.  
   Since $|p| = 0.5 < 1$, both poles lie inside the unit circle $\implies \mathbf{BIBO\ Stable}$.

**Part B: $H_2(z) = \frac{z^2 - 1}{z^2 - 0.9z + 0.81}$ (2.5 Marks)**
1. **Zeros**: Set numerator $z^2 - 1 = 0 \implies \mathbf{z = \pm 1}$ *(Zeros lie directly on the unit circle at $+1$ and $-1$)*.
2. **Poles**: Set denominator $z^2 - 0.9z + 0.81 = 0$:
   $$z = \frac{0.9 \pm \sqrt{(-0.9)^2 - 4(1)(0.81)}}{2} = \frac{0.9 \pm \sqrt{0.81 - 3.24}}{2} = \frac{0.9 \pm j1.5588}{2} = \mathbf{0.45 \pm j0.7794}$$
3. **Stability**: Magnitude $|p| = \sqrt{0.45^2 + 0.7794^2} = \sqrt{0.2025 + 0.6075} = \sqrt{0.81} = 0.9$.  
   Since $|p| = 0.9 < 1$, all poles lie inside the unit circle $\implies \mathbf{BIBO\ Stable}$.

---

### Question 16: Determine the poles, zeros, and BIBO stability for the system transfer function: $H(z) = \frac{1 - 0.5 z^{-1}}{1 - 0.8 z^{-1} + 0.64 z^{-2}}$. (5 Marks)

#### Solution:

**1. Conversion to Positive Powers of $z$ (1 Mark)**
Multiply numerator and denominator by $z^2$:
$$H(z) = \frac{z^2 (1 - 0.5 z^{-1})}{z^2 (1 - 0.8 z^{-1} + 0.64 z^{-2})} = \frac{z(z - 0.5)}{z^2 - 0.8z + 0.64}$$

**2. Zeros Calculation (1.5 Marks)**
Set numerator $z(z - 0.5) = 0$:
- $z = 0 \implies \mathbf{z_1 = 0}$ *(Zero at origin)*
- $z - 0.5 = 0 \implies \mathbf{z_2 = 0.5}$ *(Real zero at $z=0.5$)*

**3. Poles Calculation (1.5 Marks)**
Set denominator $z^2 - 0.8z + 0.64 = 0$:
$$z = \frac{0.8 \pm \sqrt{(-0.8)^2 - 4(1)(0.64)}}{2} = \frac{0.8 \pm \sqrt{0.64 - 2.56}}{2} = \frac{0.8 \pm \sqrt{-1.92}}{2} = \frac{0.8 \pm j1.38564}{2} = \mathbf{0.4 \pm j0.69282}$$

**4. Stability Verification (1 Mark)**
Pole magnitude $|p| = \sqrt{0.4^2 + 0.69282^2} = \sqrt{0.16 + 0.48} = \sqrt{0.64} = \mathbf{0.8}$.  
Since $|p| = 0.8 < 1$, both poles lie strictly inside the unit circle $\implies$ System is **BIBO Stable**.

---

### Question 17: Determine the poles, zeros, and plot locations for the discrete-time speech filter: $H(z) = \frac{z(z - 0.7)}{(z - 0.8 e^{j\pi/4})(z - 0.8 e^{-j\pi/4})}$. (5 Marks)

#### Solution:

**1. Zeros Calculation (1.5 Marks)**
Set numerator to zero: $z(z - 0.7) = 0$:
- $z = 0 \implies \mathbf{z_1 = 0}$ *(Zero at origin)*
- $z - 0.7 = 0 \implies \mathbf{z_2 = 0.7}$ *(Real zero at $z=0.7$)*

**2. Poles Calculation in Rectangular Form (2 Marks)**
Set denominator factors to zero:
- $p_1 = 0.8 e^{j\pi/4} = 0.8 \left( \cos\frac{\pi}{4} + j\sin\frac{\pi}{4} \right) = 0.8 \left( \frac{\sqrt{2}}{2} + j\frac{\sqrt{2}}{2} \right) = \mathbf{0.5657 + j0.5657}$
- $p_2 = 0.8 e^{-j\pi/4} = 0.8 \left( \cos\frac{\pi}{4} - j\sin\frac{\pi}{4} \right) = 0.8 \left( \frac{\sqrt{2}}{2} - j\frac{\sqrt{2}}{2} \right) = \mathbf{0.5657 - j0.5657}$

**3. Stability & Formant Angle Analysis (1.5 Marks)**
- **Pole Magnitude**: $|p_{1,2}| = 0.8 < 1 \implies \mathbf{BIBO\ Stable}$.
- **Formant Frequency**: Angle $\theta = \frac{\pi}{4} \text{ rad} = 45^\circ$. For a sampling rate of $F_s = 16\text{ kHz}$, the resonant formant frequency is:
  $$f_0 = \frac{\theta}{2\pi} \times F_s = \frac{\pi/4}{2\pi} \times 16000 = \frac{1}{8} \times 16000 = \mathbf{2000\text{ Hz}}$$

---

### Question 18: Compare Continuous-Time ($s$-plane) vs. Discrete-Time ($z$-plane) Pole-Zero Analysis. Show how a pole location affects speech spectrum resonance. (5 Marks)

#### Answer:

**1. Comparison of $s$-plane vs. $z$-plane Representation (3 Marks)**

| Parameter | Continuous-Time ($s$-plane) | Discrete-Time ($z$-plane) |
| :--- | :--- | :--- |
| **Mathematical Domain** | Laplace Transform $H(s) = \int h(t) e^{-st} dt$ | Z-Transform $H(z) = \sum h[n] z^{-n}$ |
| **Frequency Axis** | Imaginary axis $s = j\Omega$ ($\Omega \in (-\infty, +\infty)$) | Unit Circle $|z| = 1 \implies z = e^{j\omega}$ ($\omega \in [-\pi, +\pi]$) |
| **Stability Region** | Left-Half of $s$-plane ($\text{Re}(s) < 0$) | Inside the Unit Circle ($|z| < 1$) |
| **Pole Symbol** | Marked with **X** | Marked with **X** |
| **Zero Symbol** | Marked with **O** | Marked with **O** |

**2. Effect of Pole Location on Speech Spectrum Resonance (2 Marks)**
- **Distance from Unit Circle ($|p|$)**:
  - As $|p| \to 1$ (pole approaches unit circle), the spectral peak magnitude becomes higher and sharper (narrow formant bandwidth).
  - As $|p| \to 0$ (pole moves toward origin), the spectral peak becomes flat and smooth (broad formant bandwidth).
- **Angle around Unit Circle ($\angle p = \omega_0$)**:
  - The polar angle $\omega_0 = \angle p$ directly determines the physical formant resonance frequency $f_0 = \frac{\omega_0}{2\pi} F_s$.

