# Chapter 9: Exam Practice Questions & Model Solutions

> **Course**: Speech and Video Processing (CS30033)  
> **Topic**: Motion, Shape and Scene Modeling in Computer Vision  
> **Grading Format**: Standard University 5-Mark Questions with Step-by-Step Marking Schemes

---

### Question 1: Explain the four primary causes of inter-frame change in video sequences. Provide a distinct real-world scenario for each cause and explain why pixel differences do not always imply physical motion. (5 Marks)

#### Model Solution:

**1. The Four Causes of Inter-Frame Changes (4 Marks - 1 Mark Each):**
1. **Object Motion**:
   - *Description*: The camera remains stationary, while independent physical objects move within the field of view.
   - *Example*: A fixed traffic CCTV camera observing a vehicle moving across a street intersection.
2. **Camera Motion (Egomotion)**:
   - *Description*: Objects in the environment remain stationary, but the camera platform translates or rotates in 3D space.
   - *Example*: A tourist walking around a historical statue while recording video on a smartphone.
3. **Depth Variation & Motion Parallax**:
   - *Description*: Objects situated at different distances from the camera shift by different pixel displacements during camera translation.
   - *Example*: A moving car dashcam: roadside trees at $5\text{ m}$ rush past rapidly, whereas distant hills at $500\text{ m}$ barely appear to move.
4. **Illumination and Appearance Changes**:
   - *Description*: Variations in scene lighting, shadows, reflections, or surface orientation alter pixel intensities without physical spatial displacement.
   - *Example*: The sun emerging from behind dense clouds, or a pedestrian moving from bright sunlight into building shade.

**2. Why Pixel Differences Do Not Always Imply Motion (1 Mark):**
Pixel differences between frames measure changes in radiant light intensity received by sensor photosites. Changes in ambient illumination, flickering fluorescent lights, or cast shadows alter pixel values drastically even when every physical object and the camera are completely stationary, thereby violating the **Brightness Constancy Assumption**.

---

### Question 2: Classify camera motions into rotational, translational, and optical focal variations. Contrast camera Dolly motion with optical Zoom motion and explain why only one produces motion parallax. (5 Marks)

#### Model Solution:

**1. Classification of Camera Motions (2 Marks):**
- **Rotational Motions (Zero-Baseline Movements)**:
  - *Pan (Yaw)*: Horizontal rotation left or right around the vertical axis.
  - *Tilt (Pitch)*: Vertical rotation up or down around the transverse horizontal axis.
  - *Roll*: In-plane rotation around the longitudinal optical axis.
- **Translational Motions (Non-Zero-Baseline Movements)**:
  - *Dolly*: Physical translation forward or backward along the optical axis ($Z$).
  - *Truck / Track*: Physical translation horizontally left or right ($X$).
  - *Pedestal / Boom*: Physical translation vertically up or down ($Y$).
- **Focal Variation (Internal Optical Adjustment)**:
  - *Zoom*: Mechanical alteration of lens focal length ($f$) without physical camera displacement.

**2. Dolly vs. Zoom Parallax Comparison (3 Marks):**

| Criterion | Camera Dolly Motion | Optical Zoom Motion |
| :--- | :--- | :--- |
| **Physical Mechanism** | Camera physically translates along optical axis ($T_Z \neq 0$). | Camera stays stationary; internal lens elements alter $f$. |
| **Optical Center Position** | Optical center shifts in 3D world space. | Optical center remains completely fixed. |
| **Parallax Generation** | **Strong Parallax**: Near objects expand much faster than distant objects because $\Delta Z / Z$ is larger for near objects. | **Zero Parallax**: All image points scale by the identical uniform factor ($f_{\text{new}} / f_{\text{old}}$) regardless of depth. |
| **Perspective Distortion** | Perspective changes dynamically (basis of the Hitchcock "Vertigo" dolly-zoom effect). | Perspective remains completely unchanged; creates flat telephoto flattening. |

---

### Question 3: Explain the concept of motion parallax. Derive the mathematical relationship between a translating camera's velocity and the apparent optical velocity of an observed 3D object. (5 Marks)

#### Model Solution:

