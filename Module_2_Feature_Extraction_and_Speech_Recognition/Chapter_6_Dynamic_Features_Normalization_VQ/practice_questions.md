# Chapter 6: Exam Practice Questions & Solved Numericals

> **Course**: Speech and Video Processing (CS30033)  
> **Topic**: Dynamic Features, Feature Normalization, and Vector Quantization  
> **Grading Format**: Standard University 5-Mark Questions with Complete Step-by-Step Solutions

---

### Question 1: Explain static and dynamic features in speech processing. Discuss the need for dynamic features and explain how Delta and Delta-Delta coefficients capture temporal information. (5 Marks)

#### Model Solution:
**1. Definition of Static vs Dynamic Features (2 Marks):**
- **Static Features**: Parametric vectors (e.g., 13 MFCCs) that characterize the vocal tract spectral envelope at a single instant in time ($20–30\text{ ms}$ frame).
- **Dynamic Features**: First-order (Delta $\Delta$) and second-order (Delta-Delta $\Delta\Delta$) time derivatives that quantify how spectral characteristics change over time.

**2. Need for Dynamic Features in Speech Processing (1.5 Marks):**
1. Speech is non-stationary and produced by continuously moving articulators.
2. Coarticulation transitions between adjacent phonemes contain critical acoustic information for word disambiguation.
3. Statistical models (HMMs) assume frame conditional independence; appending dynamic features provides the model with critical trajectory slopes and curvatures.

**3. Mathematical Representation of Temporal Information (1.5 Marks):**
- **Velocity ($\Delta$)**: $\Delta c_t = \frac{c_{t+1} - c_{t-1}}{2}$ (Slope / Rate of spectral change).
- **Acceleration ($\Delta\Delta$)**: $\Delta\Delta c_t = \frac{\Delta c_{t+1} - \Delta c_{t-1}}{2}$ (Curvature / Acceleration of spectral change).

---

### Question 2 (Solved Problem): Consider five consecutive frames of one MFCC coefficient: 5, 9, 14, 20, 25. Determine the delta and delta-delta coefficients for the available frames. (5 Marks)

#### Solution:

**1. Given Data (1 Mark):**
Let the frame sequence be indexed $t = 1, 2, 3, 4, 5$:
- $c_1 = 5$
- $c_2 = 9$
- $c_3 = 14$
- $c_4 = 20$
- $c_5 = 25$

**2. Delta ($\Delta$) Coefficient Calculations (2 Marks):**
Using $\Delta c_t = \frac{c_{t+1} - c_{t-1}}{2}$:
- **For Frame $t = 2$**:
  $$\Delta c_2 = \frac{c_3 - c_1}{2} = \frac{14 - 5}{2} = \frac{9}{2} = \mathbf{4.5}$$
- **For Frame $t = 3$**:
  $$\Delta c_3 = \frac{c_4 - c_2}{2} = \frac{20 - 9}{2} = \frac{11}{2} = \mathbf{5.5}$$
- **For Frame $t = 4$**:
  $$\Delta c_4 = \frac{c_5 - c_3}{2} = \frac{25 - 14}{2} = \frac{11}{2} = \mathbf{5.5}$$

**3. Delta-Delta ($\Delta\Delta$) Coefficient Calculation (2 Marks):**
Using $\Delta\Delta c_t = \frac{\Delta c_{t+1} - \Delta c_{t-1}}{2}$:
- **For Frame $t = 3$**:
  $$\Delta\Delta c_3 = \frac{\Delta c_4 - \Delta c_2}{2} = \frac{5.5 - 4.5}{2} = \frac{1.0}{2} = \mathbf{0.5}$$

**Final Summary:**
- $\Delta c_2 = \mathbf{4.5}, \quad \Delta c_3 = \mathbf{5.5}, \quad \Delta c_4 = \mathbf{5.5}$
- $\Delta\Delta c_3 = \mathbf{0.5}$

---

### Question 3 (Solved Problem): Suppose the values of one MFCC coefficient from four consecutive speech frames are 6, 10, 14, and 18. Apply mean normalization and variance normalization to these values and determine the normalized feature values. (5 Marks)

#### Solution:

