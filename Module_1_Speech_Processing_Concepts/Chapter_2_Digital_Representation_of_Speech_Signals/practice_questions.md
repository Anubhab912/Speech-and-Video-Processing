# Chapter 2: PPT Slide Exercises & Solved Numerical Problems

> [!NOTE]  
> **Status**: `[Needs clarification]` — Pending user-supplied 5-mark question list (to be updated next week). The problems below are solved directly from the official PowerPoint presentation slides (Slide 28 Class Exercise, Slide 30 Exercise, and Slide 31 Practice Problems).

---

## Conceptual Questions (Derived from PPT Outcomes)

### Question 1
**Explain the complete process of converting an analog speech signal into a digital signal using ADC.**

#### Solution:
Analog-to-Digital Conversion (ADC) transforms a continuous-time, continuous-amplitude acoustic wave into a discrete-time, discrete-amplitude binary sequence through three stages:

1. **Sampling (Continuous-to-Discrete Conversion)**:
   - Measures signal amplitude at uniform time intervals $T_s = 1 / F_s$.
   - Converts continuous signal $x_a(t)$ into discrete-time sequence $x[n] = x_a(n T_s)$.
   - Requires $F_s \ge 2 f_{max}$ per the Nyquist theorem.
2. **Quantization**:
   - Maps continuous sample amplitudes to the nearest discrete voltage level among $L = 2^N$ allowed quantization levels.
   - Restricts amplitude values to a finite set with step size $\Delta = (V_{max} - V_{min}) / 2^N$.
   - Introduces quantization error $e[n] = x[n] - x_q[n]$ bounded within $[-\Delta/2, +\Delta/2]$.
3. **Coding (Binary Encoding)**:
   - Assigns a unique $N$-bit binary sequence (code word) to each quantized discrete amplitude level $x_q[n]$ for digital storage or transmission.

---

### Question 2
**State the Nyquist-Shannon Sampling Theorem. Explain the concept of Aliasing and discuss how it can be prevented.**

#### Solution:
1. **Nyquist-Shannon Sampling Theorem**:
   - *"To completely and accurately reconstruct a continuous-time signal from its discrete samples without distortion, the sampling frequency ($F_s$) must be at least twice the maximum frequency component ($f_{max}$) contained within the signal."*
   - Mathematical condition: $F_s \ge 2 f_{max}$. Minimum rate $2 f_{max}$ is the **Nyquist Rate**.

2. **Aliasing Phenomenon**:
   - Occurs when a signal is under-sampled ($F_s < 2 f_{max}$).
   - High-frequency components fold over into the lower frequency spectrum, causing high frequencies to masquerade as lower frequencies and distorting the reconstructed signal.

3. **Prevention of Aliasing**:
   - Sample at or above the Nyquist rate ($F_s \ge 2 f_{max}$).
   - Apply an analog low-pass **Anti-Aliasing Filter** prior to sampling to remove frequency components higher than $F_s / 2$.

---

## Solved PowerPoint Slide Numerical Exercises

### Problem 1 (Slide 28 Exercise)
**A speech signal is uniformly quantized using 16 bits per sample over a range of $\pm 5\text{ V}$. Find the quantization step size ($\Delta$). If the sampling frequency is $12\text{ Hz}$, what will be the size of the file for a $10\text{ sec}$ recording?**

#### Step-by-Step Solution:

**Given:**
- Bit resolution ($N$) = $16\text{ bits}$
- Voltage range ($V_{min}$ to $V_{max}$) = $-5\text{ V}$ to $+5\text{ V} \rightarrow \text{Range} = 10\text{ V}$
- Sampling frequency ($F_s$) = $12\text{ Hz}$
- Duration ($T$) = $10\text{ seconds}$

**1. Quantization Step Size ($\Delta$):**
$$L = 2^N = 2^{16} = 65,536\text{ levels}$$

$$\Delta = \frac{V_{max} - V_{min}}{L} = \frac{10\text{ V}}{65,536} \approx \mathbf{0.000152588\text{ V} \quad (0.1526\text{ mV})}$$

**2. Digital File Size Calculation:**
$$\text{File Size (bits)} = F_s \times N \times T = 12 \times 16 \times 10 = 1,920\text{ bits}$$

$$\text{File Size (bytes)} = \frac{1,920}{8} = \mathbf{240\text{ bytes}}$$

---