**1. Concept of Motion Parallax (1.5 Marks):**
Motion parallax is the apparent difference in velocity and displacement of objects located at different depths in a 3D scene when the camera platform undergoes physical translation. Closer objects appear to sweep across the field of view rapidly, while distant objects appear nearly static.

**2. Mathematical Derivation (2.5 Marks):**
- Consider a camera translating horizontally along its $X$-axis with linear velocity $V_X = \frac{dX}{dt}$.
- Let a static 3D world point have camera coordinates $\mathbf{P} = (X, Y, Z)^T$, where $Z$ is the physical depth distance from the camera optical center.
- According to the pinhole perspective projection model, the 2D projected image coordinate $x$ is:
  $$x = f \frac{X}{Z}$$
- Differentiating $x$ with respect to time $t$ using the chain rule (since $Z$ is constant for purely horizontal translation $\frac{dZ}{dt} = 0$):
  $$v_x = \frac{dx}{dt} = \frac{d}{dt}\left(f \frac{X}{Z}\right) = \frac{f}{Z} \frac{dX}{dt}$$
- Because camera motion is opposite to apparent object displacement in camera coordinates ($\frac{dX}{dt} = -V_X$):
  $$\mathbf{v_x = - f \frac{V_X}{Z}}$$

**3. Physical Conclusion (1 Mark):**
Apparent image velocity $v_x$ is **inversely proportional to depth $Z$**. An object at depth $Z = 5\text{ m}$ produces ten times greater optical flow velocity on the image plane than an object at $Z = 50\text{ m}$, providing the foundational depth cue for biological vision and Structure from Motion (SfM) algorithms.

---

### Question 4: Explain the four coordinate systems in video geometry: World, Camera, Image Plane, and Pixel Array coordinates. Provide the mathematical mapping equations between them. (5 Marks)

#### Model Solution:

**1. The Four Coordinate Frames (2 Marks):**
1. **World Coordinates ($X_W, Y_W, Z_W$)**: Fixed global 3D metric reference frame representing the physical environment.
2. **Camera Coordinates ($X_C, Y_C, Z_C$)**: 3D Cartesian frame with its origin at the camera's optical center $\mathbf{O}$, with $+Z_C$ pointing along the optical axis.
3. **Continuous Image Plane Coordinates ($x, y$)**: 2D physical metric coordinates on the sensor plane at focal distance $f$, centered on the principal point.
4. **Discrete Pixel Array Coordinates ($u, v$)**: 2D discrete integer row-column indices of the digital image array, with origin $(0, 0)$ at the top-left corner.

**2. Mathematical Mapping Transformations (3 Marks):**
1. **World to Camera Frame (Extrinsic Transformation)**:
   $$\begin{bmatrix} X_C \\ Y_C \\ Z_C \end{bmatrix} = \mathbf{R} \begin{bmatrix} X_W \\ Y_W \\ Z_W \end{bmatrix} + \mathbf{T}$$
   *(where $\mathbf{R}$ is the $3 \times 3$ rotation matrix and $\mathbf{T}$ is the $3 \times 1$ translation vector).*
2. **Camera to Image Plane (Perspective Projection)**:
   $$x = f \frac{X_C}{Z_C}, \quad y = f \frac{Y_C}{Z_C}$$
3. **Image Plane to Pixel Coordinates (Digitization & Principal Point Offset)**:
   $$u = \frac{x}{p_x} + c_x = f_x \frac{X_C}{Z_C} + c_x$$
   $$v = \frac{y}{p_y} + c_y = f_y \frac{Y_C}{Z_C} + c_y$$
   *(where $p_x, p_y$ are physical pixel widths, $f_x, f_y$ are focal lengths in pixel units, and $(c_x, c_y)$ is the principal point in pixel coordinates).*

---

### Question 5: Compare Point, Line, Bounding Box, Contour, Blob, and Surface Patch shape models in terms of degrees of freedom, computational complexity, robustness to non-rigid deformation, and practical computer vision applications. (5 Marks)

#### Model Solution:

**1. Overview of Shape Models (1 Mark):**
Shape models are mathematical representations used in computer vision to describe the boundary, geometry, and spatial extent of objects in video frames for tracking, detection, and segmentation.

