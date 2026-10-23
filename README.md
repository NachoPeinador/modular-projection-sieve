# Algebraic Theory of Modular Projection Sieving

### Prime-Coprime Entanglement, Asymmetric Activation Thresholds, and Formal Verification in Lean 4

[![Lean 4 Certified](https://img.shields.io/badge/Lean_4-19_Modules_Certified-purple?style=flat&logo=lean&logoColor=white)](https://colab.research.google.com/github/NachoPeinador/modular-projection-sieve/blob/main/Notebooks/Lean4_Theory_of_Modular_Projection_Sieving.ipynb)
[![Mathlib4](https://img.shields.io/badge/Mathlib4-v4.35.0-blue?style=flat)](https://github.com/leanprover-community/mathlib4)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/NachoPeinador/modular-projection-sieve/blob/main/Notebooks/ATM_Experimental_Suite.ipynb)
[![DOI: 10.5281/zenodo.22043293](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.22043293-blue.svg)](https://doi.org/10.5281/zenodo.22043293)
[![ORCID](https://img.shields.io/badge/ORCID-0009--0008--1822--3452-A6CE39?style=flat&logo=orcid&logoColor=white)](https://orcid.org/0009-0008-1822-3452)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat)](https://opensource.org/licenses/MIT)
[![Papers](https://img.shields.io/badge/Paper-Read_PDF-B31B1B?style=flat&logo=latex&logoColor=white)](https://github.com/NachoPeinador/modular-projection-sieve/blob/main/Papers/ATMPS.pdf)

---

## 🔬 Scientific Overview

This repository hosts the official research archive, formal verification library, and computational benchmarks for the paper:

> **Algebraic Theory of Modular Projection Sieving: Prime-Coprime Entanglement and Asymmetric Activation Thresholds** 
> *Author:* José Ignacio Peinador Sala (Independent Researcher, Valladolid, Spain)
> *Target Journal:* **Mathematics of Computation** (American Mathematical Society)
> *AMS Submission Identifier:* `261023-PeinadorSala` (Submitted: October 23, 2026)  
> *Permanent DOI Archive:* [10.5281/zenodo.22043293](https://doi.org/10.5281/zenodo.22043293)

The manuscript develops an algebraic theory of modular projection sieving over the unit group $(\mathbb{Z}/6\mathbb{Z})^\times = \lbrace 1, 5 \rbrace$, defining the dual active channels:

$$\mathcal{C}_1 = \lbrace 6k+1 \rbrace_{k \ge 1}, \qquad \mathcal{C}_5 = \lbrace 6k-1 \rbrace_{k \ge 1}.$$

While classical wheel sieves apply a single symmetric activation boundary $\kappa_{\min}(p) = (p^2-1)/6$ across all residue classes, this work establishes that this boundary is suboptimal for channel $\mathcal{C}_5$[cite: 1]. The correct threshold is strictly delayed, deterministic, and dictated by a canonical chiral pairing across opposite channels designated **prime-coprime entanglement**.

---

## 📐 Mathematical Core & Key Theoretical Results

### 1. Explicit Asymmetric Activation Thresholds ($\kappa_{\min}^\pm$)
For every base prime $p = 6k_p + \varepsilon_p > 3$ with $\varepsilon_p \in \lbrace -1, +1 \rbrace$, we formalize the **positional coprime** $\mathrm{Cop}(p)$ as the minimal prime $q = 6k_q - \varepsilon_p$ in the opposite channel satisfying:

$$k_q \ge \begin{cases} k_p, & \text{if } \varepsilon_p = -1 \ (p \in \mathcal{C}_5), \\ k_p + 1, & \text{if } \varepsilon_p = +1 \ (p \in \mathcal{C}_1). \end{cases}$$

Setting $\mathrm{NextKop}(p) = k_q$, the exact activation boundaries in the two channels are:

$$\kappa_{\min}^+(p) = p k_p + \varepsilon_p k_p \quad (\mathcal{C}_1), \qquad \kappa_{\min}^-(p) = p\,\mathrm{NextKop}(p) - \varepsilon_p k_p \quad (\mathcal{C}_5).$$

- **Strict Threshold Domination (Theorem 2.9):** For every base prime $p > 3$, the inequality $\kappa_{\min}^-(p) > \kappa_{\min}^+(p)$ holds strictly, with equality if and only if $p \in \mathcal{C}_5$ and $k_q = k_p$, in which case $\lbrace p, \mathrm{Cop}(p) \rbrace$ forms a twin-prime pair.

### 2. Twin Primes as the Entanglement Ground State
- **Quadratic Annihilator (Theorem 3.2):** An index $k \in \mathbb{N}^+$ generates a twin-prime pair $(6k-1, 6k+1)$ if and only if:

  $$k^2 - k_p^2 \not\equiv 0 \pmod{p} \qquad \forall p \in \mathcal{P}_{>3}, \ p \le \sqrt{6k+1}.$$

- **Local Ground State (Proposition 3.3):** The entanglement jump $\Delta k(p) = \mathrm{NextKop}(p) - k_p$ vanishes ($\Delta k(p) = 0$) if and only if $p \in \mathcal{C}_5$ and $p+2$ is prime.
- **Hardy–Littlewood Heuristic (Proposition 3.4):** Under the standard local independence hypothesis, the surviving density of the quadratic annihilator reproduces the Hardy–Littlewood local product:

  $$\prod_{p \ge 5} \left(1 - \frac{1}{(p-1)^2}\right) = \frac{4}{3}C_2.$$

### 3. Complexity & Asymptotic Optimality in Positional Sieving
- **Working Memory (Theorem 4.4):** $\Theta(\sqrt{N}/\log N)$ words (no boolean array of size $N$ is allocated).
- **Time Complexity (Theorem 4.5):** $O(N^{3/2}/\log N)$ elementary operations.
- **Matching Lower Bound (Theorem 4.6):** Any deterministic, state-vectorless sieve algorithm certifying primality via positional divisibility requires $\Omega(N^{3/2}/\log N)$ operations in the worst case. The algorithm is therefore asymptotically optimal within the state-vectorless positional class.

### 4. Structural Optimality of Modulus $m=6$
- **Algebraic Minimality (Theorem 5.4):** $m=6$ uniquely minimizes the candidate survival density $\rho(m) = \phi(m)/m = 1/3$ among all moduli with $\phi(m) \le 2$.
- **Analytic $L$-Value Identity (Theorem 5.5):** For the principal character $\chi_0^{(6)}$ and the primitive quadratic character $\chi_{12} = \chi_{-4}\chi_0^{(3)}$:

  $$L(2, \chi_0^{(6)}) = [L(1, \chi_{12})]^2 = \frac{\pi^2}{9}.$$

---

## 🛡️ Formal Verification in Lean 4 (Mathlib4)

All algebraic results in the manuscript are certified in **Lean 4** (v4.35.0) with strictly **0 `sorry` gaps** and **0 global `axiom` declarations**. The suite comprises **19 self-contained modules** (91 theorems, 30 definitions) audited by the Lean 4 kernel:

| Module Name | Level | Reference | Key Formally Certified Result |
| :--- | :---: | :--- | :--- |
| `ModularClassification.lean` | **N1** | Thm 2.1 | Exhaustive residue classification and prime coverage for $p > 3$. |
| `UnitGroupStructure.lean` | **N1** | §2.1 | Group $(\mathbb{Z}/6\mathbb{Z})^\times = \lbrace 1, 5 \rbrace$ and chiral involution $5 \cdot 5 \equiv 1 \pmod 6$. |
| `PositionalCongruence.lean` | **N1** | Lem 2.3 | Equivalence $p \mid (6k+\varepsilon) \iff p \mid (k - \varepsilon_p\varepsilon k_p)$ via Bézout identity. |
| `KminPlus.lean` | **N1** | Thm 2.5 | Symmetric threshold formula $\kappa_{\min}^+(p) = p k_p + \varepsilon_p k_p$. |
| `EntanglementThresholds.lean` | **N1** | Thm 2.8 | Asymmetric threshold formulas $\kappa_{\min}^-(p)$ across all 4 chiral cases. |
| `CopExistence.lean` | **N1-P** | Def 2.6, Thm 2.7 | Predicate $\mathrm{IsCop}$ and existence conditional on Dirichlet's theorem (parametric). |
| `ThresholdSeparation.lean` | **N1** | Thm 2.9 | Strict inequality $\kappa_{\min}^-(p) > \kappa_{\min}^+(p)$ proved via `nlinarith` and `ring`. |
| `CompositeStructure.lean` | **N1** | Prop A.1 | Full local branching equivalence for composite candidates. |
| `TwinPrimeGroundState.lean` | **N1** | Thm 3.2 | Equivalence between twin primes and quadratic annihilator survival. |
| `TwinPrimesBoth.lean` | **N1** | Rem 2.10 | Mono-prime channel incompatibility ($p \ge 5$ cannot divide $6k\pm 1$ simultaneously). |
| `TwinPrimesExt.lean` | **N1** | §3.3 | Finite Hardy–Littlewood factorization: $\mathrm{survival} = \mathrm{coprime} \times \mathrm{HL}$. |
| `HardyLittlewood.lean` | **N1** | Prop 3.4 | Field identity $1 - (p-1)^{-2} = (p-2)p/(p-1)^2$ and numerical anchor at $p=5$. |
| `EulerFactorization.lean` | **N1** | §2.2 | Finite Euler product separation over active channels $\mathcal{C}_1 \cup \mathcal{C}_5$. |
| `DigitalFilter5.lean` | **N1** | Thm 4.2 | Modulo 5/10 residue reductions ($k \equiv 4,9 \pmod{10}$ and $k \equiv 1,6 \pmod{10}$). |
| `Complexity.lean` | **N1** | Thms 4.4–4.5 | Positivity and algebraic formulation of memory/time bounds. |
| `SieveOperatorSelfAdjoint.lean`| **N1** | §4.3 | Self-adjointness $(M M^T)^T = M M^T$ over arbitrary commutative rings. |
| `ChiralConvergence.lean` | **N1** | §5 | Ratio identity $c_1/c_5 = 1 + (c_1 - c_5)/c_5$ for empirical convergence. |
| `OptimalityM6.lean` | **N1** | Thm 5.4 | Strict minimization of $\rho(m) = \phi(m)/m$ at $m=6$ among $\phi(m) \le 2$. |
| `AnalyticOptimality.lean` | **N1-P** | Thm 5.5 | Proof that $L(2, \chi_0^{(6)}) = [L(1, \chi_{12})]^2 = \pi^2/9$ (conditional on $\zeta(2)$ and $L(1, \chi_{-4})$). |

- **Level N1 (17 modules):** Pure constructive/algebraic theorems proven strictly from Lean 4/Mathlib axioms.
- **Level N1-P (2 modules):** Pure proofs where external analytic inputs (Dirichlet, classical $L$-values) are localized as explicit signature hypotheses, preventing global axiomatic pollution.

---

## ⚡ Computational Benchmark Pipeline

The empirical validation is implemented as an autonomous JIT-compiled engine in **Python 3.13 / Numba 0.61**:

1. **Protocol Rigor (§5.1):** Warm-up iterations, median over 10 repetitions, IQR dispersion, and 95% bootstrap confidence intervals ($B = 10^4$). Single-threaded CPU execution.
2. **Exact Counting (§5.2):** Certified exact prime counting $\pi(N)$ up to $N \sim 3 \times 10^8$ without omission or false detection (reproducing values matching Oliveira e Silva et al.).
3. **Transition Ratios (§5.3):** Empirical runtime scaling ratios match theoretical predictions $\Theta(N^{3/2}/\log N)$ to within 5% for all scales $N \ge 10^6$.
4. **Entanglement Jumps (§5.4):** Complete distribution of $\Delta k(p) = \mathrm{NextKop}(p) - k_p$ at two scales ($N \sim 6 \times 10^7$ and $N \sim 6 \times 10^8$) with Wilson 95% confidence intervals. Demonstrates that ground-state density ($\Delta k = 0$) decreases from 15.75% to 13.83%, consistent with twin-prime decay.
5. **Record Jumps (§5.5):** Analysis of 32 record jumps up to $N \sim 6 \times 10^8$ (maximum $\Delta k = 87$ at $p = 393{,}202{,}127$), comparative model fitting (power law vs. exponential law via AIC/BIC), and Hill tail index estimation.

---

## 📁 Repository Structure

```text
modular-projection-sieve/
├── Papers/
│   └── ATMPS.pdf                            # Full LaTeX manuscript (amsart, MoC format)
├── Notebooks/
│   ├── Lean4_Theory_of_Modular_Projection_Sieving.ipynb # Master Colab notebook (interactive Lean 4 audit)
│   └── ATM_Experimental_Suite.ipynb         # Benchmarking engine, timing logs & Wilson CIs
├── Lean/
│   ├── lean-toolchain                           # Lean toolchain specification (v4.35.0)
│   ├── lakefile.toml                            # Lake workspace configuration
│   ├── lake-manifest.json                       # Mathlib4 frozen dependency manifest
│   ├── ATM_Lean.lean                            # Root aggregation module
│   └── ATM_Lean/                                # 19 verified modules (N1 & N1-P)
│       ├── ModularClassification.lean
│       ├── PositionalCongruence.lean
│       ├── ThresholdSeparation.lean
│       ├── TwinPrimeGroundState.lean
│       └── ...
├── Archive/
│   └── ATM_Lean4_Reproducibility_Suite.zip      # Byte-level audit archive (SHA-256: 0ee5544f...)
├── LICENSE                                      # MIT License
└── README.md                                    # Repository documentation
```
---

## 🚀 Quick Reproduction Guide

### 1. Automated Execution via Google Colab

Click the badge below to run the verified Lean 4 kernel audit and Python benchmarks directly in a browser environment:

### 2. Local Lean 4 Verification

Requires `elan` installed on Linux/macOS:

```bash
# Clone the repository
git clone [https://github.com/NachoPeinador/modular-projection-sieve.git](https://github.com/NachoPeinador/modular-projection-sieve.git)
cd modular-projection-sieve/Lean

# Synchronize dependencies and download Mathlib4 cache
lake update
lake exe cache get!

# Compile and audit the complete formal library
lake build ATM_Lean

# Audit individual modules directly against the Lean 4 kernel
lake env lean ATM_Lean/ThresholdSeparation.lean
lake env lean ATM_Lean/TwinPrimeGroundState.lean
lake env lean ATM_Lean/CompositeStructure.lean

```

### 3. Local Python Benchmarking

```bash
python -m venv venv
source venv/bin/activate
pip install numpy numba scipy

# Execute benchmark suite up to N ~ 3 x 10^8
python -c "import numba; print('Numba version:', numba.__version__)"
jupyter notebook Notebooks/ATM_Experimental_Suite.ipynb

```

---

## 📜 Citation

If you utilize this algebraic framework, the asymmetric threshold formulation, or the Lean 4 formalization library in your research, please cite:

```bibtex
@article{Peinador2026ATM,
  author    = {Peinador Sala, Jos{\'e} Ignacio},
  title     = {Algebraic Theory of Modular Projection Sieving: Prime-Coprime Entanglement and Asymmetric Activation Thresholds},
  journal   = {Submitted to Mathematics of Computation},
  year      = {2026},
  note      = {AMS Submission ID: 261023-PeinadorSala. Complete verification suite archived at Zenodo: \url{[https://doi.org/10.5281/zenodo.22043293](https://doi.org/10.5281/zenodo.22043293)}}
}

```
---

## ⚖️ License

The Lean 4 verification library, computational algorithms, and datasets in this repository are distributed under the **[MIT License](https://www.google.com/search?q=LICENSE)**.