### Problem 2 (Slide 30 Exercise)
**Suppose there is an 8-bit ADC with input range $-1\text{ V}$ to $+1\text{ V}$. Find:**
1. Quantization Step size ($\Delta$)
2. Maximum Quantization Error ($e_{max}$)
3. Mean Squared Quantization Error ($\sigma_e^2$)

#### Step-by-Step Solution:

**Given:**
- $N = 8\text{ bits} \rightarrow L = 2^8 = 256\text{ levels}$
- Range = $-1\text{ V}$ to $+1\text{ V} \rightarrow \Delta V = 2\text{ V}$

**1. Quantization Step Size ($\Delta$):**
$$\Delta = \frac{\text{Range}}{L} = \frac{2\text{ V}}{256} = \mathbf{0.0078125\text{ V}}$$

**2. Maximum Quantization Error ($e_{max}$):**
$$e_{max} = \frac{\Delta}{2} = \frac{0.0078125\text{ V}}{2} = \mathbf{0.00390625\text{ V}}$$

**3. Mean Squared Quantization Error ($\sigma_e^2$):**
$$\sigma_e^2 = \frac{\Delta^2}{12} = \frac{(0.0078125)^2}{12} = \frac{6.1035 \times 10^{-5}}{12} = \mathbf{5.086 \times 10^{-6}\text{ V}^2}$$

---

### Problem 3 (Slide 31 Practice Problem 1 & 2)
**Part A: A 10-bit ADC converts analog signals in the range $-5\text{ V}$ to $+5\text{ V}$. Determine Quantization step size, maximum quantization error, and mean squared quantization error.**  
**Part B: Suppose the ADC is modified to operate with 12-bit resolution instead of 10-bit resolution. Discuss how this change affects ADC operation.**

#### Step-by-Step Solution:

**Part A (10-bit ADC):**
- $N = 10\text{ bits} \rightarrow L = 2^{10} = 1024\text{ levels}$
- $\text{Range} = 10\text{ V}$

1. **Step Size ($\Delta$)**:
   $$\Delta = \frac{10\text{ V}}{1024} = \mathbf{0.009765625\text{ V}}$$
2. **Maximum Error ($e_{max}$)**:
   $$e_{max} = \frac{\Delta}{2} = \mathbf{0.0048828125\text{ V}}$$
3. **Mean Squared Error ($\sigma_e^2$)**:
   $$\sigma_e^2 = \frac{\Delta^2}{12} = \frac{(0.009765625)^2}{12} = \mathbf{7.947 \times 10^{-6}\text{ V}^2}$$

**Part B (Comparison with 12-bit ADC):**
- For $N = 12\text{ bits}$, $L = 2^{12} = 4096\text{ levels}$.
- New step size $\Delta_{12} = \frac{10\text{ V}}{4096} = 0.0024414\text{ V}$.
- **Operational Impact**: Step size and maximum error are reduced by $75\%$ (factor of 4). Mean squared quantization noise power decreases by a factor of 16 ($12\text{ dB}$ improvement in Signal-to-Quantization Noise Ratio), providing higher audio fidelity at the cost of a $20\%$ increase in bit rate and storage requirements per sample.

---

### Problem 4 (Slide 31 Practice Problem 3)
**A speech acquisition system samples a signal at $16\text{ kHz}$ using a 10-bit ADC over the input range $-1.5\text{ V}$ to $+1.5\text{ V}$. Calculate Quantization step size, maximum quantization error, and mean squared quantization error.**

#### Step-by-Step Solution:

**Given:**
- $F_s = 16,000\text{ Hz}$
- $N = 10\text{ bits} \rightarrow L = 1024\text{ levels}$
- Range = $-1.5\text{ V}$ to $+1.5\text{ V} \rightarrow \Delta V = 3\text{ V}$

1. **Quantization Step Size ($\Delta$)**:
   $$\Delta = \frac{3\text{ V}}{1024} = \mathbf{0.0029296875\text{ V}}$$

2. **Maximum Quantization Error ($e_{max}$)**:
   $$e_{max} = \frac{\Delta}{2} = \frac{0.0029296875}{2} = \mathbf{0.00146484375\text{ V}}$$

3. **Mean Squared Quantization Error ($\sigma_e^2$)**:
   $$\sigma_e^2 = \frac{\Delta^2}{12} = \frac{(0.0029296875)^2}{12} = \mathbf{7.1525 \times 10^{-7}\text{ V}^2}$$
