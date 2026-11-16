---
layout: default
title: Overview
math: true
---
# Overview

The present repository documents the computational implementation of an exact analytical solution for the electrokinetic flow of an electrolyte through a silica microchannel, where forward osmosis drives the fluid motion to generate a streaming potential. 

Assuming a fully developed flow, the mathematical model (which couples the Navier-Stokes equations, electric-current conservation, and a prescribed volumetric flow rate) reduces to the following linear Fredholm integro-differential equation with a separable rank-one kernel:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
0 = -\Pi_D + \frac{d^2F}{dY^2} - \Lambda\delta^2 \frac{\cosh(\delta Y)}{\cosh(\delta)} \int_{-1}^{1} F(s)\frac{\cosh(\delta s)}{\cosh(\delta)}\,ds
$$
</div>

where $F(Y)$ is the transverse function that determines the dimensionless longitudinal velocity $U(Y)$, $\Pi_D$ is the modified pressure gradient parameter, and $\Lambda$ and $\delta$ are electrokinetic dimensionless parameters.

## Python Codes and Implementations

<div style="margin: 1.5rem 0; padding: 1.25rem 1.5rem; background:#fafafa; border-radius:10px; border:1px solid #e0e0e0;">
  <h3 style="margin-top:0; margin-bottom:0.75rem; font-size:1.1rem;">
    Python implementations included in this repository:
  </h3>

  <ul style="margin:0; padding-left:1.2rem; list-style-type:disc;">
    <li style="margin:0.4rem 0;">
      <strong>Analytical Solution</strong><br/>
      <span>Direct evaluation of the closed-form exact mathematical expressions for the transverse function and velocity profile.</span>
    </li>
    <li style="margin:0.4rem 0;">
      <strong>Dense Gaussian Elimination Solver</strong><br/>
      <span>Baseline finite-difference solver treating the discretized integro-differential equation as a general dense matrix (using <code>SciPy</code>/<code>NumPy</code>).</span>
    </li>
    <li style="margin:0.4rem 0;">
      <strong>Schur-Complement Reduction</strong><br/>
      <span>An optimized numerical approach that exploits the block structure of the augmented linear system using a tridiagonal solver algorithm.</span>
    </li>
    <li style="margin:0.4rem 0;">
      <strong>Sherman–Morrison Rank-One Update</strong><br/>
      <span>A highly efficient implementation that applies the Sherman-Morrison formula directly to the rank-one modified tridiagonal operator.</span>
    </li>
    <li style="margin:0.4rem 0;">
      <strong>Computational Efficiency Benchmark</strong><br/>
      <span>A performance routine utilizing Python's <code>perf_counter_ns()</code> to evaluate and compare execution times, demonstrating the $O(N)$ vs $O(N^3)$ complexity differences.</span>
    </li>
  </ul>
</div>

## The related article

These results accompany the manuscript:  

<div style="display:inline-block; padding:0.6em 0.9em; margin:0.4em 0; background-color:#f5f5f5; border:1px solid #dddddd; border-radius:6px;" markdown="1">
***Power Generation in a Silica Microchannel Driven by Forward Osmosis***
</div>

that was recently submitted to the journal *Tecnología y Ciencia Aplicada* (ISSN 2992-8338), edited in Mexico by the Tecnológico Nacional de México.

# Map of the site 
You can use the navigation bar above, or the following buttons, to explore:

<div style="display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:0.9rem; margin:1rem 0;">

  <a href="{{ '/finite-difference.html' | relative_url }}" style="text-decoration:none; color:inherit;">
    <div style="background:#fafafa; border:1px solid #e0e0e0; border-radius:10px; padding:0.75rem 0.9rem; cursor:pointer;">
      <strong>Finite Difference</strong><br/>
      <span style="font-size:0.95rem; color:#555;">
        Discretization of the linear Fredholm integro-differential equation.
      </span>
    </div>
  </a>

  <a href="{{ '/gaussian-elimination.html' | relative_url }}" style="text-decoration:none; color:inherit;">
    <div style="background:#fafafa; border:1px solid #e0e0e0; border-radius:10px; padding:0.75rem 0.9rem; cursor:pointer;">
      <strong>Gaussian Elimination</strong><br/>
      <span style="font-size:0.95rem; color:#555;">
        Direct solution baseline treating the system as a dense matrix.
      </span>
    </div>
  </a>

  <a href="{{ '/schur-complement.html' | relative_url }}" style="text-decoration:none; color:inherit;">
    <div style="background:#fafafa; border:1px solid #e0e0e0; border-radius:10px; padding:0.75rem 0.9rem; cursor:pointer;">
      <strong>Schur-Complement</strong><br/>
      <span style="font-size:0.95rem; color:#555;">
        Block structure elimination yielding $O(N)$ computational complexity.
      </span>
    </div>
  </a>

  <a href="{{ '/numerical-verification.html' | relative_url }}" style="text-decoration:none; color:inherit;">
    <div style="background:#fafafa; border:1px solid #e0e0e0; border-radius:10px; padding:0.75rem 0.9rem; cursor:pointer;">
      <strong>Verification</strong><br/>
      <span style="font-size:0.95rem; color:#555;">
        Comparison of analytical vs. numerical profiles and APE analysis.
      </span>
    </div>
  </a>
  
  <a href="{{ '/computational-efficiency.html' | relative_url }}" style="text-decoration:none; color:inherit;">
    <div style="background:#fafafa; border:1px solid #e0e0e0; border-radius:10px; padding:0.75rem 0.9rem; cursor:pointer;">
      <strong>Efficiency</strong><br/>
      <span style="font-size:0.95rem; color:#555;">
        Execution times analysis and speedup benchmarking of the methods.
      </span>
    </div>
  </a>

</div>

<div style="border-left: 4px solid #f39c12; padding: 0.7em 1em; background: #fff7e6; margin-top: 1.5rem;">
<b style="color:#c0392b;">⚠️ Important:</b><br>
For full details on the mathematical nondimensionalization, Debye-Hückel approximation, and derivation of the analytical solution, please refer to the main manuscript mentioned above.
</div>
