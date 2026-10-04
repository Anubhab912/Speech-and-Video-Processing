# Chapter 8: Exam Practice Questions & Model Solutions

> **Course**: Speech and Video Processing (CS30033)  
> **Topic**: Fundamentals of Video Formation, Perception, and Representation  
> **Grading Format**: Standard University 5-Mark Questions with Step-by-Step Marking Schemes

---

### Question 1: Explain the step-by-step physical and electronic process of video formation. Discuss the roles of the optical lens system, sensor array, and ADC digitizer. (5 Marks)

#### Model Solution:

**1. Overview of Video Formation Pipeline (1 Mark):**
Video formation is the multi-stage conversion of a continuous real-world 3D scene into a discrete sequence of 2D digital image grids (frames) captured at regular time intervals ($t$). The pipeline follows the sequence:
$$\text{Real Scene} \longrightarrow \text{Optics/Lens} \longrightarrow \text{Sensor Array} \longrightarrow \text{Electrical Signals} \longrightarrow \text{A/D Digitizer} \longrightarrow \text{Digital Frames Sequence}$$

**2. Physical and Electronic Components (3 Marks):**
1. **Optics / Lens System (1 Mark)**:
   - Gathers diverging light rays reflected from surfaces in the 3D scene.
   - Refracts and focuses the optical wavefront through an aperture onto the camera's image plane based on perspective geometry.
2. **Sensor Array (Photosites) (1 Mark)**:
   - Comprises a 2D grid of millions of light-sensitive photodetectors (CCD or CMOS elements).
   - Exploits the photoelectric effect to convert incoming photon energy into proportional accumulated electrical charges (analog voltages).
3. **A/D Converter (Digitizer) (1 Mark)**:
   - **Spatial Sampling**: Discretizes continuous 2D space into regular rows and columns of picture elements (**pixels**).
   - **Temporal Sampling**: Samples the dynamic scene at fixed periodic time intervals (e.g., $1/30\text{ s}$ or $1/60\text{ s}$) dictated by the frame rate.
   - **Quantization**: Converts continuous analog voltage levels into discrete binary values of bit depth $b$ (e.g., $0–255$ for 8-bit).

**3. Output Digital Representation (1 Mark):**
The final output is a 3D numeric tensor $V[x, y, t]$ with dimensions $H \times W \times C$ per frame, where $H$ is frame height, $W$ is frame width, and $C$ is the number of color channels ($C = 3$ for RGB/YCbCr).

---

### Question 2: Explain the biological and psychological mechanisms behind human video perception. Define persistence of vision, apparent motion, and the Critical Flicker Fusion (CFF) threshold. (5 Marks)

#### Model Solution:

**1. Physiological Basis & Persistence of Vision (2 Marks):**
- Video systems exploit the perceptual limitations of the Human Visual System (HVS) rather than capturing infinite continuous data.
- **Persistence of Vision**: Retinal photoreceptor chemical responses (rods and cones) do not terminate instantly when an optical stimulus vanishes; an image impression lingers on the retina for roughly $\frac{1}{16}$ to $\frac{1}{10}$ of a second ($60–100\text{ ms}$).
- When consecutive still images appear with slight displacements within this interval, the visual cortex integrates them into a unified, continuous sensation.

**2. Apparent Motion (Phi Phenomenon & Beta Movement) (1.5 Marks):**
- The psychological illusion whereby the brain perceives fluid continuous motion from an alternating or sequential presentation of static visual stimuli.
- If spatial displacements between frames are small and the frame rate exceeds $\approx 16–24\text{ fps}$, the brain automatically infers smooth trajectory paths between discrete positions.

**3. Critical Flicker Fusion (CFF) Threshold (1.5 Marks):**
- The CFF is the frequency (measured in $\text{Hz}$) at which an intermittent, flashing light stimulus ceases to flicker and is perceived as completely steady and continuous.
- In normal photopic (daylight) vision, CFF occurs between **$50\text{ Hz}$ and $60\text{ Hz}$**.
- If refresh rates fall below CFF, viewers experience perceptible strobing and ocular fatigue.
- *Cinema implementation*: While films are captured at $24\text{ fps}$ to save film stock, multi-blade projection shutters flash each frame 2 or 3 times to raise the display frequency to $48\text{ Hz}$ or $72\text{ Hz}$, surpassing the CFF threshold.

---