**2. Comprehensive Comparison Matrix (4 Marks):**

| Shape Model | Representation | Degrees of Freedom (DoF) | Computational Cost | Deformation Robustness | Typical Application |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Point Model** | Centroid $(x, y)$ | $2$ (Position) | Negligible | None (ignores shape) | Distant aircraft tracking, corner feature tracking (KLT). |
| **Line Model** | Line parameters $(\rho, \theta)$ | $2$ to $4$ | Low | Low (rigid straight edges) | Road lane tracking, structural edge detection. |
| **Bounding Box** | Box $[x, y, w, h]$ | $4$ (Position + Size) | Low | Moderate | Real-time object detection (YOLO, SSD, Faster R-CNN). |
| **Contour Model** | Parameterized curve / snake | High ($2N$ control points) | High | Very High (non-rigid) | Articulated human tracking, medical organ segmentation. |
| **Blob / Region** | Connected component mask | Variable (Area, Centroid) | Moderate | High | Foreground tracking in surveillance via background subtraction. |
| **Surface Patch** | Planar or 3D mesh | $6$ to $8$ (Affine/Homography) | Moderate to High | Moderate (planar assumption) | Optical flow template matching, AR marker tracking. |

---

### Question 6: Differentiate between Static and Dynamic scenes. Discuss the video analysis challenges associated with fixed surveillance cameras, handheld devices, and aerial drone platforms. (5 Marks)

#### Model Solution:

**1. Static vs. Dynamic Scenes (2 Marks):**
- **Static Scene**: The background environment and all constituent objects remain completely stationary. If the camera is also stationary, consecutive frames are identical up to sensor noise. Changes occur only due to ambient illumination shifts.
- **Dynamic Scene**: The scene contains independent moving foreground entities (pedestrians, vehicles, animals). Consecutive video frames exhibit optical flow and spatial boundary shifts over time.

**2. Video Processing Challenges Across Platforms (3 Marks):**
1. **Fixed Surveillance Camera (1 Mark)**:
   - Camera platform is immobile ($\mathbf{R} = \mathbf{I}, \mathbf{T} = \mathbf{0}$).
   - *Challenge*: Foreground segmentation is straightforward using Background Subtraction (GMM), but algorithms must handle illumination changes, moving tree branches, dynamic shadows, and object camouflage.
2. **Handheld / Wearable Camera (1 Mark)**:
   - Camera experiences rapid, erratic 3D rotations, platform translations, and high-frequency shakes concurrently with independent object movement.
   - *Challenge*: Background subtraction fails because the entire background moves. Requires digital video stabilization, feature matching (SIFT/ORB), and egomotion compensation.
3. **Aerial Drone Platform (1 Mark)**:
   - High-altitude camera undergoes continuous 3D translation, altitude changes, and perspective pitch.
   - *Challenge*: Objects appear very small (low resolution); large global homography transformations must be computed to separate tiny moving targets from ground motion.

---

### Question 7: Detail the 2D Motion Model Ladder from Translation to Projective transformation. Construct a comparison table specifying the degrees of freedom (DoF), transformation matrices, and geometric invariants preserved for each model. (5 Marks)

#### Model Solution:

**1. The 2D Motion Model Ladder Concept (1 Mark):**
The 2D Motion Model Ladder categorizes planar image transformations in order of increasing geometric complexity and expressiveness, allowing algorithms to choose the simplest model that explains the observed frame-to-frame change.

**2. Comparison Table of the 2D Motion Ladder (4 Marks):**

