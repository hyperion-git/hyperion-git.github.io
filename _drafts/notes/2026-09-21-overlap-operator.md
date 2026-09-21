---
title: The overlap operator and the path-integral picture of atom interferometry
date: 2026-09-21
description: What an atom interferometer measures, why the relative evolution of the two arms is the object that carries the phase, how the Feynman path integral reproduces it, and why the familiar split into propagation, laser and separation phases is not invariant.
tags: [atom interferometry, path integral, derivation]
---

An atom interferometer does not measure a phase. It measures populations in its output ports, and the phase is what we extract from them. Keeping this in mind settles a number of questions that otherwise lead to long discussions: which operator carries the phase, in which direction it is to be read, and whether the classical action along the two arms is the whole story. In the following we go through the chain from the detected signal to the interference phase once, first in operator language and then in the path-integral language of Storey and Cohen-Tannoudji [[1]](#ref1), and we show where the two agree and where the path integral has to be read with care. The presentation condenses the corresponding chapters of the handbook of `fringe`, our operator-algebra engine for light-pulse interferometers; the conventions are those of Ufrecht [[2]](#ref2) and of my thesis [[3]](#ref3).

## Conventions

We work in one dimension with the vertical axis pointing upward, so that the Hamiltonian of an atom of mass $m$ in uniform gravity reads

$$
\hat H=\frac{\hat p^{2}}{2m}+mg\hat x ,
$$

and the classical acceleration is $-g$. A light pulse at time $t_\ell$ with wave vector $k$ and laser phase $\phi$ acts as the kick operator $\exp[i(k\hat x+\phi)]$, which transfers the momentum $+\hbar k$; its conjugate has both $k$ and $\phi$ negated. Between pulses each arm evolves under the time-ordered exponential

$$
U_j(t_f,t_i)=\mathcal T\exp\left[-\frac{i}{\hbar}\int_{t_i}^{t_f}dt\,\hat H_j(t)\right],\qquad j=A,B ,
$$

where time ordering places later operations to the left. The arm propagator $U_j$ is the product of free-evolution and kick operators in chronological order, later factors to the left. Arm A is the reference arm; arm B is the arm that receives the first kick.

## What Is Measured

Let $\rho_0$ be the prepared state and $E_a$ the detector effect for outcome $a$, say a position bin. A beam-splitter readout mixes the two arms into the ports $T_\pm=\tfrac12\left(U_A\pm e^{i\varphi}U_B\right)$ with a scanned readout phase $\varphi$, and the joint port-and-position probability is

$$
p_\pm(a;\varphi)=\frac14\left[n_A(a)+n_B(a)\pm2\operatorname{Re}\!\left(e^{i\varphi}z(a)\right)\right],
$$

with the single-arm densities $n_j(a)=\operatorname{Tr}\left(E_aU_j\rho_0U_j^{\dagger}\right)$ and the complex cross term

$$
z(a)=\operatorname{Tr}\!\left(E_aU_B\rho_0U_A^{\dagger}\right)=|z(a)|\,e^{i\Phi(a)} .
$$

Everything one calls "the interferometer phase" is the argument $\Phi(a)$ of this cross term, and everything one calls "the contrast" is its modulus. Note that $z(a)$ depends on the state and on the detector; a finite detector resolution changes the observable, and replacing $E_a$ by the identity gives a different number.

## The Overlap Operator

The cross term contains the two arm propagators only in the combination $U_A^{\dagger}E_aU_B$, sandwiched by the input state. Using the cyclic property of the trace and the unitarity of the arms we can equally refer everything to the output state of the reference arm, $\rho_A=U_A\rho_0U_A^{\dagger}$:

$$
z(a)=\operatorname{Tr}\!\left(E_a\,U_{\mathrm{rel}}\,\rho_A\right),\qquad U_{\mathrm{rel}}=U_BU_A^{\dagger} .
$$

We call $U_{\mathrm{rel}}$ the overlap operator, or relative evolution: it is the operator that takes the state as arm A delivers it to the detector and turns it into the state arm B delivers. For a pure state the cross term is $\langle\psi_A\vert E_aU_{\mathrm{rel}}\vert \psi_A\rangle$, and for ideal imaging it is simply $\psi_A(a)^{\ast}\psi_B(a)$. Two remarks are in order. First, the direction matters: reversing A and B conjugates $z(a)$ and flips the sign of the phase. Second, $U_BU_A^{\dagger}$ and $U_A^{\dagger}U_B$ are different operators. They are related by conjugation with $U_A$, and for a closed interferometer, where the two arms end at the same phase-space point, the two agree. For an open interferometer they differ in both modulus and phase, because the conjugation moves a c-number, the symplectic area between the residual separation and the reference trajectory, into the phase slot. The phase of an open interferometer is therefore only defined once the frame it is referred to is named alongside it.

If the relative evolution happens to be a pure phase, $U_{\mathrm{rel}}=e^{i\Delta\phi}\mathbb 1$, then $z(a)=e^{i\Delta\phi}n_A(a)$ and the port populations reduce to the textbook fringe $P_\pm(\varphi)=\tfrac12[1\pm\cos(\varphi+\Delta\phi)]$. This is the only situation in which a scalar phase is a property of the interferometer alone. In every other situation the invariant object is $U_{\mathrm{rel}}$, and a scalar is obtained only by taking an expectation value in a state.

## The Path-Integral Picture

Now insert position identities into the cross term. With the kernels $K_j(x,y)=\langle x\vert U_j\vert y\rangle$ and $\rho_0(y,y')=\langle y\vert \rho_0\vert y'\rangle$, and a detector that weights the final position with a resolution function $w_R(a-x)$, the same trace reads

$$
z_R(a)=\int dx\,dy\,dy'\;w_R(a-x)\,\rho_0(y,y')\,K_B(x,y)\,K_A(x,y')^{\ast} .
$$

The two arms share the final position $x$, where the detector looks, and the initial coherence is carried by the off-diagonal source kernel $\rho_0(y,y')$ with distinct launch points $y$ and $y'$. It should be remarked that this off-diagonal kernel cannot in general be replaced by a distribution of classical launch points; the interferometer is sensitive to the coherence of the source, not only to its density.

For a Hamiltonian with quadratic kinetic energy and a smooth potential each kernel has the Feynman representation

$$
K_j(x,y)=\int_{x_j(t_i)=y}^{x_j(t_f)=x}\mathcal Dx_j\;e^{i\mathcal S_j[x_j]/\hbar},\qquad
\mathcal S_j[x_j]=\int_{t_i}^{t_f}dt\,L_j(x_j,\dot x_j,t),
$$

with the time-sliced measure fixed by the operator kernel. A pair of paths in the cross term therefore carries the weight $\exp[i(\mathcal S_B[x_B]-\mathcal S_A[x_A])/\hbar]$, and an ideal laser kick contributes the factor $\exp[i(kx(t_\ell)+\phi)]$ evaluated at its interaction time. In the kernel language a pulse is the distribution $K_P(x,y)=e^{i(kx+\phi)}\delta(x-y)$: it adds $\hbar(kx+\phi)$ to the action at the joining point and does not move the atom. Varying the joining point in the full action gives $p_{\mathrm{before}}-p_{\mathrm{after}}+\hbar k=0$, so the momentum jump is $+\hbar k$, in agreement with the operator convention above. This is the first place where the two pictures are tied together: the sign of the momentum transfer is not a separate convention of the path integral, it follows from the phase the pulse imprints.

### Expanding Around a Reference Path

Write every path as $x=r+\eta$ with a reference trajectory $r(t)$ and a fluctuation $\eta(t)$. For $L=m\dot x^{2}/2-V(x,t)$ the action expands as

$$
\begin{aligned}
\mathcal S[r+\eta]={}&\mathcal S[r]+\left[m\dot r\,\eta\right]_{t_i}^{t_f}
+\int dt\,\left[-m\ddot r-V'(r,t)\right]\eta\\
&+\frac12\int dt\,\left[m\dot\eta^{2}-V''(r,t)\,\eta^{2}\right]+\mathcal R_{\mathcal S}[\eta] .
\end{aligned}
$$

The bulk linear term vanishes when $r$ is a classical trajectory. The boundary term vanishes only if $\eta$ vanishes at both ends, which is the case for the stationary path that connects the endpoints of one particular kernel. A packet-centroid trajectory, however, does not connect every pair of endpoints $(y,x)$ that appears in the cross term, so in general its boundary terms survive and must be combined with the source, detector and pulse phases. This is the point where the naive recipe, phase equals action difference divided by $\hbar$, silently assumes more than it states.

Keeping the quadratic sector and dropping the remainder $\mathcal R_{\mathcal S}$, one classical saddle away from a caustic gives

$$
K(x,y)\simeq\mathcal F_r\,e^{i\mathcal S[r]/\hbar},\qquad
\mathcal F_r=\int_{\eta(t_i)=\eta(t_f)=0}\mathcal D\eta\;e^{i\mathcal S^{(2)}_r[\eta]/\hbar},
$$

the Van Vleck form. The Gaussian fluctuation integral $\mathcal F_r$ is a determinant with its own normalization and phase branch; it describes spreading, focusing and the phase they generate. For a globally quadratic potential the remainder vanishes and this form is exact. Even then the cross term contains $\mathcal F_B\mathcal F_A^{\ast}$ together with the endpoint integrals, and its phase is in general not just the difference of two classical actions. In uniform gravity the one-dimensional kernel over a time $T$ can be written down in closed form,

$$
\mathcal S_{\mathrm{cl}}(x,y)=\frac{m(x-y)^{2}}{2T}-\frac{mgT(x+y)}{2}-\frac{mg^{2}T^{3}}{24},\qquad
K(x,y;T)=\sqrt{\frac{m}{2\pi i\hbar T}}\;e^{i\mathcal S_{\mathrm{cl}}(x,y)/\hbar},
$$

and one sees explicitly that the prefactor depends on the interval only. In the Mach–Zehnder sequence below both arms therefore share the same fluctuation evolution and its phase cancels at closure; for a different geometry, in particular when the two arms evolve under different Hamiltonians, this cancellation has to be established again.

## Quadratic Hamiltonians: The Overlap Operator in Closed Form

For quadratic Hamiltonians the operator picture becomes exact and finite. Every arm propagator factorises into a phase-space displacement and a metaplectic operator,

$$
U=D(d,A)\,M(S),\qquad D(d,A)=\exp\!\left[\frac{i}{\hbar}\left(A+d_p\hat x-d_x\hat p\right)\right],
$$

where $S$ is the symplectic matrix of the linearised classical flow, $d=(d_x,d_p)^{T}$ the displacement of the classical trajectory that starts at the origin, and $A$ a scalar action. On an interval of length $t$ the scalar obeys $\dot A=-V_0-\tfrac12 f^{T}\delta$ with the linear force $f$ and the driven path $\delta$, which integrates to

$$
A(t)=\int_0^{t}\left[p\,\dot q-H(q,p)\right]du-\tfrac12\,q(t)\,p(t) .
$$

In uniform gravity this is $A=mg^{2}t^{3}/12-V_0t$. Note that this central action is positive and is not the fixed-endpoint action $\mathcal S_{\mathrm{cl}}$ of the kernel above; the two differ by the boundary term $\tfrac12 qp$, which is exactly the term the packet-centroid argument of the previous section warned about. Intervals compose according to

$$
S_{21}=S_2S_1,\qquad d_{21}=d_2+S_2d_1,\qquad A_{21}=A_2+A_1-\tfrac12\,\Omega(d_2,S_2d_1),
$$

with the symplectic form $\Omega(u,v)=u^{T}Jv$, and a pulse is the displacement $d=(0,\hbar k)^{T}$ with $A=\hbar\phi$. The last term of the composition law is the symplectic area swept between the two displacements; it is the operator-algebra form of the boundary terms in the path integral, and it is the reason why the scalar of a sequence is not simply the sum of the scalars of its parts.

Combining arm B with the inverse of arm A, $(d,A,S)^{-1}=(-S^{-1}d,-A,S^{-1})$, gives the overlap operator in closed form:

$$
\begin{aligned}
U_{\mathrm{rel}}&=D(d,A_r)\,M(S_r),\\
S_r&=S_BS_A^{-1},\qquad d=d_B-S_rd_A,\qquad
A_r=A_B-A_A+\tfrac12\,\Omega(d_B,S_rd_A).
\end{aligned}
$$

The scalar phase that a detector at the centroid reports is then

$$
\begin{aligned}
\phi_c&=\frac1\hbar\left[A_r-\tfrac12\Omega(d,S_r\zeta_A)-\tfrac12\Omega(\sigma,\zeta_A)\right],\\
\zeta_A&=d_A+S_A\zeta_0,\qquad \sigma=d+(S_r-\mathbb 1)\zeta_A ,
\end{aligned}
$$

with the prepared phase-space centroid $\zeta_0$, the centroid $\zeta_A$ at which arm A arrives, and the separation $\sigma$ between the two arms at detection. For equal flows on both arms, $S_r=\mathbb 1$, this collapses to $\phi_c=[A_r-\Omega(d,\zeta_A)]/\hbar$. The two area terms are the frame dependence announced above: they vanish when the interferometer is closed, $d=0$, and they are the whole difference between $U_BU_A^{\dagger}$ and $U_A^{\dagger}U_B$ when it is not.

## The Mach–Zehnder Phase, Twice

Take the standard sequence with pulses at $0$, $T$ and $2T$, laser phases $\phi_1,\phi_2,\phi_3$, and let $v_r=\hbar k/m$ be the recoil velocity. Arm B receives $+\hbar k$ with phase $+\phi_1$ at $t=0$ and $-\hbar k$ with phase $-\phi_2$ at $t=T$; arm A receives $+\hbar k$ with phase $+\phi_2$ at $t=T$ and $-\hbar k$ with phase $-\phi_3$ at $t=2T$. With the unkicked trajectory $x_c(t)=x_0+v_0t-gt^{2}/2$ the two arms follow

$$
\begin{array}{c|cc}
 & 0\le t\le T & T\le t\le 2T\\ \hline
x_B(t) & x_c(t)+v_rt & x_c(t)+v_rT\\
x_A(t) & x_c(t) & x_c(t)+v_r(t-T)
\end{array}
$$

and both final centroids and momenta coincide, so the interferometer is closed.

*Route A, action and laser phases.* Integrating $m\dot x^{2}/2-mgx$ along each free interval and adding each laser phase at the kick position gives

$$
\mathcal S_B^{\mathrm{cl}}-\mathcal S_A^{\mathrm{cl}}=0,\qquad
k\left[x_B(0)-x_B(T)-x_A(T)+x_A(2T)\right]=-kgT^{2} .
$$

The classical actions of the two arms are equal, and the $x_0$, $v_0$ and recoil contributions cancel separately in the laser term. Since the interferometer is closed and both arms share the same fluctuation evolution, the endpoint and prefactor terms drop out as well, and the phase is

$$
\Phi_{\mathrm{MZ}}=\phi_1-2\phi_2+\phi_3-kgT^{2} .
$$

*Route B, transported displacements.* Alternatively, transport every kick to the final time with the classical flow, $c_j=S(t_f,t_j)\kappa_j$, collect the displacements and areas of each arm with the composition law above, and read off $A_r$ of the overlap operator. Each transported kick contributes its laser phase minus the symplectic area between the free-fall displacement of the reference over 0t_j,t_f] the kick itself; these areas add up to 0kgT^{2}1 The areas Omega(c_\ell,c_j) the transported kicks carry the recoil contributions, which cancel in this closed geometry. This second route is the one `fringe` implements; the first is the independent check it is tested against.

The sign deserves a comment, since the textbook form is usually quoted as $+k_{\mathrm{eff}}gT^{2}$. With the axis pointing upward, gravity accelerating downward, the kick $e^{+ikx}$ transferring $+\hbar k$ and the overlap read as $U_BU_A^{\dagger}$, the phase is negative. Flipping any one of these four choices flips the sign, and a closed symmetric Mach–Zehnder cannot tell the four apart: reversing both arm sequences is algebraically the same as swapping the arms and sending $k\to-k$. The sign is a property of the quadruple, not of any single convention.

## Beyond the Closed Loop

Two things change once the Hamiltonian acquires a gravity gradient $\Gamma$, $\hat H=\hat p^{2}/2m+mg\hat x+\tfrac12 m\Gamma\hat x^{2}$. The flows of the two arms are no longer equal, the loop opens, and the frame terms in $\phi_c$ become physical. To first order in $\Gamma$ and for $x_0=v_0=0$ the centroid phase becomes

$$
\Phi=\Phi_L-kgT^{2}+\Gamma\left[\frac{7}{12}kgT^{4}-\frac{\hbar k^{2}T^{3}}{2m}\right]+\mathcal O(\Gamma^{2}),\qquad \Phi_L=\phi_1-2\phi_2+\phi_3 ,
$$

which is Eq. (1.99) of Ufrecht [[2]](#ref2). The term proportional to $\hbar k^{2}$ is the recoil correction, and its sign relative to the classical $\tfrac{7}{12}kgT^{4}$ is the quantity that survives every overall rescaling of the phase. It is also the term that the naive action-difference recipe gets wrong unless the boundary terms are tracked, which is the practical reason for insisting on the overlap operator as the primary object. Roura, Zeller and Schleich [[4]](#ref4) discuss the resulting loss of contrast and how to overcome it; the perturbative operator approach of Ufrecht and Giese [[5]](#ref5) extends the construction to anharmonic potentials, where the metaplectic factorisation is no longer exact.

Finally, the conventional split of the phase into propagation, laser, separation and recoil contributions is useful but not invariant. Moving phase between the plane-wave carrier of a packet and its normalization, changing the interaction picture or the reference trajectory, all shift contributions between the named pieces while leaving the cross term $z(a)$ unchanged. The measurable object is $z(a)$, and for an open interferometer the invariant that produces it is the overlap operator together with the state it acts on; a bare scalar "phase" is well defined only once the loop is closed.

## References

<a id="ref1"></a>[1] P. Storey and C. Cohen-Tannoudji, *The Feynman path integral approach to atomic interferometry. A tutorial*, J. Phys. II France **4**, 1999 (1994). [doi:10.1051/jp2:1994103](https://doi.org/10.1051/jp2:1994103)

<a id="ref2"></a>[2] C. Ufrecht, *Theoretical approach to high-precision atom interferometry*, PhD thesis, Universität Ulm (2019). [doi:10.18725/OPARU-17923](https://doi.org/10.18725/OPARU-17923)

<a id="ref3"></a>[3] A. Friedrich, *Interference of Clocks: Atom Interferometry and Quantum Tests of Relativity*, PhD thesis, Universität Ulm (2024). [doi:10.18725/OPARU-53901](https://doi.org/10.18725/OPARU-53901)

<a id="ref4"></a>[4] A. Roura, W. Zeller and W. P. Schleich, *Overcoming loss of contrast in atom interferometry due to gravity gradients*, New J. Phys. **16**, 123012 (2014). [arXiv:1401.7699](https://arxiv.org/abs/1401.7699)

<a id="ref5"></a>[5] C. Ufrecht and E. Giese, *Perturbative operator approach to high-precision light-pulse atom interferometry*, Phys. Rev. A (2020). [arXiv:2003.02042](https://arxiv.org/abs/2003.02042)
