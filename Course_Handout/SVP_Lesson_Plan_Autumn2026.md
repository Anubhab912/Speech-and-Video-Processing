# Course Handout: Speech and Video Processing (CS30033)

**School of Computer Engineering**  
**KIIT Deemed to be University, Bhubaneswar**  
**Session:** July–November, 2026  
**L-T-P-Cr Structure:** 3-1-0-3  
**Course Code:** CS30033  
**Course Title:** Speech and Video Processing  

---

## Course Faculty & Contact Details
- **Faculty:** Dr. Kunal Anand, Asst. Professor
- **Contact Address:** Chamber-G, C-101; Campus 25
- **Visiting Hours:** 5:00 PM – 6:00 PM (Monday, Wednesday, Thursday)

---

## Course Objectives
1. To introduce speech properties, issues, and speech-processing concepts for prediction.
2. To learn feature extraction, selection, and speech recognition algorithms.
3. To understand video principles and its processing techniques.
4. To learn motion estimation, optimization techniques, object tracking, boundary detection, and compression techniques.
5. To implement the algorithms using Python and auxiliary tools.

---

## Course Outcomes (COs)
At the end of the course, students will be able to:
- **CO1:** Assess the mechanisms of human speech production systems and methods for speech feature extraction.
- **CO2:** Apply the algorithms of speech analysis and speech recognition.
- **CO3:** Incorporate fundamental techniques in digital video processing, including image characteristics and sensors.
- **CO4:** Implement motion estimation and object tracking algorithms on video sequences.
- **CO5:** Develop approximated real-life speech and video processing systems using Python.
- **CO6:** Apply suitable Learning Models in different problems to obtain desirable results.

---

## Textbooks & Reference Books

### Text Books
1. *Fundamentals of Speech Recognition* – L. Rabiner and B. Juang, Prentice Hall Signal Processing Series.
2. *Discrete-Time Speech Signal Processing: Principles and Practice* – Thomas F. Quatieri, Prentice Hall.
3. *Digital Video Processing* – A. Murat Tekalp, Prentice Hall.
4. *Video Processing and Communications* – Yao Wang, J. Ostermann, and Qin Zhang, Pearson Education.

### Reference Books
1. *Speech and Audio Signal Processing* – B. Gold and N. Morgan, Wiley.
2. *Digital Image Sequence Processing, Compression, and Analysis* – Todd R. Reed, CRC Press.
3. *Handbook of Image and Video Processing* – Al Bovik, Academic Press, Second Edition.

---

## Evaluation Scheme

| ES No. | Evaluation Component | Percentage of Evaluation |
| :--- | :--- | :---: |
| 1 | Mid-Semester Examination | 20% (20 Marks) |
| 2 | Activities (Quizzes, Assignments, Presentations) | 30% (30 Marks) |
| 3 | End-Semester Examination | 50% (50 Marks) |
| **Total** | | **100% (100 Marks)** |

---

## Tentative Activity Calendar (Autumn 2026)

| Activity No. | Type | Date Range | Marks | Target Course Outcomes |
| :---: | :--- | :---: | :---: | :---: |
| **Activity 1** | Problem Solving Assignment | 20th July – 14th Aug | 5 | CO1, CO2 |
| **Activity 2** | Quiz | 17th Aug – 31st Aug | 5 | CO1, CO2 |
| **Activity 3** | Critical Thinking Assignment | 01st Sep – 06th Sep | 5 | CO1, CO2, CO3 |
| **MID-SEM** | **Mid-Semester Examination** | **07th Sep – 12th Sep 2026** | **20** | **CO1, CO2, CO3** |
| **Activity 4** | Problem Solving / Code | 14th Sep – 30th Sep | 5 | CO3, CO4 |
| **Activity 5** | Quiz / Viva | 01st Oct – 15th Oct | 5 | CO3, CO4 |
| **Activity 6** | Presentation / Project | 21st Oct – 06th Nov | 5 | CO3, CO4, CO5, CO6 |
| **END-SEM** | **End-Semester Examination** | **09th Nov – 18th Nov 2026** | **50** | **CO1 – CO6** |

---

## Detailed Syllabus & Lecture Breakdown

### Module I: Speech Processing Concepts (10 Lectures | Serials 1–10)
1. Introduction, applications of speech and video processing *(Slide Deck: Ch-01)*
2. Speech production mechanism, Speech perception and characteristics of speech signals *(Slide Deck: Ch-01)*
3. Sampling, quantization, and digital representation of speech, Spectrogram and time-frequency representation *(Slide Deck: Ch-02)*
4. Convolution and Speech Systems, Pole-zero Modeling
5. DFT and FFT Representation for Speech Processing, FFT Properties, Spectral Estimation using DFT
6. Linear Filter Banks
7. Linear prediction and prediction error, Linear Predictive Coding (LPC)
8. Python Implementation of FFT Spectrum Analysis, Spectrogram Generation, LPC Analysis

### Module II: Feature Extraction and Speech Recognition (7 Lectures | Serials 11–17)
1. Feature extraction overview, Real Cepstrum, Cepstral analysis, MFCC and LPCC
2. Dynamic features (Delta, Delta-Delta) and normalization, Vector Quantization
3. Pattern matching approaches, HMM-based speech recognition

### Module III: Basics of Video Processing (8 Lectures | Serials 18–25)
1. Video formation, perception and representation
2. Principles of color video, video cameras and displays, Pinhole camera model
3. Camera motion, shape model, scene model
4. 2D Motion Models, 3D Rigid Motion & Projective Mapping

### Module IV: Motion Estimation Techniques (8 Lectures | Serials 26–33)
1. Optical flow and motion representation
2. Motion estimation criteria and optimization methods
3. Pixel-based and block matching motion estimation
4. Gradient-based methods, intensity matching, feature matching
5. Frequency-domain motion estimation and Depth from motion
6. Motion Analysis Applications: Video Summarization & Surveillance

### Module V: Object Tracking and Segmentation (7 Lectures | Serials 34–40)
1. 2D and 3D video tracking, blob tracking, kernel-based contour tracking
2. Filtering, mosaicking, video segmentation, mean shift-based segmentation
3. Active shape model, video shot boundary detection, inter-frame compression
4. Python/OpenCV Implementation of Video Frame Extraction, Color Space Conversion, Mean Shift Tracking