| Transformation Model | DoF | Homogeneous Matrix Formulation | Geometric Invariants Preserved | Practical Computer Vision Usage |
| :--- | :--- | :--- | :--- | :--- |
| **Translation** | $2$ | $\begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix}$ | Lengths, angles, areas, orientations | Block matching in video compression (MPEG, H.264). |
| **Euclidean (Rigid)** | $3$ | $\begin{bmatrix} \cos\theta & -\sin\theta & t_x \\ \sin\theta & \cos\theta & t_y \\ 0 & 0 & 1 \end{bmatrix}$ | Distances between points, angles, areas | Tracking planar objects rotated on a flat surface. |
| **Similarity** | $4$ | $\begin{bmatrix} s\cos\theta & -s\sin\theta & t_x \\ s\sin\theta & s\cos\theta & t_y \\ 0 & 0 & 1 \end{bmatrix}$ | Angles, ratios of lengths, shape | Tracking objects with camera zoom or altitude variation. |
| **Affine** | $6$ | $\begin{bmatrix} a_1 & a_2 & a_3 \\ a_4 & a_5 & a_6 \\ 0 & 0 & 1 \end{bmatrix}$ | Parallelism of lines, ratios of parallel line segments | Tracking planar surface patches under mild viewpoint slant. |
| **Projective (Homography)** | $8$ | $\begin{bmatrix} h_{11} & h_{12} & h_{13} \\ h_{21} & h_{22} & h_{23} \\ h_{31} & h_{32} & h_{33} \end{bmatrix}$ | Straight lines, cross-ratio of 4 collinear points | Panorama stitching, document scanning, AR markers. |

---

### Question 8: Explain the necessity and concept of Homogeneous Coordinates in computer vision. Show how homogeneous coordinates unify translation, rotation, scaling, and projective transformations into standard matrix multiplications. (5 Marks)

#### Model Solution:

**1. The Problem with Standard Cartesian Coordinates (1.5 Marks):**
In standard 2D Cartesian coordinates, affine transformations require a hybrid mathematical structure:
$$\begin{bmatrix} x' \\ y' \end{bmatrix} = \mathbf{A} \begin{bmatrix} x \\ y \end{bmatrix} + \mathbf{t}$$
- Rotation and scaling are represented by $2 \times 2$ matrix multiplication ($\mathbf{A}$), whereas translation is an additive vector operation ($\mathbf{t}$).
- Because translation is not a linear operation in 2D Cartesian space, multiple sequential transformations cannot be combined into a single matrix multiplication.

**2. Homogeneous Coordinate Formulation (1.5 Marks):**
Homogeneous coordinates lift 2D Cartesian points into a 3D projective space by appending a third coordinate (scale factor):
$$\mathbf{p} = \begin{bmatrix} x \\ y \end{bmatrix} \quad \Longrightarrow \quad \mathbf{\tilde{p}} = \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$$
To recover 2D Cartesian coordinates from a general homogeneous vector $[\tilde{x}, \tilde{y}, w]^T$:
$$x = \frac{\tilde{x}}{w}, \quad y = \frac{\tilde{y}}{w}$$

**3. Unified Matrix Representation (2 Marks):**
With homogeneous coordinates, every 2D transformation becomes a single $3 \times 3$ matrix multiplication $\mathbf{\tilde{p}}' = \mathbf{H} \mathbf{\tilde{p}}$:
- **Translation ($2\text{ DoF}$)**: $\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$
- **Rotation ($1\text{ DoF}$)**: $\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$
- **Affine ($6\text{ DoF}$)**: $\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} a_1 & a_2 & a_3 \\ a_4 & a_5 & a_6 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$
- **Benefit**: A chain of $N$ transformations $\mathbf{H}_1, \mathbf{H}_2, \dots, \mathbf{H}_N$ collapses into a single composite matrix $\mathbf{H} = \mathbf{H}_N \cdots \mathbf{H}_1$, enabling high-performance GPU execution and direct OpenCV implementation (`cv2.warpAffine`, `cv2.warpPerspective`).

---

### Question 9: Define Planar Homography (Projective Mapping). State its non-linear Cartesian equations, determine the minimum number of point correspondences needed to compute it, and explain its applications. (5 Marks)

#### Model Solution:

**1. Definition of Planar Homography (1.5 Marks):**
A planar homography is an invertible projective mapping between two 2D planes (such as a planar world surface and the camera sensor plane, or between two camera views of a planar scene taken from different viewpoints):
$$\begin{bmatrix} \tilde{x}' \\ \tilde{y}' \\ \tilde{w}' \end{bmatrix} = \begin{bmatrix} h_{11} & h_{12} & h_{13} \\ h_{21} & h_{22} & h_{23} \\ h_{31} & h_{32} & h_{33} \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$$
Dividing by the homogeneous scale factor $w' = h_{31} x + h_{32} y + h_{33}$ yields the non-linear Cartesian mapping:
$$\mathbf{x' = \frac{h_{11} x + h_{12} y + h_{13}}{h_{31} x + h_{32} y + h_{33}}}, \quad \mathbf{y' = \frac{h_{21} x + h_{22} y + h_{23}}{h_{31} x + h_{32} y + h_{33}}}$$