**1. Mean Normalization Calculation (2 Marks):**
- Given sample values: $c_1 = 6, c_2 = 10, c_3 = 14, c_4 = 18$ ($N = 4$).
- Mean $\mu$:
  $$\mu = \frac{6 + 10 + 14 + 18}{4} = \frac{48}{4} = \mathbf{12.0}$$
- Mean-centered features $\tilde{c}_t = c_t - \mu$:
  - $\tilde{c}_1 = 6 - 12 = \mathbf{-6}$
  - $\tilde{c}_2 = 10 - 12 = \mathbf{-2}$
  - $\tilde{c}_3 = 14 - 12 = \mathbf{+2}$
  - $\tilde{c}_4 = 18 - 12 = \mathbf{+6}$
  $$\mathbf{\tilde{c} = \{-6, -2, +2, +6\}}$$

**2. Variance Normalization Calculation (3 Marks):**
- Variance $\sigma^2$:
  $$\sigma^2 = \frac{1}{N} \sum_{t=1}^4 (c_t - \mu)^2 = \frac{(-6)^2 + (-2)^2 + (+2)^2 + (+6)^2}{4} = \frac{36 + 4 + 4 + 36}{4} = \frac{80}{4} = \mathbf{20.0}$$
- Standard Deviation $\sigma$:
  $$\sigma = \sqrt{20} \approx \mathbf{4.4721}$$
- Standardized feature values $\hat{c}_t = \frac{\tilde{c}_t}{\sigma}$:
  - $\hat{c}_1 = \frac{-6}{\sqrt{20}} = \frac{-6}{4.4721} \approx \mathbf{-1.3416}$
  - $\hat{c}_2 = \frac{-2}{\sqrt{20}} = \frac{-2}{4.4721} \approx \mathbf{-0.4472}$
  - $\hat{c}_3 = \frac{+2}{\sqrt{20}} = \frac{+2}{4.4721} \approx \mathbf{+0.4472}$
  - $\hat{c}_4 = \frac{+6}{\sqrt{20}} = \frac{+6}{4.4721} \approx \mathbf{+1.3416}$

**Final Normalized Features:**
$$\mathbf{\hat{c} = \{-1.3416, -0.4472, +0.4472, +1.3416\}}$$

---

### Question 4 (Solved Problem): Briefly explain the VQ encoding process. Suppose an input MFCC vector is $\mathbf{x} = [3, 2]$ and two codewords are $\mathbf{C}_1 = [1, 1]$ and $\mathbf{C}_2 = [6, 5]$. Using the Euclidean distance, determine which codeword the input vector $\mathbf{x}$ belongs to. (5 Marks)

#### Solution:

**1. VQ Encoding Explanation (2 Marks):**
Vector Quantization encoding assigns an arbitrary continuous input vector $\mathbf{x}$ to the nearest prototype codeword $\mathbf{C}_i$ from a predefined codebook $\mathcal{C}$ by minimizing the Euclidean distance metric $d(\mathbf{x}, \mathbf{C}_i)$.

**2. Step-by-Step Distance Computations (2 Marks):**
- **Distance to Codeword $\mathbf{C}_1 = [1, 1]$**:
  $$d(\mathbf{x}, \mathbf{C}_1) = \sqrt{(3 - 1)^2 + (2 - 1)^2} = \sqrt{2^2 + 1^2} = \sqrt{4 + 1} = \sqrt{5} \approx \mathbf{2.2361}$$
- **Distance to Codeword $\mathbf{C}_2 = [6, 5]$**:
  $$d(\mathbf{x}, \mathbf{C}_2) = \sqrt{(3 - 6)^2 + (2 - 5)^2} = \sqrt{(-3)^2 + (-3)^2} = \sqrt{9 + 9} = \sqrt{18} \approx \mathbf{4.2426}$$

**3. Decision & Conclusion (1 Mark):**
Since $d(\mathbf{x}, \mathbf{C}_1) = 2.2361 < d(\mathbf{x}, \mathbf{C}_2) = 4.2426$, the input vector $\mathbf{x} = [3, 2]$ is **assigned to Codeword $\mathbf{C}_1 = [1, 1]$**.
