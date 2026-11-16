---
layout: default
title: Gaussian Elimination
math: true
---

# Direct solution by Gaussian elimination

As a base numerical strategy, the linear system obtained from the finite-difference discretization in the previous subsection is solved by Gaussian elimination with partial pivoting. In this approach, the coefficient matrix $\mathbf A \in \mathbb R^{N \times N}$, is assembled explicitly and treated as a general dense matrix. No use is made of its tridiagonal-plus-rank-one structure. This baseline implementation serves as a point of comparison against which the computational advantages of the subsequent formulations can be assessed.

For completeness, the entries of the coefficient matrix and the right-hand side are:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
A_{ij} = \frac{-2\delta_{ij} + \delta_{i,j-1} + \delta_{i,j+1}}{h^2} - \Lambda\delta^2h\Psi_i\Psi_j,
$$
</div>

and $b_i = \Pi_D$, with $i,j = 1, \ldots, N$, where $\delta_{ij}$ denotes the Kronecker delta. The boundary values are already incorporated through the homogeneous Dirichlet conditions.

As we know, Gaussian elimination transforms the system $\mathbf A \mathbf f = \mathbf b$ into an equivalent upper-triangular system. To improve numerical robustness, partial pivoting is performed at each elimination step. At step $k$, a pivot row $p$ is selected according to:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
p = \operatorname*{arg\,max}_{k \leq i \leq N} \left| A_{ik}^{(k)} \right|,
$$
</div>

where $A^{(k)}$ denotes the coefficient matrix at the beginning of elimination step $k$. The resulting nodal solution $\mathbf f$ is used to evaluate the discrete integral $I_h$, the derived quantities, and the discrepancies with respect to the analytical solution. 

Because all subsequent algebraic strategies will be applied to the same finite-difference discretization, their numerical solutions are expected to agree up to floating-point effects. Accordingly, comparisons of accuracy against the analytical reference assess the discretization, whereas comparisons of execution time and memory requirements assess the efficiency of the respective linear-system solvers.

The complete computational procedure, including matrix assembly, partial pivoting, forward elimination, and backward substitution, is summarized in **Algorithm 1**.

---

## Algorithm 1: Dense Gaussian elimination with partial pivoting

<div style="background:#fafafa; border:1px solid #e0e0e0; border-left:4px solid #3c6e71; border-radius:8px; padding:20px; margin:20px 0; overflow-x:auto; font-family: monospace; font-size: 0.95rem; line-height: 1.6;">
  <strong>Require:</strong> Number of interior nodes $N$; parameters $\Pi_D, \Lambda, \delta$; pivot threshold $\tau \geq 0$.<br>
  <strong>Ensure:</strong> Nodal solution $\mathbf f = (F_1, \ldots, F_N)^T$ or a failure message.<br><br>
  
  $h \gets 2/(N+1)$<br>
  <strong>for</strong> $i = 1, \ldots, N$ <strong>do</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;$Y_i \gets -1 + ih$; $\Psi_i \gets \cosh(\delta Y_i) / \cosh(\delta)$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;$b_i \gets \Pi_D$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>for</strong> $j = 1, \ldots, N$ <strong>do</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$A_{ij} \gets \frac{-2\delta_{ij} + \delta_{i,j-1} + \delta_{i,j+1}}{h^2} - \Lambda\delta^2h\Psi_i\Psi_j$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>end for</strong><br>
  <strong>end for</strong><br><br>
  
  <strong>for</strong> $k = 1, \ldots, N-1$ <strong>do</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;$p \gets \operatorname*{arg\,max}_{k \leq i \leq N} |A_{ik}|$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>if</strong> $|A_{pk}| \leq \tau$ <strong>then</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<strong>return</strong> <code>Failure</code><br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>end if</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>if</strong> $p \neq k$ <strong>then</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Swap rows $p$ and $k$ of $\mathbf A$; swap $b_p$ and $b_k$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>end if</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>for</strong> $i = k+1, \ldots, N$ <strong>do</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$m_{ik} \gets A_{ik} / A_{kk}$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$A_{ik} \gets 0$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<strong>for</strong> $j = k+1, \ldots, N$ <strong>do</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$A_{ij} \gets A_{ij} - m_{ik}A_{kj}$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<strong>end for</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$b_i \gets b_i - m_{ik}b_k$<br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>end for</strong><br>
  <strong>end for</strong><br><br>
  
  <strong>if</strong> $|A_{NN}| \leq \tau$ <strong>then</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;<strong>return</strong> <code>Failure</code><br>
  <strong>end if</strong><br><br>
  
  $F_N \gets b_N / A_{NN}$<br>
  <strong>for</strong> $i = N-1, N-2, \ldots, 1$ <strong>do</strong><br>
  &nbsp;&nbsp;&nbsp;&nbsp;$F_i \gets \frac{b_i - \sum_{j=i+1}^{N} A_{ij}F_j}{A_{ii}}$<br>
  <strong>end for</strong><br><br>
  
  <strong>return</strong> $\mathbf f$
</div>