### Question 3: Differentiate between Progressive Scanning and Interlaced Scanning in digital video systems. Discuss the historical bandwidth rationale for interlacing and the causes of "combing" artifacts. (5 Marks)

#### Model Solution:

**1. Scanning Mechanisms (2 Marks):**
- **Progressive Scanning ($1080\text{p}$)**: All horizontal scan lines across the frame ($1, 2, 3, \dots, H$) are scanned and displayed sequentially from top to bottom in a single vertical pass. Each frame captures the complete scene at a single instant $t$.
- **Interlaced Scanning ($1080\text{i}$)**: Each complete frame is divided into two temporally distinct half-frames called **fields**:
  - *Odd Field*: Scan lines $1, 3, 5, 7, \dots, 1079$.
  - *Even Field*: Scan lines $2, 4, 6, 8, \dots, 1080$.
  - The display alternates between odd and even fields at twice the frame rate (e.g., 60 fields/s for 30 fps video).

**2. Comparison Matrix (1.5 Marks):**

| Parameter | Progressive Scanning ($1080\text{p}$) | Interlaced Scanning ($1080\text{i}$) |
| :--- | :--- | :--- |
| **Scan Method** | Sequential full lines ($1$ to $H$) | Alternating odd and even line fields |
| **Temporal Sampling** | Full frame at time $t$ | Field 1 at $t$, Field 2 at $t + \Delta t$ |
| **Bandwidth** | Full spatial bandwidth | $50\%$ bandwidth savings per field |
| **Motion Artifacts** | None; sharp edges during motion | "Combing" / jagged serrated edges |
| **Modern Usage** | Native standard for LCD, OLED, CV | Legacy analog CRT broadcasting |

**3. Historical Rationale and Combing Artifacts (1.5 Marks):**
- *Historical Rationale*: Enabled analog television broadcasters (NTSC/PAL) to double the apparent flicker rate to $50/60\text{ Hz}$ (surpassing human CFF) while consuming only half the transmission bandwidth of a full progressive frame.
- *Combing / Feathering Artifacts*: Because odd and even fields are recorded at different moments in time (e.g., $1/60\text{ s}$ apart), fast-moving objects translate across the scene between fields. Displaying both fields simultaneously on modern progressive monitors produces jagged horizontal serrations along moving boundaries.

---

### Question 4 (Solved Numerical): A digital surveillance camera records video at a resolution of $1280 \times 720$ pixels, using 24-bit TrueColor RGB ($8\text{ bits/channel}$) at $30\text{ fps}$. (5 Marks)
**(a) Calculate the total frame count for a 20-second clip and determine the sensor resolution in Megapixels.**  
**(b) Calculate the uncompressed data rate in $\text{Mbit/s}$ and $\text{MB/s}$.**  
**(c) Determine the uncompressed storage required for a 2-hour recording in Gigabytes (GB).**

#### Model Solution:

**1. Part (a): Frame Count & Megapixels (1.5 Marks):**
- Total Frames:
  $$\text{Total Frames} = \text{Frame Rate} \times \text{Duration} = 30\text{ fps} \times 20\text{ s} = \mathbf{600\text{ frames}}$$
- Sensor Resolution in Megapixels:
  $$\text{Pixel Count} = W \times H = 1280 \times 720 = 921,600\text{ pixels}$$
  $$\text{Megapixels} = \frac{921,600}{10^6} = \mathbf{0.9216\text{ MP}}$$

**2. Part (b): Uncompressed Data Rate (2 Marks):**
- Formula:
  $$\text{Data Rate (bits/s)} = W \times H \times C \times b \times \text{FPS}$$
- Given: $W = 1280$, $H = 720$, $C = 3$ channels (RGB), $b = 8\text{ bits/channel}$, $\text{FPS} = 30$.
  $$\text{Data Rate} = 1280 \times 720 \times 3 \times 8 \times 30 = 663,552,000\text{ bits/s}$$
- Convert to $\text{Mbit/s}$:
  $$\text{Bitrate} = \frac{663,552,000}{10^6} = \mathbf{663.552\text{ Mbit/s}} \approx \mathbf{663.6\text{ Mbit/s}}$$
- Convert to $\text{MB/s}$ (Megabytes per second):
  $$\text{Storage Rate} = \frac{663,552,000}{8 \times 10^6} = \mathbf{82.944\text{ MB/s}} \approx \mathbf{82.9\text{ MB/s}}$$

