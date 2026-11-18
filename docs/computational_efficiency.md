---
layout: default
title: Computational Efficiency
math: true
---

# Computational Efficiency

Although the three numerical approaches solve the same discretized integro-differential equation, their computational costs differ due to the underlying algebraic procedures. This section examines their computational efficiency and compares their performance against the direct evaluation of the analytical solution.

## 1. Experimental Setup

The computational experiments were performed under the following hardware and software conditions:
* **Processor:** AMD Ryzen 7 5700G (3.80 GHz)
* **Memory:** 32 GB of RAM
* **Environment:** 64-bit Windows operating system, Python using `NumPy` and `SciPy`.
* **Arithmetic:** Double-precision floating-point arithmetic.

To reduce the influence of initialization costs, five preliminary executions were performed before collecting measurements. Subsequently, **30 repetitions** were carried out for each method and grid size, randomizing the execution order to minimize systematic evaluation effects. The computational times are characterized by their arithmetic mean and sample standard deviation.

---

## 2. Comparison Among Numerical Methods

The first stage compares the three numerical approaches using the same spatial discretizations. Gaussian elimination was implemented via a dense LU factorization with partial pivoting ($O(N^3)$ complexity), whereas the Schur-complement and Sherman–Morrison approaches exploited the tridiagonal structure of the finite-difference operator ($O(N)$ complexity).

**Table 1: Mean computational times (ms) for the numerical methods.**

| $N$ | Gauss-LU | Schur | Sherman–Morrison |
| :---: | :---: | :---: | :---: |
| 100 | $0.211 \pm 0.014$ | $0.099 \pm 0.006$ | $0.099 \pm 0.004$ |
| 200 | $0.461 \pm 0.068$ | $0.121 \pm 0.018$ | $0.123 \pm 0.020$ |
| 400 | $2.602 \pm 0.392$ | $0.177 \pm 0.039$ | $0.170 \pm 0.038$ |
| 800 | $10.718 \pm 1.168$ | $0.280 \pm 0.100$ | $0.256 \pm 0.097$ |

<div style="border-left: 4px solid #f39c12; padding: 0.7em 1em; background: #fff7e6; margin: 1.5rem 0;">
<b>💡 Highlight:</b><br>
For $N=800$, the structured methods (Schur and Sherman-Morrison) achieved speedup factors of approximately <b>38.3</b> and <b>41.9</b> relative to dense Gaussian elimination, demonstrating the massive advantage of exploiting the matrix structure.
</div>

---

## 3. Analytical vs. Numerical Performance

In the second stage, the direct evaluation of the analytical expressions is compared against the numerical methods. The analytical solution directly evaluates the closed-form expressions at the $N+2$ grid points (including boundaries) without assembling any algebraic system.

### Analytical vs. Sherman-Morrison

**Table 2: Computational performance of the analytical solution vs. Sherman–Morrison.**

| $N$ | Analytical (ms) | SM (ms) | $S_{\mathrm{SM}}$ (Speedup) |
| :---: | :---: | :---: | :---: |
| 100 | $0.0180 \pm 0.0003$ | $0.0939 \pm 0.0049$ | **5.22** |
| 200 | $0.0198 \pm 0.0003$ | $0.0989 \pm 0.0050$ | **5.00** |
| 400 | $0.0216 \pm 0.0005$ | $0.1067 \pm 0.0039$ | **4.94** |
| 800 | $0.0267 \pm 0.0010$ | $0.1237 \pm 0.0022$ | **4.63** |

### Analytical vs. Gaussian Elimination

**Table 3: Computational performance of the analytical solution vs. Gaussian elimination.**

| $N$ | Analytical (ms) | Gauss-LU (ms) | $S_{\mathrm{G}}$ (Speedup) |
| :---: | :---: | :---: | :---: |
| 100 | $0.0186 \pm 0.0008$ | $0.2109 \pm 0.0150$ | **11.34** |
| 200 | $0.0274 \pm 0.0060$ | $0.5119 \pm 0.0413$ | **18.66** |
| 400 | $0.0350 \pm 0.0080$ | $2.3907 \pm 0.1378$ | **68.28** |
| 800 | $0.0427 \pm 0.0095$ | $9.7281 \pm 0.5138$ | **227.91** |

<div style="background:#eafaf1; border-left:4px solid #27ae60; padding:15px; border-radius:6px; margin-top:20px;">
<strong>Conclusion</strong><br>
The analytical formulation is substantially faster than both the standard $O(N^3)$ Gaussian elimination and the optimized $O(N)$ numerical schemes. It provides an efficient computational alternative for evaluating the streaming potential, without the overhead of spatial discretization and algebraic system assembly.
</div>