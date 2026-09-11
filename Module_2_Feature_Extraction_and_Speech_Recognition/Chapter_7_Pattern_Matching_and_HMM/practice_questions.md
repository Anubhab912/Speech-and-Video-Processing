# Chapter 7: Exam Practice Questions & Solved Numericals

> **Course**: Speech and Video Processing (CS30033)  
> **Topic**: Pattern Matching and HMM-based Speech Recognition  
> **Grading Format**: Standard University 5-Mark Questions with Complete Step-by-Step Solutions

---

### Question 1: Explain the three fundamental problems of Hidden Markov Models (HMMs) and the algorithms used to solve them. (5 Marks)

#### Model Solution:
**1. Problem 1: Evaluation (1.5 Marks)**
- **Objective**: Given model $\lambda = (A, B, \pi)$ and an observation sequence $O = (O_1, O_2, \dots, O_T)$, compute total likelihood $P(O \mid \lambda)$.
- **Algorithm**: **Forward-Backward Algorithm**. Uses dynamic programming to sum across all possible state trajectories in $O(N^2 T)$ operations.

**2. Problem 2: Decoding (1.5 Marks)**
- **Objective**: Given model $\lambda$ and observation sequence $O$, find the single most likely hidden state sequence $Q^* = (q_1^*, q_2^*, \dots, q_T^*)$.
- **Algorithm**: **Viterbi Algorithm**. Uses max-product dynamic programming and path backtracking.

**3. Problem 3: Learning / Training (2 Marks)**
- **Objective**: Given training observation sequences, optimize model parameters $\lambda = (A, B, \pi)$ to maximize $P(O \mid \lambda)$.
- **Algorithm**: **Baum-Welch (Expectation-Maximization) Algorithm**. Iteratively estimates state occupancies ($\gamma_t, \xi_t$) and updates $\bar{\pi}, \bar{A}, \bar{B}$ until convergence.

---

### Question 2 (Solved Problem): Given a two-state HMM with hidden states $S_1$ and $S_2$, initial state vector $\pi = [0.7, 0.3]$, and state transition matrix $A = \begin{bmatrix} 0.6 & 0.4 \\ 0.2 & 0.8 \end{bmatrix}$, calculate the total probability $P(X \mid \lambda)$ of generating observation sequence $X = (x_1, x_2)$ using the Forward Algorithm. Emission probabilities: $b_1(x_1) = 0.4, b_2(x_1) = 0.3$, and $b_1(x_2) = 0.5, b_2(x_2) = 0.7$. (5 Marks)

#### Solution:

**1. Given Model Parameters (1 Mark):**
- $\pi_1 = 0.7, \quad \pi_2 = 0.3$
- $a_{11} = 0.6, \quad a_{12} = 0.4, \quad a_{21} = 0.2, \quad a_{22} = 0.8$
- $b_1(x_1) = 0.4, \quad b_2(x_1) = 0.3$
- $b_1(x_2) = 0.5, \quad b_2(x_2) = 0.7$

**2. Step 1: Initialization at $t = 1$ (1.5 Marks):**
$$\alpha_1(i) = \pi_i \cdot b_i(x_1)$$
- $\alpha_1(1) = \pi_1 \cdot b_1(x_1) = 0.7 \times 0.4 = \mathbf{0.28}$
- $\alpha_1(2) = \pi_2 \cdot b_2(x_1) = 0.3 \times 0.3 = \mathbf{0.09}$

**3. Step 2: Induction / Recursion at $t = 2$ (1.5 Marks):**
$$\alpha_2(j) = \left[ \sum_{i=1}^2 \alpha_1(i) a_{ij} \right] b_j(x_2)$$
- **For State $S_1$ ($j = 1$):**
  $$\alpha_2(1) = [\alpha_1(1) a_{11} + \alpha_1(2) a_{21}] \cdot b_1(x_2) = [(0.28 \times 0.6) + (0.09 \times 0.2)] \times 0.5$$
  $$\alpha_2(1) = [0.168 + 0.018] \times 0.5 = 0.186 \times 0.5 = \mathbf{0.093}$$