**3. Part (c): 2-Hour Storage Capacity (1.5 Marks):**
- Duration in seconds: $2\text{ hours} = 2 \times 3600 = 7200\text{ seconds}$.
- Total Storage in MB:
  $$\text{Total Storage} = 82.944\text{ MB/s} \times 7200\text{ s} = 597,196.8\text{ MB}$$
- Convert to Gigabytes ($1\text{ GB} = 1000\text{ MB}$ or decimal metric GB):
  $$\text{Storage in GB} = \frac{597,196.8}{1000} = \mathbf{597.2\text{ GB}}$$
  *(Or in binary $\text{GiB}$: $\frac{597,196.8}{1024} = \mathbf{583.2\text{ GiB}}$).*

---

### Question 5: Explain the trichromatic theory of human color vision. Compare Additive (RGB) and Subtractive (CMYK) color models, and discuss why the YCbCr color model is preferred in video compression. (5 Marks)

#### Model Solution:

**1. Trichromatic Theory of Color Vision (1.5 Marks):**
- The human retina contains three types of cone photoreceptors, each tuned to different optical wavelength bands:
  - **L-Cones**: Long wavelengths (peak near Red $\approx 564\text{ nm}$).
  - **M-Cones**: Medium wavelengths (peak near Green $\approx 534\text{ nm}$).
  - **S-Cones**: Short wavelengths (peak near Blue $\approx 420\text{ nm}$).
- Any visible color stimulus is perceived as a linear combination of excitation responses across these three receptor channels.

**2. Additive vs. Subtractive Color Models (1.5 Marks):**
- **Additive Model (RGB)**:
  - Applicable to light-emitting systems (monitors, televisions, digital displays).
  - Starts with darkness (black) and creates colors by superimposing light of Red, Green, and Blue primary wavelengths. Adding all three produces white ($R+G+B = \text{White}$).
- **Subtractive Model (CMYK)**:
  - Applicable to reflective media (color printing, paints, dyes).
  - Cyan, Magenta, Yellow, and Key (Black) pigments subtract (absorb) specific reflected wavelengths from ambient white light.

**3. Why YCbCr is Preferred in Video Compression (2 Marks):**
1. **Channel Correlation**: In RGB, Red, Green, and Blue are highly cross-correlated; an illumination change alters all three channels simultaneously.
2. **Luminance-Chrominance Decoupling**: YCbCr decouples brightness ($Y$) from color difference ($Cb, Cr$):
   $$Y = 0.299 R + 0.587 G + 0.114 B$$
3. **Exploitation of Visual Acuity (Chroma Subsampling)**: The human eye has far higher spatial resolving power for luminance ($Y$) than for chrominance ($Cb, Cr$). This allows systems to heavily compress or subsample $Cb$ and $Cr$ (e.g., $4:2:0$) with zero perceived loss of visual sharpness.

---

### Question 6: What is Chroma Subsampling? Explain the $J:a:b$ notation and compare $4:4:4$, $4:2:2$, and $4:2:0$ subsampling in terms of pixel structure, bandwidth savings, and applications. (5 Marks)

#### Model Solution:

**1. Definition and Rationale (1 Mark):**
Chroma subsampling is a compression technique in which color-difference signals ($Cb, Cr$) are sampled at lower spatial resolutions than the luminance signal ($Y$). It exploits the human visual system's lower spatial sensitivity to high-frequency color variations.

**2. The $J:a:b$ Notation Explained (1 Mark):**
Based on a conceptual reference block $J$ pixels wide ($J = 4$) by $2$ scan lines high:
- **$J$ ($=4$)**: Horizontal reference width in luminance pixels.
- **$a$**: Number of chrominance samples ($Cb, Cr$) taken in the first row of $4$ pixels.
- **$b$**: Number of additional chrominance samples taken in the second row of $4$ pixels.

**3. Comparison of Schemes (3 Marks):**

| Scheme | Sampling Pattern (per $4 \times 2$ block) | Effective Bitrate ($8\text{-bit}$) | Bandwidth Savings | Common Applications |
| :--- | :--- | :--- | :--- | :--- |
| **$4:4:4$** | $8Y + 8Cb + 8Cr = 24\text{ samples}$ | $24\text{ bits/pixel}$ | $0\%$ (Reference) | High-end VFX, medical imaging, CGI |
| **$4:2:2$** | $8Y + 4Cb + 4Cr = 16\text{ samples}$ | $16\text{ bits/pixel}$ | $33.3\%$ reduction | Professional broadcast (ProRes, DVCPRO) |
| **$4:2:0$** | $8Y + 2Cb + 2Cr = 12\text{ samples}$ | $12\text{ bits/pixel}$ | **$50.0\%$ reduction** | Web streaming, H.264/HEVC, Blu-ray, YouTube |

