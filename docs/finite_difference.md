---
layout: default
title: Finite Difference
math: true
---

# Finite-difference discretization of the integro-differential equation

To independently verify the analytical solution derived in the previous section, the governing Fredholm integro-differential equation is discretized using a finite-difference approach. The numerical formulation is developed directly from the original governing equation subjected to the homogeneous Dirichlet boundary conditions $F(-1)=F(1)=0$.

The computational domain $[-1,1]$ is divided into $N+1$ equally spaced subintervals, defining the nodal coordinates:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
Y_i = -1 + ih, \qquad h = \frac{2}{N+1},
$$
</div>

for $i=0,1,\ldots,N+1$. Here, $N$ denotes the number of interior nodes, while $Y_0=-1$ and $Y_{N+1}=1$ correspond to the boundaries. The numerical approximation to $F(Y_i)$ is denoted by $F_i$. At each interior node, the second derivative is approximated using the standard second-order central-difference formula:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
F''(Y_i) = \frac{F(Y_{i-1}) - 2F(Y_i) + F(Y_{i+1})}{h^2} + O(h^2).
$$
</div>

The integral containing the nonlocal term is approximated using the composite trapezoidal rule:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
I_h = \frac{h}{2} \left[ F_0\Psi_0 + 2\sum_{j=1}^{N} F_j\Psi_j + F_{N+1}\Psi_{N+1} \right].
$$
</div>

Since the boundary conditions impose $F_0=F_{N+1}=0$, this expression simplifies to:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
I_h = h\sum_{j=1}^{N} F_j\Psi_j.
$$
</div>

Substituting these approximations into the governing equation yields:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\frac{F_{i-1} - 2F_i + F_{i+1}}{h^2} - \Lambda\delta^2h\Psi_i\sum_{j=1}^{N} F_j\Psi_j = \Pi_D.
$$
</div>

Although the original equation contains a nonlocal integral term, the latter discrete formulation remains linear. Its feature is that the approximation at each interior node depends on all interior nodal values through the quadrature approximation of the integral. Introducing the vectors:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\mathbf{f} = \begin{pmatrix} F_1 \\ F_2 \\ \vdots \\ F_N \end{pmatrix}, \qquad 
\boldsymbol{\psi} = \begin{pmatrix} \Psi_1 \\ \Psi_2 \\ \vdots \\ \Psi_N \end{pmatrix}, \qquad 
\mathbf{1} = \begin{pmatrix} 1 \\ 1 \\ \vdots \\ 1 \end{pmatrix},
$$
</div>

the discrete equations can be expressed in matrix form as:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\left( \mathbf{D} - \Lambda\delta^2h\,\boldsymbol{\psi}\boldsymbol{\psi}^T \right)\mathbf{f} = \Pi_D\mathbf{1},
$$
</div>

where

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\mathbf{D} = \frac{1}{h^2} \begin{pmatrix}
-2 & 1 & 0 & \cdots & 0 \\
1 & -2 & 1 & \ddots & \vdots \\
0 & 1 & -2 & \ddots & 0 \\
\vdots & \ddots & \ddots & \ddots & 1 \\
0 & \cdots & 0 & 1 & -2
\end{pmatrix}
$$
</div>

is the tridiagonal matrix associated with the second-order central-difference approximation. Defining

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\mathbf{A} = \mathbf{D} - \Lambda\delta^2h\,\boldsymbol{\psi}\boldsymbol{\psi}^T, \qquad \mathbf{b} = \Pi_D\mathbf{1},
$$
</div>

the numerical problem reduces to the linear algebraic system:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\mathbf{A}\mathbf{f} = \mathbf{b}.
$$
</div>

An important property of this formulation is that the nonlocal contribution constitutes a rank-one modification of the tridiagonal finite-difference matrix. Furthermore, for $\Lambda \geq 0$, the coefficient matrix is symmetric and negative definite. Indeed, for any nonzero vector $\mathbf{x} \in \mathbb{R}^N$:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\mathbf{x}^T\mathbf{A}\mathbf{x} = \mathbf{x}^T\mathbf{D}\mathbf{x} - \Lambda\delta^2h\left(\boldsymbol{\psi}^T\mathbf{x}\right)^2 < 0,
$$
</div>

because $\mathbf{D}$ is negative definite under homogeneous Dirichlet boundary conditions. Therefore, the discrete system admits a unique solution for every $N \geq 1$ and $\Lambda \geq 0$.

This matrix formulation provides a basis for the numerical strategies considered below. The first approach employs a conventional dense linear-system solver, whereas the subsequent formulations exploit the special structure of the discrete operator to reduce computational cost.