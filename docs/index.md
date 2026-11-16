---
layout: default
title: Home
math: true
---
# Overview

The present repository provides the computational implementation that allows the verification of the exact analytical solution of the electrokinetic flow of an electrolyte through a silica microchannel driven by forward osmosis.

The governing equations describing the steady, fully developed flow in the microchannel reduce to the following linear Fredholm integro-differential equation with a separable rank-one kernel:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
0 = -\Pi_D + \frac{d^2F}{dY^2} - \Lambda\delta^2 \frac{\cosh(\delta Y)}{\cosh(\delta)} \int_{-1}^{1} F(s)\frac{\cosh(\delta s)}{\cosh(\delta)}\,ds
$$
</div>

## Numerical Implementations

<div style="margin: 1.5rem 0; padding: 1.25rem 1.5rem; background:#fafafa; border-radius:10px; border:1px solid #e0e0e0;">
  <h3 style="margin-top:0; margin-bottom:0.75rem; font-size:1.1rem;">
    Implementations included in this repository:
  </h3>

  <ul style="margin:0; padding-left:1.2rem; list-style-type:disc;">
    <li style="margin:0.4rem 0;">
      <strong>Finite-difference discretization</strong><br/>
      <span>Implementation of the integro-differential equation on a discrete grid.</span>
    </li>
    <li style="margin:0.4rem 0;">
      <strong>Direct solution by Gaussian elimination</strong><br/>
      <span>Base numerical strategy using partial pivoting.</span>
    </li>
    <li style="margin:0.4rem 0;">
      <strong>Schur-complement reduction</strong><br/>
      <span>Implementation of block elimination for the augmented system.</span>
    </li>
    <li style="margin:0.4rem 0;">
      <strong>Sherman-Morrison rank-one update</strong><br/>
      <span>Fast evaluation exploiting the rank-one modification of the tridiagonal matrix.</span>
    </li>
  </ul>
</div>

## The related article

These results accompany the manuscript:  

<div style="display:inline-block; padding:0.6em 0.9em; margin:0.4em 0;
            background-color:#f5f5f5; border:1px solid #dddddd; border-radius:6px;"
     markdown="1">
***Power Generation in a Silica Microchannel Driven by Forward Osmosis***
</div>

that was recently submitted to the journal *Tecnología y Ciencia Aplicada*.

# Map of the site 
You can use the navigation bar above, or the following buttons, to explore:

[Finite Difference]({{ '/finite-difference.html' | relative_url }})<br>
[Discretization of the linear Fredholm integro-differential equation.]({{ '/finite-difference.html' | relative_url }})

[Gaussian Elimination]({{ '/gaussian-elimination.html' | relative_url }})<br>
[Direct solution baseline treating the system as a dense matrix.]({{ '/gaussian-elimination.html' | relative_url }})

[Schur-Complement]({{ '/schur-complement.html' | relative_url }})<br>
[Block structure elimination yielding $O(N)$ computational complexity.]({{ '/schur-complement.html' | relative_url }})

[Sherman-Morrison]({{ '/sherman-morrison.html' | relative_url }})<br>
[Sherman-Morrison rank-one update strategy.]({{ '/sherman-morrison.html' | relative_url }})

[Verification]({{ '/numerical-verification.html' | relative_url }})<br>
[Comparison of analytical vs. numerical profiles and APE analysis.]({{ '/numerical-verification.html' | relative_url }})

[Efficiency]({{ '/computational-efficiency.html' | relative_url }})<br>
[Execution times analysis and speedup benchmarking of the methods.]({{ '/computational-efficiency.html' | relative_url }})

<div style="border-left: 4px solid #f39c12; padding: 0.7em 1em; background: #fff7e6; margin-top: 2rem;">
<b style="color:#c0392b;">⚠️ Important:</b><br>
For full details on the mathematical nondimensionalization, Debye-Hückel approximation, and derivation of the analytical solution, please refer to the main manuscript mentioned above.
</div>