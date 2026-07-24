# Standard Academic Syllabus & Lesson Plan: Speech and Video Processing

**Target Audience:** Undergraduate / Postgraduate Students (Computer Science, ECE, Data Science, AI/ML)  
**Standard Credit Structure:** 3-1-0-3 (30–40 Lecture Hours)  
**Course Code:** CS30033 / ECE4050 (Standard University Elective)  
**Course Title:** Speech and Video Processing  

---

## Course Overview & Objectives
1. **Speech Signal Foundations**: Introduce human speech production, acoustic phonetics, sampling, quantization, and linear predictive modeling.
2. **Feature Extraction & Recognition**: Master spectral feature extraction (MFCC, LPCC), vector quantization, and pattern recognition (HMMs, DTW).
3. **Video Processing Fundamentals**: Understand color spaces (RGB, YCbCr), pinhole camera models, 2D/3D motion models, and video perception.
4. **Motion Estimation & Analytics**: Implement optical flow, block-matching motion estimation algorithms (EBMA), and video summarization.
5. **Object Tracking & Segmentation**: Apply Mean-Shift, Active Shape Models, boundary detection, and OpenCV implementations for real-time video analytics.

---

## Course Outcomes (COs)
At the end of this course, students across any university program will be able to:
- **CO1:** Analyze human speech production anatomy, speech perception, and digital sampling/quantization mechanisms.
- **CO2:** Extract spectral features (MFCC, LPCC) and implement pattern recognition models (HMMs, DTW) for speech signals.
- **CO3:** Explain fundamental principles of digital video formation, color models, camera geometry, and 3D rigid motion.
- **CO4:** Implement motion estimation (Optical Flow, Block Matching) and video analytics algorithms.
- **CO5:** Develop end-to-end Python/OpenCV applications for speech recognition and video object tracking.
- **CO6:** Design computer vision and audio processing pipelines for multimodal artificial intelligence applications.

---

## Recommended Textbooks & Academic References

### Primary Text Books
1. *Fundamentals of Speech Recognition* – L. Rabiner and B. Juang, Prentice Hall Signal Processing Series.
2. *Discrete-Time Speech Signal Processing: Principles and Practice* – Thomas F. Quatieri, Prentice Hall.
3. *Digital Video Processing* – A. Murat Tekalp, Prentice Hall.
4. *Video Processing and Communications* – Yao Wang, J. Ostermann, and Qin Zhang, Pearson Education.

### Reference Books & Standards
1. *Speech and Audio Signal Processing* – B. Gold and N. Morgan, Wiley.
2. *Digital Image Sequence Processing, Compression, and Analysis* – Todd R. Reed, CRC Press.
3. *Handbook of Image and Video Processing* – Al Bovik, Academic Press.

---

## Standard University Evaluation Scheme

| Component | Weightage | Target Learning Objectives |
| :--- | :---: | :--- |
| **Continuous Evaluation** (Quizzes, Assignments, Python Labs) | 30% | Practical implementation, problem solving & coding |
| **Mid-Semester Examination** | 20% | Conceptual grasp of Module I & Module II topics |
| **End-Semester Examination** | 50% | Comprehensive evaluation of Modules I – V |
| **Total** | **100%** | **Full Academic Assessment** |

---

## Recommended 16-Week Academic Schedule

| Phase / Weeks | Target Topics & Milestones | Evaluation & Assignments |
| :---: | :--- | :--- |
| **Weeks 1 – 3** | Speech Production, Acoustic Phonetics, Analog-to-Digital Conversion (Sampling, Quantization, Nyquist Rate) | Assignment 1: ADC Numericals |
| **Weeks 4 – 5** | Convolution, Pole-Zero Modeling, DFT/FFT Spectral Estimation, Linear Filter Banks | Quiz 1: Spectral Analysis |
| **Weeks 6 – 7** | Linear Predictive Coding (LPC), MFCC/LPCC Feature Extraction | Lab Assignment: Python Audio Processing |
| **Week 8** | **Mid-Semester Assessment** | **Mid-Sem Exam** |
| **Weeks 9 – 10** | Vector Quantization, HMM Speech Recognition, Video Perception & Color Models | Assignment 2: HMM & Color Spaces |
| **Weeks 11 – 12** | Camera Models, 2D/3D Motion Models, Optical Flow & Block Matching | Quiz 2: Motion Estimation |
| **Weeks 13 – 14** | Object Tracking (Mean-Shift, Active Shape Models), Video Segmentation & Compression | Project / Lab Viva: OpenCV Tracking |
| **Weeks 15 – 16** | Course Revision & Final Assessment | **End-Sem Exam** |

---

## Detailed Syllabus & Lecture Breakdown

### Module I: Speech Processing Concepts (10 Lectures)
1. Introduction and application domains of speech and video processing.
2. Human speech production mechanism, vocal tract anatomy, speech perception, and signal characteristics.
3. Sampling, quantization, continuous vs. discrete representations, spectrograms, and time-frequency analysis.
4. Convolution in speech systems and pole-zero modeling of vocal tract transfer functions.
5. Discrete Fourier Transform (DFT) and Fast Fourier Transform (FFT) for speech, spectral estimation.
6. Linear Filter Banks, Mel-scale filtering, sub-band analysis.
7. Linear prediction, prediction error, and Linear Predictive Coding (LPC).
8. Python Implementation: Spectral analysis (`scipy`), spectrogram generation (`librosa`), and LPC parameter extraction.

### Module II: Feature Extraction and Speech Recognition (7 Lectures)
1. Feature extraction overview, Real/Complex Cepstrum, MFCC and LPCC derivation.
2. Dynamic features (Delta, Delta-Delta), feature normalization, Vector Quantization (VQ) & LBG algorithm.
3. Pattern matching (Dynamic Time Warping) and Hidden Markov Model (HMM) speech recognition architecture.

### Module III: Basics of Video Processing (8 Lectures)
1. Video formation, temporal perception, digital video representation and frame rate standards.
2. Principles of color video (RGB, YUV, YCbCr), video sensors (CCD/CMOS), displays, and pinhole camera model.
3. Camera motion, 2D/3D shape models, scene modeling.
4. 2D Motion Models (Affine, Projective) and 3D Rigid Motion transformations.

### Module IV: Motion Estimation Techniques (8 Lectures)
1. Optical flow constraint equation and motion field representation.
2. Motion estimation criteria (SAD, MAD, MSE) and optimization techniques.
3. Block-matching algorithms (Exhaustive Block Matching, Fast Search methods).
4. Gradient-based methods (Horn-Schunck, Lucas-Kanade) and feature-based matching.
5. Frequency-domain motion estimation and depth estimation from motion.
6. Applications: Video summarization, keyframe extraction, and automated surveillance.

### Module V: Object Tracking and Segmentation (7 Lectures)
1. 2D/3D video tracking, blob tracking, kernel-based contour tracking (Mean-Shift, CamShift).
2. Kalman/Particle filtering, video mosaicking, mean-shift video segmentation.
3. Active Shape Models (ASM), shot boundary detection, motion-compensated inter-frame video compression (MPEG/H.264).
4. Python/OpenCV Implementation: Frame extraction, color conversion, object tracking using OpenCV (`cv2`).
