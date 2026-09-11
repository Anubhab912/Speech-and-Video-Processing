# 🎙️ Module 2: Feature Extraction and Speech Recognition

Welcome to **Module 2: Feature Extraction and Speech Recognition** of the **Speech and Video Processing (CS30033)** course curriculum.

This module covers the core mathematical, algorithmic, and statistical foundations used to extract robust acoustic representations from digital speech waveforms and recognize spoken words using pattern matching and Hidden Markov Models (HMMs).

---

## 🗺️ Module 2 Learning Architecture

```mermaid
flowchart TD
    subgraph Chapter 5: Feature Extraction (MFCC & LPCC)
        A1["Raw Speech s[n]"] --> A2["Pre-emphasis & Windowing"]
        A2 --> A3["FFT Power Spectrum"]
        A3 --> A4["Mel Filterbank & Log Compression"]
        A4 --> A5["DCT Decorrelation → 13 Static MFCCs"]
        A1 --> A6["LPC Analysis → Recursive LPCCs"]
    end

    subgraph Chapter 6: Dynamic Features & Normalization
        B1["Static MFCCs (c_t)"] --> B2["Delta (Δ - Velocity) & Delta-Delta (ΔΔ - Acceleration)"]
        B2 --> B3["Concatenated 39-Dimensional Feature Vector"]
        B3 --> B4["Mean & Variance Normalization / CMN"]
        B4 --> B5["Vector Quantization (VQ Codebook)"]
    end

    subgraph Chapter 7: Pattern Matching & HMMs
        C1["Acoustic Vectors / VQ Symbols"] --> C2["Hidden Markov Model λ = (A, B, π)"]
        C2 --> C3["Problem 1: Evaluation (Forward Algorithm)"]
        C2 --> C4["Problem 2: Decoding (Viterbi Algorithm)"]
        C2 --> C5["Problem 3: Learning (Baum-Welch EM Training)"]
        C4 --> C6["🔤 Recognized Text Output W*"]
    end

    A5 --> B1
    A6 --> B1
    B5 --> C1
```

---

## 📂 Chapter Contents & Quick Links

| Chapter | Topic | Key Concepts | Notes & Practice Links |
| :--- | :--- | :--- | :---: |
| **Chapter 5** | **Feature Extraction Overview, Real Cepstrum, MFCC & LPCC** | Source-Filter model, Homomorphic deconvolution, Quefrency & Liftering, Real vs Complex Cepstrum, Mel Filterbank, 13 Static MFCCs, LPCC recursion. | [Lecture Notes](Chapter_5_Feature_Extraction_MFCC_LPCC/README.md)<br>[Practice Q&A](Chapter_5_Feature_Extraction_MFCC_LPCC/practice_questions.md) |
| **Chapter 6** | **Dynamic Features, Normalization & Vector Quantization** | Static vs Dynamic features, Delta ($\Delta$) velocity, Delta-Delta ($\Delta\Delta$) acceleration, 39-D vector, Mean & Variance normalization, CMN, VQ codebooks, LBG algorithm. | [Lecture Notes](Chapter_6_Dynamic_Features_Normalization_VQ/README.md)<br>[Practice Q&A](Chapter_6_Dynamic_Features_Normalization_VQ/practice_questions.md) |
| **Chapter 7** | **Pattern Matching & HMM-based Speech Recognition** | Template matching vs Statistical models, DTW, HMM parameters $\lambda = (A, B, \pi)$, 3 Fundamental Problems, Forward Algorithm, Viterbi Algorithm, Baum-Welch training, GMM-HMMs. | [Lecture Notes](Chapter_7_Pattern_Matching_and_HMM/README.md)<br>[Practice Q&A](Chapter_7_Pattern_Matching_and_HMM/practice_questions.md) |

---

## 📘 Official Master Question Bank Solutions

- 📖 **[Module 2 Master Question Bank Solutions (53 SAQs + 30 LAQs)](Question_Bank_SAQ_LAQ_Solutions.md)**:
  - **Part I: 53 Short Answer Questions (SAQs)** $\to$ Strictly **2 Marks Each** with crisp definitions, formulas, and real-world significance.
  - **Part II: 30 Long Answer Questions & Solved Numericals (LAQs)** $\to$ Strictly **5 Marks Each** with step-by-step mathematical workings, mark allocations, comparison matrices, and diagrams.
    - *Solved Numericals Include*: Delta & Delta-Delta calculations, Mean & Variance Normalization, VQ Euclidean Distance matching, Forward Algorithm likelihood evaluation, and Viterbi optimal path decoding.
