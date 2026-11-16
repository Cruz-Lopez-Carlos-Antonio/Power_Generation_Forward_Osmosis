# Power Generation in a Silica Microchannel Driven by Forward Osmosis


## Overview of the Repository

The present repository provides the computational implementation that allows the verification of the exact analytical solution developed in this work. This research was recently submitted to the journal "Tecnología y Ciencia Aplicada" (ISSN 2992-8338), a biannual publication edited in Mexico by the Tecnológico Nacional de México through the Centro Nacional de Investigación y Desarrollo Tecnológico (CENIDET).

The physical system consists of an electrokinetic flow of an electrolyte through a silica microchannel bounded by two parallel plates, where forward osmosis drives the fluid motion to generate a streaming potential. Assuming a fully developed flow, the coupled Navier-Stokes equations, electric-current conservation, and a prescribed volumetric flow rate reduce to a linear Fredholm integro-differential equation with a separable rank-one kernel:

$$0 = -\Pi_D + \frac{d^2F}{dY^2} - \Lambda\delta^2 \frac{\cosh(\delta Y)}{\cosh(\delta)} \int_{-1}^{1} F(s)\frac{\cosh(\delta s)}{\cosh(\delta)}\,ds$$

By exploiting this mathematical structure, an exact closed-form solution is derived for the transverse function $F(Y)$, which uniquely defines the dimensionless longitudinal velocity $U(Y) = \frac{d\Pi}{dX} F(Y)$ under the homogeneous Dirichlet boundary conditions $F(\pm 1) = 0$. This analytical framework directly enables the precise determination of the pressure distribution and the streaming potential without requiring complex iterative algorithms.

## Authors and Financial Support

**Authors:**

* Guillermo Alberto Sánchez-Lozano (Universidad Nacional Autónoma de México)
* Carlos Antonio Cruz-López (Universidad Autónoma Metropolitana)

**Financial Support**

Guillermo Sánchez and Carlos Cruz acknowledges the support from Programa de Apoyo a Proyectos de Investigación e Innovación Tecnológica (PAPPIT), DGAPA-PAPIIT, of Universidad Autónoma Nacional de México (UNAM), under contract number IA104126.

The author Carlos Antonio Cruz López gratefully acknowledges the financial support received from the Secretaría de Ciencia, Humanidades, Tecnología e Innovación (SECIHTI, formerly known as CONAHCYT), through the program *Estancias Posdoctorales por México, 2022*, under the project entitled: *Desarrollo de modelos fenomenológicos energéticos de orden fraccional, para la optimización y simulación en reactores nucleares de potencia*, as well as the financial support from the Basic Science and Frontier Project 2023-2024, with the reference CBF-2023-2024-2023, also belonging to SECIHTI-CONAHCYT.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details. You are free to use, modify, and distribute this software for academic and commercial purposes, provided that appropriate credit is given to the original authors.

## Web of the Repository
<div style="background:#f1f7ff; padding:12px 15px; border-left:4px solid #4a90e2; border-radius:8px; margin-top:20px;">
  <strong>📘 Full Documentation</strong><br>
  The complete project website (opens in a new page) is available here:<br><br>
  👉 <a href="https://cruz-lopez-carlos-antonio.github.io/Power-Series-of-Bateman-Equations/"
        target="_blank" rel="noopener noreferrer">

        https://cruz-lopez-carlos-antonio.github.io/Power-Series-of-Bateman-Equations/
      </a>

</div>