- In $4:2:0$, chroma resolution is halved both horizontally and vertically, slashing total uncompressed video bandwidth by $50\%$ while preserving pristine perceptual sharpness.

---

### Question 7: Explain why image sensor photosites are inherently color-blind. Compare the Bayer Color Filter Array (CFA) with the 3-Sensor Dichroic Prism approach. Why does the Bayer pattern allocate $50\%$ of its filters to Green? (5 Marks)

#### Model Solution:

**1. The Color-Blind Sensor Dilemma (1.5 Marks):**
- Silicon photodetectors (photosites in CCD/CMOS arrays) operate purely via the photoelectric effect, accumulating electrical charges proportional to the total count of incoming photons regardless of wavelength.
- A raw photosite records only radiant intensity (grayscale amplitude) and cannot determine whether incoming photons are red, green, or blue.

**2. Bayer CFA Mosaic vs. 3-Sensor Dichroic Prism (2 Marks):**
- **Bayer CFA (Single Sensor Architecture)**:
  - A microscopic mosaic of color filters is fabricated directly over individual photosites: $50\%$ Green, $25\%$ Red, and $25\%$ Blue arranged in a repeating $2 \times 2$ checkerboard (`RG/GB`).
  - Each pixel records only one primary color; missing colors are reconstructed via **demosaicing** algorithms.
  - *Pros*: Low cost, compact, highly integrated (smartphones, DSLRs).
  - *Cons*: Demosaicing artifacts (false colors, moiré, edge blurring).
- **3-Sensor Dichroic Prism (Multi-Sensor Architecture)**:
  - An optical prism assembly splits incoming white light into separate Red, Green, and Blue wavelength bands directed onto three independent full-resolution sensors.
  - *Pros*: Full optical $4:4:4$ resolution; zero interpolation artifacts.
  - *Cons*: High manufacturing cost, large physical form factor, heavy weight (used in professional broadcast studio cameras).

**3. Rationale for $50\%$ Green Allocation (1.5 Marks):**
- The human eye's photopic spectral luminous efficiency curve peaks in the green spectrum (around $555\text{ nm}$).
- As reflected in the luminance equation ($Y = 0.299 R + 0.587 G + 0.114 B$), Green contributes nearly $59\%$ of perceived visual sharpness and brightness.
- Allocating twice as many photosites to Green maximizes perceived sharpness and luminance signal-to-noise ratio.

---

### Question 8 (Solved Numerical): (a) Derive the perspective projection equations for a pinhole camera model. (b) A traffic surveillance camera has a focal length of $f = 20\text{ mm}$. A vehicle of height $H = 1.5\text{ m}$ is located at a depth of $Z = 12\text{ m}$. Calculate the projected height of the vehicle on the sensor. (5 Marks)

#### Model Solution:

**1. Part (a): Mathematical Derivation (2.5 Marks):**
- Let the pinhole aperture be at the origin $(0, 0, 0)$ of the 3D camera coordinate system, with the optical axis along $+Z$.
- A real 3D point $\mathbf{P} = (X, Y, Z)^T$ projects onto the image plane at depth $Z = f$, yielding continuous image coordinates $(x, y)$.
- From the geometric property of **similar right triangles**:
  $$\frac{x}{f} = \frac{X}{Z} \implies \mathbf{x = f \frac{X}{Z}}$$
  $$\frac{y}{f} = \frac{Y}{Z} \implies \mathbf{y = f \frac{Y}{Z}}$$
- For an object of vertical height $H$ at depth $Z$, its projected height $h$ on the image plane satisfies:
  $$\frac{h}{f} = \frac{H}{Z} \implies \mathbf{h = \frac{f \cdot H}{Z}}$$

**2. Part (b): Step-by-Step Numerical Calculation (2.5 Marks):**
- **Given Parameters (converted to identical units: millimeters)**:
  - Real Height $H = 1.5\text{ m} = 1500\text{ mm}$
  - Depth Distance $Z = 12\text{ m} = 12000\text{ mm}$
  - Focal Length $f = 20\text{ mm}$