- **For State $S_2$ ($j = 2$):**
  $$\alpha_2(2) = [\alpha_1(1) a_{12} + \alpha_1(2) a_{22}] \cdot b_2(x_2) = [(0.28 \times 0.4) + (0.09 \times 0.8)] \times 0.7$$
  $$\alpha_2(2) = [0.112 + 0.072] \times 0.7 = 0.184 \times 0.7 = \mathbf{0.1288}$$

**4. Step 3: Termination & Total Likelihood (1 Mark):**
$$P(X \mid \lambda) = \alpha_2(1) + \alpha_2(2) = 0.093 + 0.1288 = \mathbf{0.2218}$$

$$\mathbf{P(X \mid \lambda) = 0.2218 \quad (22.18\%)}$$

---

### Question 3 (Solved Problem): For the two-state HMM specified in Question 2, use the Viterbi Algorithm to determine the single optimal hidden state path $Q^* = (q_1^*, q_2^*)$ that generates observation sequence $X = (x_1, x_2)$ and find its path probability. (5 Marks)

#### Solution:

**1. Step 1: Initialization at $t = 1$ (1.5 Marks):**
$$v_1(i) = \pi_i \cdot b_i(x_1), \quad \psi_1(i) = 0$$
- $v_1(1) = \pi_1 \cdot b_1(x_1) = 0.7 \times 0.4 = \mathbf{0.28}, \quad \psi_1(1) = 0$
- $v_1(2) = \pi_2 \cdot b_2(x_1) = 0.3 \times 0.3 = \mathbf{0.09}, \quad \psi_1(2) = 0$

**2. Step 2: Recursion at $t = 2$ (2 Marks):**
$$v_2(j) = \max_{i \in \{1, 2\}} [v_1(i) a_{ij}] \cdot b_j(x_2), \quad \psi_2(j) = \arg\max_{i \in \{1, 2\}} [v_1(i) a_{ij}]$$

- **For State $S_1$ ($j = 1$):**
  - Candidate from $S_1$: $v_1(1) a_{11} = 0.28 \times 0.6 = \mathbf{0.168}$
  - Candidate from $S_2$: $v_1(2) a_{21} = 0.09 \times 0.2 = \mathbf{0.018}$
  - Maximum $= \max(0.168, 0.018) = 0.168$ from State $S_1$ ($\psi_2(1) = 1$).
  $$v_2(1) = 0.168 \times b_1(x_2) = 0.168 \times 0.5 = \mathbf{0.084}$$

- **For State $S_2$ ($j = 2$):**
  - Candidate from $S_1$: $v_1(1) a_{12} = 0.28 \times 0.4 = \mathbf{0.112}$
  - Candidate from $S_2$: $v_1(2) a_{22} = 0.09 \times 0.8 = \mathbf{0.072}$
  - Maximum $= \max(0.112, 0.072) = 0.112$ from State $S_1$ ($\psi_2(2) = 1$).
  $$v_2(2) = 0.112 \times b_2(x_2) = 0.112 \times 0.7 = \mathbf{0.0784}$$

**3. Step 3: Termination and Path Backtracking (1.5 Marks):**
- **Optimal Final State $q_2^*$**:
  $$P^* = \max[v_2(1), v_2(2)] = \max(0.084, 0.0784) = \mathbf{0.084}$$
  $$q_2^* = \arg\max[v_2(1), v_2(2)] = \mathbf{S_1}$$
- **Backtracking $q_1^*$**:
  $$q_1^* = \psi_2(q_2^*) = \psi_2(1) = \mathbf{S_1}$$

**Final Conclusion:**
- **Optimal State Path**: $\mathbf{Q^* = (S_1, S_1)}$
- **Best Path Probability**: $\mathbf{P^* = 0.084 \quad (8.4\%)}$
