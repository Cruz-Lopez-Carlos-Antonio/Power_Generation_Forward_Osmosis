---
layout: default
title: Appendices
math: true
---

# Appendices

This section gathers the three mathematical appendices supporting the analytical formulation developed in the main manuscript:

* [Appendix A: Nondimensionalization of the Governing Equations](#appendix-a-nondimensionalization-of-the-governing-equations)
* [Appendix B: Derivation of the Dimensionless Physical Pressure](#appendix-b-derivation-of-the-dimensionless-physical-pressure)
* [Appendix C: Fully Developed Flow and Simplification of the Governing Equations](#appendix-c-fully-developed-flow-and-simplification-of-the-governing-equations)

---

## Appendix A: Nondimensionalization of the Governing Equations

### A.1 Spatial Coordinates and Longitudinal Velocity

To transition from the physical model to a dimensionless framework, we define characteristic scales based on the geometry, boundary conditions, and flow properties of the microchannel. Since the channel is assumed to be slender ($L \gg l$), the scaling of the spatial coordinates follows naturally as:

$$
X = \frac{x}{L}, \qquad Y = \frac{y}{l}.
$$

On the other hand, the integral flow constraint establishes that the mean longitudinal velocity equals the water flux across the membrane, $\bar{u} = J_w$. Thus, $J_w$ is chosen as the characteristic longitudinal velocity:

$$
U = \frac{u}{J_w}.
$$

### A.2 Continuity Equation and Transverse Velocity Scaling

Once the dimensionless variables $X$, $Y$, and $U$ have been defined, it is possible to construct the scale for the transverse velocity. Naturally, we expect the dimensionless transverse velocity to be of the form $V = v/v_c$, where $v_c$ is an unknown reference velocity determined from the balance of the continuity equation. Substituting the defined variables into the continuity equation yields:

$$
\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} = \frac{\partial (J_w U)}{\partial (L X)} + \frac{\partial (v_c V)}{\partial (l Y)} = 0 \implies \frac{J_w}{L} \frac{\partial U}{\partial X} + \frac{v_c}{l} \frac{\partial V}{\partial Y} = 0.
$$

For both terms to contribute equally to the mass balance (assuming the dimensionless derivatives are of the same order of magnitude), their respective dimensional coefficients must balance:

$$
\frac{J_w}{L} = \frac{v_c}{l}.
$$

Isolating the unknown scale gives $v_c = J_w(l/L)$. Therefore, the dimensionless transverse velocity is defined as:

$$
V = \frac{v}{J_w \left(\frac{l}{L}\right)}.
$$

Substituting this definition back into the continuity equation results in its standard dimensionless form:

$$
\frac{\partial U}{\partial X} + \frac{\partial V}{\partial Y} = 0.
$$

### A.3 Momentum Equation and Pressure Scaling

Starting from the modified longitudinal momentum equation, we first substitute the dimensionless spatial coordinates and velocity components introduced above while retaining the dimensional modified pressure $p'$ and electric potential $\phi$, so that the effect of each transformation can be identified explicitly:

$$
\rho\left[ J_w U \frac{J_w}{L}\frac{\partial U}{\partial X} + J_w\left(\frac{l}{L}\right)V \frac{J_w}{l}\frac{\partial U}{\partial Y} \right] = -\frac{1}{L}\frac{\partial p'}{\partial X} + \mu\left(\frac{J_w}{L^2}\frac{\partial^2 U}{\partial X^2}\right) + \mu\left(\frac{J_w}{l^2}\frac{\partial^2 U}{\partial Y^2}\right) + \frac{\epsilon\kappa^2}{L}\psi\frac{d\phi}{dX}.
$$

Notice that the transverse velocity scale $J_w l/L$ combines with the transverse derivative scale $1/l$, yielding the same characteristic factor $J_w^2/L$ as the longitudinal convective term. Consequently, the two inertial contributions can be grouped together:

$$
\rho\frac{J_w^2}{L} \left( U\frac{\partial U}{\partial X} + V\frac{\partial U}{\partial Y} \right) = -\frac{1}{L}\frac{\partial p'}{\partial X} + \frac{\mu J_w}{l^2} \left( \frac{l^2}{L^2} \frac{\partial^2 U}{\partial X^2} + \frac{\partial^2 U}{\partial Y^2} \right) + \frac{\epsilon\kappa^2}{L} \psi\frac{d\phi}{dX}.
$$

We now introduce the dimensionless modified pressure and electric potentials through:

$$
p' = p_c\Pi, \qquad \psi = \zeta\Psi, \qquad \phi = \phi_c\widetilde{\Phi},
$$

where $p_c = P_{os,D}$ denotes the characteristic pressure scale consistent with the inlet pressure reference, and $\phi_c$ is the characteristic electric potential scale to be specified below. Substituting these definitions into the preceding equation yields:

$$
\rho\frac{J_w^2}{L} \left( U\frac{\partial U}{\partial X} + V\frac{\partial U}{\partial Y} \right) = -\frac{p_c}{L}\frac{\partial\Pi}{\partial X} + \frac{\mu J_w}{L^2} \frac{\partial^2 U}{\partial X^2} + \frac{\mu J_w}{l^2} \frac{\partial^2 U}{\partial Y^2} + \frac{\epsilon\kappa^2\zeta\phi_c}{L} \Psi\frac{d\widetilde{\Phi}}{dX}.
$$

Considering $\Pi = p'/P_{os,D}$ and defining the dimensionless parameters:

$$
Re = \frac{\rho J_w L}{\mu}, \qquad \xi = \frac{l}{L}, \qquad \alpha = \frac{P_{os,D} L}{\mu J_w}, \qquad \Pi_D = \alpha \xi^2,
$$

the inertial coefficient becomes $Re\xi^2$ and the pressure-gradient coefficient becomes $\Pi_D$. The axial viscous-diffusion coefficient is $\xi^2$; it is small for a slender channel, although the corresponding derivative vanishes exactly only after the fully developed flow assumption is imposed.

### A.4 Characteristic Streaming-Potential Scale

To normalize the electric body-force coefficient in the longitudinal momentum equation, we choose $\phi_c$ such that:

$$
\frac{\epsilon\kappa^2\zeta\phi_c l^2}{\mu J_w L} = 1.
$$

With $\delta = \kappa l$, this gives:

$$
\phi_c = \frac{\mu J_w L}{\epsilon\zeta\delta^2}, \qquad \widetilde{\Phi} = \frac{\phi}{\phi_c}.
$$

Because $\zeta$ can be negative, $\phi_c$ is a signed normalization factor. The dimensionless longitudinal momentum equation consequently becomes:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
Re\xi^2\left(U\frac{\partial U}{\partial X} + V\frac{\partial U}{\partial Y}\right) = -\Pi_D\frac{\partial\Pi}{\partial X} + \xi^2\frac{\partial^2 U}{\partial X^2} + \frac{\partial^2 U}{\partial Y^2} + \Psi\frac{d\widetilde{\Phi}}{dX}.
$$
</div>

### A.5 Transverse Momentum Equation

Substituting $v = J_w(l/L)V$ and $p' = P_{os,D}\Pi$ into the transformed transverse momentum equation yields:

$$
\rho\frac{J_w^2 l}{L^2}\left(U\frac{\partial V}{\partial X} + V\frac{\partial V}{\partial Y}\right) = -\frac{P_{os,D}}{l}\frac{\partial\Pi}{\partial Y} + \frac{\mu J_w l}{L^3}\frac{\partial^2 V}{\partial X^2} + \frac{\mu J_w}{L l}\frac{\partial^2 V}{\partial Y^2}.
$$

Dividing by $\mu J_w/(L l)$ and using the dimensionless parameters defined above, we obtain:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
Re\xi^2\left(U\frac{\partial V}{\partial X} + V\frac{\partial V}{\partial Y}\right) = -\alpha\frac{\partial\Pi}{\partial Y} + \xi^2\frac{\partial^2 V}{\partial X^2} + \frac{\partial^2 V}{\partial Y^2}.
$$
</div>

The distinct coefficients $\Pi_D$ and $\alpha$ arise because the longitudinal and transverse equations are normalized by their respective transverse viscous-force scales.

### A.6 Electric-Double-Layer Potential

From the Debye–Hückel solution for the electric double layer:

$$
\psi(y) = \zeta\frac{\cosh(\kappa y)}{\cosh(\kappa l)}.
$$

Using $y = lY$, $\psi = \zeta\Psi$, and $\delta = \kappa l$ gives:

$$
\Psi(Y) = \frac{\cosh(\delta Y)}{\cosh(\delta)}, \qquad \Psi(\pm 1) = 1.
$$

### A.7 Electric-Current Conservation

Starting from the linearized electric-current conservation relation:

$$
\epsilon\kappa^2\int_{-l}^{l} u(x,y)\psi(y)\,dy + 2l\sigma_\infty\frac{d\phi}{dx} = 0,
$$

we substitute $u = J_w U$, $\psi = \zeta\Psi$, $dy = l\,dY$, and $\phi = \phi_c\widetilde{\Phi}$ to obtain:

$$
0 = \epsilon\kappa^2 J_w\zeta l \int_{-1}^{1} U(X,Y)\Psi(Y)\,dY + \frac{2l\sigma_\infty\phi_c}{L} \frac{d\widetilde{\Phi}}{dX}.
$$

Solving for the dimensionless streaming-potential gradient:

$$
\frac{d\widetilde{\Phi}}{dX} = -\frac{\epsilon\kappa^2 J_w\zeta L}{2\sigma_\infty\phi_c} \int_{-1}^{1} U(X,Y)\Psi(Y)\,dY.
$$

Substituting the expression for $\phi_c$ yields:

$$
\frac{\epsilon\kappa^2 J_w\zeta L}{2\sigma_\infty\phi_c} = \frac{\epsilon^2\zeta^2\kappa^2\delta^2}{2\mu\sigma_\infty} = \Lambda\delta^2, \qquad \text{where } \Lambda = \frac{\epsilon^2\zeta^2\kappa^2}{2\mu\sigma_\infty}.
$$

Therefore:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\frac{d\widetilde{\Phi}}{dX} = -\Lambda\delta^2\int_{-1}^{1} U(X,Y)\Psi(Y)\,dY.
$$
</div>

The negative sign follows from the current-balance convention adopted in the model.

### A.8 Dimensionless Volumetric-Flow Constraint

The volumetric flow rate satisfies:

$$
Q = w\int_{-l}^{l} u(x,y)\,dy = 2wlJ_w.
$$

Substituting $u = J_w U$ and $dy = l\,dY$ gives:

$$
2wlJ_w = wlJ_w\int_{-1}^{1} U(X,Y)\,dY \implies \int_{-1}^{1} U(X,Y)\,dY = 2,
$$

so that the dimensionless mean longitudinal velocity equals unity.

### A.9 Recovery of the Physical Pressure

The modified-pressure definition gives:

$$
p = p' + \frac{\epsilon\kappa^2}{2}\psi^2.
$$

Using $p' = P_{os,D}\Pi$ and $\psi = \zeta\Psi$ yields:

$$
\frac{p}{P_{os,D}} = \Pi + \Pi_E\Psi^2(Y), \qquad \text{where } \Pi_E = \frac{\epsilon\kappa^2\zeta^2}{2P_{os,D}}.
$$

The physical pressure therefore includes a transverse electrostatic contribution even when the modified pressure depends only on $X$.

### A.10 Dimensionless Boundary Conditions

Finally, the physical boundary conditions become:

$$
U(X,\pm 1) = 0, \qquad V(X,\pm 1) = 0, \qquad \widetilde{\Phi}(0) = 0, \qquad \Pi(0,Y) = 1.
$$

In particular, $\Pi(0,Y) = 1$ specifies the *modified* pressure at the inlet. It does not impose a uniform physical pressure there; instead, it gives $p(0,y) = P_{os,D} + \epsilon\kappa^2\psi^2(y)/2$. This inlet pressure condition is a modeling assumption rather than a direct consequence of the osmotic-flux law. No fully developed flow assumption has been imposed in the nondimensionalization itself; the subsequent simplifications for steady, unidirectional, fully developed flow are addressed in Appendix C.

---

## Appendix B: Derivation of the Dimensionless Physical Pressure

The purpose of this appendix is to derive the dimensionless physical pressure relation starting from the modified pressure definition. Rearranging the definition of $p'(x,y)$, the physical pressure can be expressed as:

$$
p(x,y) = p'(x,y) + \frac{\epsilon\kappa^2}{2} [\psi(y)]^2.
$$

Using the dimensionless scalings $\Pi(X,Y) = p'(x,y)/P_{os,D}$, $\Psi(Y) = \psi(y)/\zeta$, and defining the dimensionless physical pressure $\Pi_R = p(x,y)/P_{os,D}$, we can rewrite them as:

$$
p'(x,y) = P_{os,D}\Pi(X,Y), \qquad p(x,y) = P_{os,D}\Pi_R(X,Y), \qquad \psi(y) = \zeta\Psi(Y).
$$

Substituting these relations into the expression for $p(x,y)$ and dividing both sides by $P_{os,D}$ gives:

$$
\Pi_R(X,Y) = \Pi(X,Y) + \frac{\epsilon\zeta^2\kappa^2}{2P_{os,D}} [\Psi(Y)]^2.
$$

The factor multiplying $[\Psi(Y)]^2$ corresponds to the dimensionless electrostatic pressure parameter $\Pi_E$, yielding:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
\Pi_R(X,Y) = \Pi(X,Y) + \Pi_E [\Psi(Y)]^2.
$$
</div>

Under the fully developed flow assumption, the transverse momentum balance implies that the modified pressure is independent of the transverse coordinate, so that $\Pi(X,Y) = \Pi(X)$.

It is important to emphasize that the transverse uniformity of the modified pressure does not imply the transverse uniformity of the physical pressure. Indeed, differentiating $p(x,y)$ with respect to $y$ yields:

$$
\frac{\partial p}{\partial y} = \frac{\partial p'}{\partial y} + \epsilon\kappa^2\psi(y)\frac{d\psi(y)}{dy}.
$$

Since $\partial p'/\partial y = 0$ under the fully developed flow assumptions, it follows that:

$$
\frac{\partial p}{\partial y} = \epsilon\kappa^2\psi(y)\frac{d\psi(y)}{dy}.
$$

Thus, the physical pressure generally retains a transverse dependence associated with the electric double layer, even though the modified pressure depends only on the longitudinal coordinate. Finally, using the Debye–Hückel potential distribution, the dimensionless physical pressure can be written explicitly as:

$$
\Pi_R(X,Y) = \Pi(X) + \Pi_E \frac{\cosh^2(\delta Y)}{\cosh^2\delta}.
$$

This expression shows that the electrostatic contribution to the physical pressure is nonuniform across the channel and reaches its maximum at the walls, where $\Psi(\pm 1) = 1$.

---

## Appendix C: Fully Developed Flow and Simplification of the Governing Equations

The purpose of this appendix is to provide a detailed justification of the simplifications introduced for the dimensionless governing equations under the assumption of steady, unidirectional, fully developed flow.

### C.1 Kinematic Consequences of Fully Developed Flow

Starting from the dimensionless continuity equation, for a steady, fully developed flow in a straight microchannel, the longitudinal velocity profile does not change along the axial direction $\hat{\mathbf{x}}$. Therefore, $U(X,Y) = U(Y)$, which implies $\partial U/\partial X = 0$. By virtue of the continuity equation, we obtain:

$$
\frac{\partial V}{\partial Y} = 0.
$$

Integrating with respect to $Y$ yields $V(X,Y) = C_1(X)$, where $C_1(X)$ is an arbitrary function of the longitudinal coordinate. However, the impermeability conditions at the silica walls require $V(X,-1) = V(X,1) = 0$. Therefore, $C_1(X) = 0$, from which it follows that:

$$
V(X,Y) = 0 \implies \mathbf{U}(X,Y) = U(Y)\,\hat{\mathbf{x}}.
$$

This shows that $V(X,Y) = 0$ is not imposed independently; rather, it follows directly from the fully developed longitudinal velocity profile, the continuity equation, and the impermeability of the channel walls.

### C.2 Simplification of the Longitudinal Momentum Equation

Since $U = U(Y)$ and $V(X,Y) = 0$, we have:

$$
\frac{\partial U}{\partial X} = 0, \qquad \frac{\partial^2 U}{\partial X^2} = 0, \qquad V\frac{\partial U}{\partial Y} = 0.
$$

Combining these results, both the convective acceleration and the longitudinal viscous diffusion term vanish identically:

$$
U\frac{\partial U}{\partial X} + V\frac{\partial U}{\partial Y} = 0, \qquad \xi^2\frac{\partial^2 U}{\partial X^2} = 0.
$$

These identities are exact consequences of the assumed velocity field; in particular, they do not require taking the asymptotic limits $Re \to 0$ or $\xi \to 0$. The transverse viscous diffusion term remains nonzero ($\partial^2 U/\partial Y^2 = d^2 U/dY^2$), so the longitudinal momentum equation reduces to:

$$
0 = -\Pi_D\frac{\partial\Pi}{\partial X} + \frac{d^2 U}{dY^2} + \Psi(Y)\frac{d\widetilde{\Phi}}{dX}.
$$

### C.3 Simplification of the Transverse Momentum Equation

Repeating the procedure for the dimensionless transverse momentum equation, since $V(X,Y) = 0$ throughout the fully developed region, all of its spatial derivatives vanish:

$$
\frac{\partial V}{\partial X} = \frac{\partial V}{\partial Y} = \frac{\partial^2 V}{\partial X^2} = \frac{\partial^2 V}{\partial Y^2} = 0.
$$

Substituting into the transverse momentum equation gives:

$$
0 = -\alpha\frac{\partial\Pi}{\partial Y} \implies \frac{\partial\Pi}{\partial Y} = 0,
$$

since $\alpha = P_{os,D} L / (\mu J_w)$ is nonzero for the physical parameters considered. Thus, the modified pressure depends only on the longitudinal coordinate, $\Pi(X,Y) = \Pi(X)$, and accordingly:

$$
\frac{\partial\Pi}{\partial X} = \frac{d\Pi}{dX}.
$$

### C.4 Reduction of the Electrokinetic Relations

The dimensionless electric-current conservation relation is:

$$
\frac{d\widetilde{\Phi}}{dX} = -\Lambda\delta^2 \int_{-1}^{1} U(X,Y)\Psi(Y)\,dY.
$$

Since $U(X,Y) = U(Y)$ and $\Psi(Y)$ is independent of $X$, the integral on the right-hand side is constant along the fully developed region:

$$
\frac{d\widetilde{\Phi}}{dX} = -\Lambda\delta^2 \int_{-1}^{1} U(Y)\Psi(Y)\,dY = \mathrm{constant}.
$$

Thus, the dimensionless streaming potential varies linearly with the longitudinal coordinate. Using the boundary condition $\widetilde{\Phi}(0) = 0$, we obtain:

$$
\widetilde{\Phi}(X) = -\Lambda\delta^2 X \int_{-1}^{1} U(Y)\Psi(Y)\,dY.
$$

Likewise, the prescribed dimensionless flow-rate condition becomes:

$$
\int_{-1}^{1} U(Y)\,dY = 2,
$$

which is consistent with the longitudinal invariance of the velocity profile and expresses conservation of the volumetric flow rate along the microchannel.

### C.5 Final Reduced Governing Equation

Combining the reduced longitudinal momentum balance with $\partial\Pi/\partial X = d\Pi/dX$ and substituting the streaming-potential gradient yields the final reduced governing integro-differential equation:

<div style="background:#f7f7f7; padding:15px; border-left:4px solid #4a90e2; border-radius:6px; margin:20px 0;">
$$
0 = -\Pi_D\frac{d\Pi}{dX} + \frac{d^2 U}{dY^2} - \Lambda\delta^2\Psi(Y) \int_{-1}^{1} U(s)\Psi(s)\,ds.
$$
</div>

An additional consequence follows from the longitudinal structure of this equation. Because $U$ and $\Psi$ depend only on $Y$, all terms except the modified pressure gradient are independent of $X$. Therefore, the equality can hold throughout the fully developed region only if:

$$
\frac{d\Pi}{dX} = G,
$$

where $G$ is a constant. Integrating with respect to $X$ and imposing the prescribed inlet condition $\Pi(0) = 1$, we obtain:

$$
\Pi(X) = 1 + GX.
$$

Thus, the fully developed assumption implies a constant modified pressure gradient and a linear modified pressure distribution, establishing the mathematical basis for the reduced integro-differential formulation developed in the main text.