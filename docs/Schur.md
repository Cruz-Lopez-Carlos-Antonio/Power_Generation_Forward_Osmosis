---
layout: default
title: Schur-Complement
math: true
---

# Augmented-System Formulation

An alternative representation of the discrete problem can be obtained by treating the nonlocal integral as an additional unknown. Expressing $I_h$ as:

$$
I_h=h\sum_{j=1}^{N}F_j\Psi_j=h\boldsymbol\psi^T\mathbf f
$$

and introducing the notation $\gamma=\Lambda\delta^2$, the finite-difference equations become:

$$
\mathbf D\mathbf f-\gamma\boldsymbol\psi I_h=\Pi_D\mathbf 1
$$

while the quadrature relation supplies the additional equation:

$$
-h\boldsymbol\psi^T\mathbf f+I_h=0
$$

Combining these yields the $(N+1)\times(N+1)$ augmented linear system:

$$
\begin{pmatrix}
\mathbf D & -\gamma\boldsymbol\psi\\
-h\boldsymbol\psi^T & 1
\end{pmatrix}
\begin{pmatrix}
\mathbf f\\ I_h
\end{pmatrix}
=
\begin{pmatrix}
\Pi_D\mathbf 1\\ 0
\end{pmatrix}
$$

To make its structure explicit, the augmented coefficient matrix can also be displayed as:

$$
\mathbf A_{\mathrm{aug}}=
\left(
\begin{array}{ccccc|c}
-2/h^2 & 1/h^2 & 0 & \cdots & 0 & -\gamma\Psi_1\\
1/h^2 & -2/h^2 & 1/h^2 & \ddots & \vdots & -\gamma\Psi_2\\
0 & 1/h^2 & -2/h^2 & \ddots & 0 & -\gamma\Psi_3\\
\vdots & \ddots & \ddots & \ddots & 1/h^2 & \vdots\\
0 & \cdots & 0 & 1/h^2 & -2/h^2 & -\gamma\Psi_N\\ \hline
-h\Psi_1 & -h\Psi_2 & -h\Psi_3 & \cdots & -h\Psi_N & 1
\end{array}
\right)
$$

Unlike the dense $N\times N$ matrix of the direct formulation, $\mathbf A_{\mathrm{aug}}$ contains a tridiagonal principal block coupled to one additional row and column. Consequently, the augmented matrix has $O(N)$ nonzero entries, allowing for significant computational savings when its structure is exploited.

---

# Schur-Complement Reduction

The Schur complement can be understood as an extension of Gaussian elimination to linear systems whose coefficient matrices are partitioned into blocks (Zhang, 2005). Rather than eliminating individual unknowns one at a time, block elimination removes an entire group of variables while preserving its influence on the remaining equations.

For our present electrokinetic model, the Schur complement is a scalar rather than a matrix:

$$
S=1-\gamma h\boldsymbol\psi^T\mathbf D^{-1}\boldsymbol\psi
$$

Eliminating the nodal vector $\mathbf f$ accordingly leaves the single equation:

$$
S I_h=h\Pi_D\boldsymbol\psi^T\mathbf D^{-1}\mathbf 1
$$

To avoid explicitly forming the inverse matrix $\mathbf D^{-1}$, we define two auxiliary vectors by solving:

$$
\mathbf D\mathbf z=\Pi_D\mathbf 1, \qquad \mathbf D\mathbf v=\gamma\boldsymbol\psi
$$

The two tridiagonal systems arising from the Schur-complement reduction can be solved efficiently using the Thomas algorithm, a specialized form of Gaussian elimination for tridiagonal matrices. This procedure requires only $O(N)$ arithmetic operations and $O(N)$ storage. 

The discrete integral and the nodal solution are then obtained as:

$$
I_h=\frac{h\boldsymbol\psi^T\mathbf z}{1-h\boldsymbol\psi^T\mathbf v}, \qquad \mathbf f=\mathbf z+I_h\mathbf v
$$

---

## Algorithm 2: Schur-complement reduction for the finite-difference system

<div style="background:#fcfcfc; border:1px solid #e0e0e0; border-left:4px solid #4a90e2; border-radius:6px; padding:15px; margin-top:20px; margin-bottom:20px; overflow-x:auto; font-family: 'Courier New', Courier, monospace; font-size: 0.95rem; line-height: 1.5;">
<strong>Require:</strong> Number of interior nodes $N$; parameters $\Pi_D,\Lambda,\delta$.<br>
<strong>Ensure:</strong> Nodal solution $\mathbf f=(F_1,\ldots,F_N)^T$ and discrete integral $I_h$.<br><br>

$h \gets 2/(N+1)$;<br>
$\gamma \gets \Lambda\delta^2$<br><br>

<strong>for</strong> $i=1,\ldots,N$ <strong>do</strong><br>
&nbsp;&nbsp;&nbsp;&nbsp;$Y_i \gets -1+ih$<br>
&nbsp;&nbsp;&nbsp;&nbsp;$\Psi_i \gets \cosh(\delta Y_i)/\cosh(\delta)$<br>
&nbsp;&nbsp;&nbsp;&nbsp;$a_i \gets h^{-2}$; $d_i \gets -2h^{-2}$; $c_i \gets h^{-2}$<br>
&nbsp;&nbsp;&nbsp;&nbsp;$r_i^{(1)} \gets \Pi_D$; $r_i^{(2)} \gets \gamma\Psi_i$<br>
<strong>end for</strong><br><br>

$a_1 \gets 0$; $c_N \gets 0$<br><br>

<em style="color:#2c3e50;">// Tridiagonal factorization (Thomas algorithm)</em><br>
<strong>for</strong> $i=2,\ldots,N$ <strong>do</strong><br>
&nbsp;&nbsp;&nbsp;&nbsp;$m_i \gets a_i/d_{i-1}$<br>
&nbsp;&nbsp;&nbsp;&nbsp;$d_i \gets d_i-m_ic_{i-1}$<br>
&nbsp;&nbsp;&nbsp;&nbsp;$r_i^{(1)} \gets r_i^{(1)}-m_ir_{i-1}^{(1)}$<br>
&nbsp;&nbsp;&nbsp;&nbsp;$r_i^{(2)} \gets r_i^{(2)}-m_ir_{i-1}^{(2)}$<br>
<strong>end for</strong><br><br>

<em style="color:#2c3e50;">// Backward substitution</em><br>
$z_N \gets r_N^{(1)}/d_N$<br>
$v_N \gets r_N^{(2)}/d_N$<br>
<strong>for</strong> $i=N-1,N-2,\ldots,1$ <strong>do</strong><br>
&nbsp;&nbsp;&nbsp;&nbsp;$z_i \gets (r_i^{(1)}-c_iz_{i+1})/d_i$<br>
&nbsp;&nbsp;&nbsp;&nbsp;$v_i \gets (r_i^{(2)}-c_iv_{i+1})/d_i$<br>
<strong>end for</strong><br><br>

<em style="color:#2c3e50;">// Schur-complement evaluation</em><br>
$S \gets 1-h\sum_{i=1}^{N}\Psi_iv_i$<br>
$I_h \gets (h\sum_{i=1}^{N}\Psi_iz_i)/S$<br><br>

<em style="color:#2c3e50;">// Solution reconstruction</em><br>
<strong>for</strong> $i=1,\ldots,N$ <strong>do</strong><br>
&nbsp;&nbsp;&nbsp;&nbsp;$F_i \gets z_i+I_hv_i$<br>
<strong>end for</strong><br><br>

<strong>return</strong> $\mathbf f, I_h$
</div>