**2. Degrees of Freedom & Point Correspondences (1.5 Marks):**
- Matrix $\mathbf{H}$ has $9$ coefficients, but it is defined up to an arbitrary scale factor $\lambda \neq 0$ (multiplying all elements by $\lambda$ cancels out in the fractions for $x'$ and $y'$).
- Hence, $\mathbf{H}$ has **$8$ independent Degrees of Freedom**.
- Each point correspondence $(x_i, y_i) \leftrightarrow (x'_i, y'_i)$ supplies $2$ independent constraint equations.
- Therefore, a minimum of **$4$ non-collinear point correspondences** ($4 \times 2 = 8$ equations) are required to solve $\mathbf{H}$ uniquely using the Direct Linear Transformation (DLT) algorithm.

**3. Practical Computer Vision Applications (2 Marks):**
1. **Document Rectification (Mobile Scanning Apps)**: Correcting perspective keystoning in photographs of receipts, whiteboards, or documents to produce an upright front-parallel image.
2. **Panorama / Mosaic Stitching**: Stitching photos captured by rotating a camera around its optical center.
3. **Augmented Reality (AR)**: Superimposing virtual planar graphics (e.g., virtual billboards on soccer fields) accurately aligned with perspective lines.

---

### Question 10 (Solved Numerical): In a video sequence, the 2D motion of an object across consecutive frames is described by the affine transformation: (5 Marks)
$$x' = 1.2 x + 15$$
$$y' = 0.8 y - 10$$
**(a) If a point on the object has coordinates $(x, y) = (50, 25)$ in the first frame, calculate its transformed coordinates $(x', y')$ in the next frame.**  
**(b) Determine the exact directional displacement (shift) of the point.**  
**(c) Explain what the scaling coefficients $1.2$ and $0.8$ indicate regarding the object's physical motion, shape change, and aspect ratio.**

#### Model Solution:

**1. Part (a): Coordinate Transformation Calculation (2 Marks):**
- Given:
  $$x = 50, \quad y = 25$$
- Substitute into the transformation equations:
  $$x' = (1.2 \times 50) + 15 = 60 + 15 = \mathbf{75\text{ pixels}}$$
  $$y' = (0.8 \times 25) - 10 = 20 - 10 = \mathbf{10\text{ pixels}}$$
- **Resulting Coordinates**: The point $(50, 25)$ moves to $(x', y') = \mathbf{(75, 10)}$.

**2. Part (b): Directional Displacement / Shift (1.5 Marks):**
- **Horizontal Shift ($\Delta x$)**:
  $$\Delta x = x' - x = 75 - 50 = \mathbf{+25\text{ pixels}} \quad (\text{Shifted } 25\text{ pixels to the right})$$
- **Vertical Shift ($\Delta y$)**:
  $$\Delta y = y' - y = 10 - 25 = \mathbf{-15\text{ pixels}} \quad (\text{Shifted } 15\text{ pixels upward})$$
- **Net Translation**: The point translates $25$ pixels rightward and $15$ pixels upward in the image coordinate frame.

**3. Part (c): Physical and Geometric Interpretation (1.5 Marks):**
- **Horizontal Scaling Factor ($s_x = 1.2$)**: Because $s_x = 1.2 > 1.0$, the object expands or stretches horizontally by $20\%$.
- **Vertical Scaling Factor ($s_y = 0.8$)**: Because $s_y = 0.8 < 1.0$, the object contracts or compresses vertically by $20\%$.
- **Shape / Aspect Ratio Deformation**: The transformation is non-isotropic ($s_x \neq s_y$), indicating non-uniform stretching/shearing that alters the object's aspect ratio (e.g., turning a square into a wide rectangle), which could indicate non-rigid object deformation or out-of-plane rotation around the vertical axis.
