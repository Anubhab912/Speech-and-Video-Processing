# 🎥 Module 3: Basics of Video Processing

Welcome to **Module 3: Basics of Video Processing** of the **Speech and Video Processing (CS30033)** course curriculum.

This module marks the transition from one-dimensional acoustic speech signals $s(t)$ and static two-dimensional images $I(x, y)$ to dynamic three-dimensional spatio-temporal video signals $V(x, y, t)$. It establishes the physical, mathematical, biological, and algorithmic foundations of digital video formation, human visual perception, color representations, camera optical models, and geometric motion modeling.

---

## 🗺️ Module 3 Learning Architecture

```mermaid
flowchart TD
    subgraph Chapter 8: Video Formation, Perception & Representation
        A1["🌍 3D World Scene"] --> A2["🔍 Lens Optics & Exposure (Aperture/Shutter)"]
        A2 --> A3["⚡ Image Sensor Array (CCD / CMOS Photosites)"]
        A3 --> A4["🎛️ Digitizer: Spatial Sampling & Temporal Quantization"]
        A4 --> A5["🎞️ Digital Video Frames V[x, y, t] (W × H × C at FPS)"]
        A5 --> A6["👁️ Human Visual Perception (Persistence of Vision & CFF)"]
        A5 --> A7["🎨 Color Systems (RGB, YCbCr, HSV) & Chroma Subsampling"]
        A2 --> A8["📐 Pinhole Camera Model & Perspective Projection"]
    end

    subgraph Chapter 9: Motion, Shape and Scene Modeling
        B1["🎞️ Consecutive Video Frames V(x, y, t)"] --> B2["🔍 4 Causes of Change (Object, Camera, Parallax, Illumination)"]
        B2 --> B3["📐 Coordinate Systems (World → Camera → Image → Pixel)"]
        B2 --> B4["📦 Shape Models (Point, Line, Bounding Box, Contour, Blob)"]
        B2 --> B5["🏙️ Scene Models (Static vs Dynamic, Surveillance, Drone)"]
        B1 --> B6["🪜 2D Motion Model Ladder (Translation → Rigid → Affine → Projective)"]
        B6 --> B7["🧮 Homogeneous Coordinates & Planar Homography"]
        B6 --> B8["🔄 3D Rigid Motion (6-DoF: Translation + Roll/Pitch/Yaw)"]
    end

    A5 --> B1
```

---

## 📂 Chapter Contents & Quick Links

| Chapter | Topic | Key Concepts | Notes & Practice Links |
| :--- | :--- | :--- | :---: |
| **Chapter 8** | **Fundamentals of Video Formation, Perception, and Representation** | 1D vs 2D vs 3D signals, Video formation pipeline, Persistence of vision, Temporal integration, Critical Flicker Fusion (CFF), Spatial resolution, FPS, Uncompressed data rate equation ($W \times H \times C \times b \times \text{FPS}$), Progressive ($1080\text{p}$) vs Interlaced ($1080\text{i}$) scanning, Containers vs Codecs, Trichromatic vision, RGB vs YCbCr vs HSV, Chroma subsampling ($4:4:4, 4:2:2, 4:2:0$), CCD vs CMOS, Bayer Filter CFA ($50\%\text{ G}, 25\%\text{ R}, 25\%\text{ B}$) & demosaicing, 3-sensor prism, Pinhole camera model derivation ($x = f X/Z, h = f H/Z$), Real lenses vs pinhole, Radial distortion, Camera calibration. | [Lecture Notes](Chapter_8_Video_Formation_Perception_Representation/README.md)<br>[Practice Q&A (10 Questions)](Chapter_8_Video_Formation_Perception_Representation/practice_questions.md) |
| **Chapter 9** | **Motion, Shape and Scene Modeling in Computer Vision** | Objectives of motion analysis, 4 causes of inter-frame changes (object, camera, parallax, illumination), Camera motions (Pan/Yaw, Tilt/Pitch, Roll, Dolly, Truck, Zoom), Depth and motion parallax ($v_x = -f V_X / Z$), Coordinate systems (World $\to$ Camera $\to$ Image $\to$ Pixel), Shape models (Point, Line, Bounding box, Contour, Blob, Surface patch), Scene models (Static vs Dynamic, Surveillance, Drone), 2D Motion Model Ladder (Translation, Euclidean, Similarity, Affine, Projective/Homography), Homogeneous coordinates ($[x, y, 1]^T$), Planar homography matrix & non-linear mapping, 3D Rigid Motion (6-DoF: 3 translations + Roll/Pitch/Yaw), Model selection principles. | [Lecture Notes](Chapter_9_Motion_Shape_and_Scene_Modeling/README.md)<br>[Practice Q&A (10 Questions)](Chapter_9_Motion_Shape_and_Scene_Modeling/practice_questions.md) |

---

## 🎯 Syllabus Learning Outcomes (Module 3)
Upon completing this module, students will master:
1. **Physical & Mathematical Video Formation**: Formulating digital video as a 3D spatio-temporal tensor $V(x, y, t)$, calculating raw uncompressed bitrates, and deriving perspective projection geometry.
2. **Biological Perception Engineering**: Understanding how human visual temporal integration, persistence of vision, and Critical Flicker Fusion govern frame rate selection and eliminate perceived flicker.
3. **Color Video & Perceptual Compression**: Exploiting human retinal sensitivity to decouple luminance ($Y$) from chrominance ($Cb, Cr$), applying chroma subsampling ($4:2:0$), and utilizing the HSV color space for lighting-invariant visual tracking.
4. **Sensor Optics & Demosaicing**: Analyzing Bayer color filter mosaics, color demosaicing interpolation, 3-sensor dichroic prism optics, and radial lens aberrations.
5. **Geometric Motion Modeling**: Distinguishing optical zoom from translational camera dolly, modeling motion parallax gradients, navigating the 2D Motion Model Ladder (from 2-DoF translation to 8-DoF projective homography), and applying 6-DoF 3D rigid body transformations.