- **Compute Projected Height $h$**:
  $$h = \frac{f \cdot H}{Z} = \frac{20\text{ mm} \times 1500\text{ mm}}{12000\text{ mm}}$$
  $$h = \frac{30,000}{12,000} = \mathbf{2.5\text{ mm}}$$
- **Conclusion**: The $1.5\text{-meter}$ tall vehicle forms a projected image $2.5\text{ mm}$ high on the camera's physical sensor.

---

### Question 9: Why do practical cameras utilize glass lens assemblies instead of a simple pinhole aperture? Discuss the physical tradeoffs involved, explain radial lens distortion, and describe camera calibration. (5 Marks)

#### Model Solution:

**1. The Pinhole Dilemma & Need for Lenses (2 Marks):**
- A simple pinhole faces an irreconcilable physical tradeoff:
  - *Large pinhole*: Multiple light rays from a single point hit different areas of the sensor, resulting in severe geometric blur.
  - *Small pinhole*: Restricts incoming photon flux, producing extremely dark, noisy images requiring impractical exposure times.
  - *Infinitesimal pinhole*: Optical diffraction around the pinhole edges causes ray dispersion, blurring the image.
- *Solution*: Convex glass lenses gather light over a wide aperture and focus converging light rays onto a single focal plane according to the thin lens equation: $\frac{1}{f} = \frac{1}{d_o} + \frac{1}{d_i}$.

**2. Radial Lens Distortion (1.5 Marks):**
Real lens curvature bends off-axis light rays non-linearly, causing geometric distortion:
- **Barrel Distortion ($k_1 < 0$)**: Image magnification decreases with radial distance from the optical axis; straight lines bow outward like a barrel (common in wide-angle lenses).
- **Pincushion Distortion ($k_1 > 0$)**: Image magnification increases with distance; straight lines bow inward toward the center (common in telephoto lenses).

**3. Camera Calibration (1.5 Marks):**
- The computational process of estimating a camera's optical parameters using known geometric targets (e.g., planar checkerboards):
  - **Intrinsic Parameters**: Focal lengths ($f_x, f_y$), principal point ($c_x, c_y$), and radial/tangential distortion coefficients ($k_1, k_2, p_1, p_2$).
  - **Extrinsic Parameters**: 3D Rotation matrix ($\mathbf{R}$) and Translation vector ($\mathbf{T}$) relating the camera coordinate frame to the world frame.
  - Essential for accurate metric 3D reconstruction and augmented reality.

---

### Question 10: Differentiate between a video container and a video codec with appropriate industry examples. Explain why computer vision libraries like OpenCV depend on underlying OS codecs. (5 Marks)

#### Model Solution:

**1. Codec vs. Container Distinction (2.5 Marks):**
- **Video Codec (Compression Algorithm)**:
  - A software algorithm or hardware ASIC responsible for compressing raw video frames to minimize bitrate for storage/transmission, and decompressing them for display.
  - Employs lossy discrete cosine transforms (DCT), motion compensation, and entropy coding.
  - *Examples*: **H.264/AVC**, **H.265/HEVC**, **VP9**, **AV1**, **MJPEG**.
- **Video Container (File Wrapper)**:
  - An overarching binary file envelope that multiplexes the compressed video stream, audio tracks, subtitle streams, synchronization timecodes, and metadata into a single file.
  - *Examples*: **MP4** (`.mp4`), **Matroska** (`.mkv`), **AVI** (`.avi`), **QuickTime** (`.mov`).
  - *Analogy*: The container is an envelope; the codec is the language written on the letter inside.

**2. OpenCV Codec Dependency & FourCC (2.5 Marks):**
- OpenCV is primarily an image processing and computer vision library, not a dedicated media encoding framework.
- In OpenCV:
  - `cv2.VideoCapture` uses underlying OS media backends (such as FFmpeg on Linux, MSMF or DirectShow on Windows, AVFoundation on macOS) to demux containers and decode video frames into uncompressed BGR NumPy arrays.
  - `cv2.VideoWriter` requires a **FourCC** (four-character code, e.g., `'XVID'`, `'MP4V'`, `'avc1'`) to instruct the system's media engine which codec to invoke during encoding.
- If the host operating system lacks the specific decoder/encoder library, OpenCV cannot open or write the requested video format.
