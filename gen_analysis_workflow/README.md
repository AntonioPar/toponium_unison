# Generator-Level Analysis Workflow  
## Toponium vs Inclusive $t\bar{t}$ Background

This document defines a complete scientific workflow for a generator-level (truth-level) analysis using only the `GenParticle` branch from Delphes ROOT files.

The goal is to compare:

- Signal: $pp \to \text{toponium} \to t\bar{t}$
- Background: $pp \to t\bar{t}$ (inclusive QCD)

This workflow is suitable for a phenomenological publication.

---

# 1. Input Data

We use only the `GenParticle` branch of the Delphes ROOT file.

Each particle provides:

- `PID`
- `Status`
- $E$
- $p_x, p_y, p_z$
- $M$
- Mother indices $(M1, M2)$
- Daughter indices $(D1, D2)$

All observables are constructed from these quantities.

---

# 2. Identification of Top Quarks

Select particles with:

- $PID = 6$ (top)
- $PID = -6$ (anti-top)

Use final-state tops (depending on generator convention, e.g. `Status = 22`).

Define 4-vectors:

- $p_t^\mu = (E_t, \vec{p}_t)$
- $p_{\bar{t}}^\mu = (E_{\bar{t}}, \vec{p}_{\bar{t}})$

---

# 3. Reconstruction of the $t\bar{t}$ System

Define the total 4-momentum:

$P_{t\bar{t}}^\mu = p_t^\mu + p_{\bar{t}}^\mu$

## 3.1 Invariant Mass

$M_{t\bar{t}}^2 = P_{t\bar{t}}^\mu P_{t\bar{t},\mu}$

$M_{t\bar{t}} = \sqrt{(E_t + E_{\bar{t}})^2 - |\vec{p}_t + \vec{p}_{\bar{t}}|^2}$

Physics expectation:

- Inclusive QCD → broad continuum
- Toponium → resonance-like enhancement

---

# 4. Partonic Center-of-Mass Energy

Define:

$\hat{s} = (p_t + p_{\bar{t}})^2$

Compare:

$d\sigma/d\hat{s}$

Threshold condition:

$\hat{s} \ge 4m_t^2$

---

# 5. Kinematic Observables

## 5.1 Transverse Momentum

$p_T = \sqrt{p_x^2 + p_y^2}$

Study:

$d\sigma/dp_T^t$

Bound-state production may produce softer spectra.

---

## 5.2 Rapidity

$y = \frac{1}{2} \ln \left( \frac{E + p_z}{E - p_z} \right)$

Define:

$\Delta y = y_t - y_{\bar{t}}$

Centrality differences may appear between signal and background.

---

# 6. Angular Distributions

## 6.1 Scattering Angle in $t\bar{t}$ Rest Frame

Boost into the $t\bar{t}$ rest frame.

Define:

$\cos\theta^* = \frac{\vec{p}_t^{\,*} \cdot \hat{z}}{|\vec{p}_t^{\,*}|}$

Compare:

$d\sigma/d\cos\theta^*$

QCD expectation:

$\sim 1 + \cos^2\theta$

Resonant state:

$\sim \sin^2\theta$

This is a strong discriminator.

---

# 7. Threshold Variable

Define the top velocity:

$\beta = \sqrt{1 - \frac{4m_t^2}{\hat{s}}}$

Near threshold:

$\beta \to 0$

Plot:

$d\sigma/d\beta$

Toponium is expected to enhance near threshold.

---

# 8. Initial-State Parton Analysis

From proton daughters, define approximate Bjorken fractions:

$x = \frac{E_{\text{parton}}}{E_{\text{beam}}}$

Construct:

$dN/dx$

and possibly

$d^2N/dx_1 dx_2$

Signal may prefer larger $x$ values.

---

# 9. Spin Correlations (Optional Advanced Study)

Using decay chains:

$t \to W^+ b$

Define angles $\theta_1, \theta_2$ between decay products and spin axis.

Correlation form:

$\frac{1}{\sigma} \frac{d^2\sigma}{d\cos\theta_1 d\cos\theta_2}
=
\frac{1}{4}(1 - C \cos\theta_1 \cos\theta_2)$

Compare spin correlation coefficient $C$.

---

# 10. Statistical Discrimination

For an observable $O$:

Define histograms:

$S_i = $ signal bin content  
$B_i = $ background bin content  

Likelihood ratio:

$\ln \Lambda = \sum_i n_i \ln \frac{S_i}{B_i}$

Compute:

- ROC curve
- AUC
- Kolmogorov–Smirnov test
- $\chi^2$ separation

---

# 11. Differential Cross Sections

If generator weights $w_i$ are available:

$d\sigma/dO = \frac{1}{\mathcal{L}} \frac{dN}{dO}$

Possible publishable distributions:

- $d\sigma/dM_{t\bar{t}}$
- $d\sigma/d\cos\theta^*$
- $d\sigma/d\beta$
- $d\sigma/dp_T$

---

# 12. Minimal Publishable Core Analysis

A scientifically solid minimal study includes:

1. $M_{t\bar{t}}$ distribution  
2. $\hat{s}$ distribution  
3. $\beta$ threshold behavior  
4. $\cos\theta^*$ angular structure  
5. $p_T^t$ spectrum  
6. $x$ initial-state fraction  
7. Likelihood-based discrimination  

---

# 13. Scientific Structure for Publication

## Section 1 — Theory Motivation  
Toponium bound-state motivation.

## Section 2 — Generator Setup  
Monte Carlo configuration.

## Section 3 — Observable Definitions  
Formal definitions of all observables.

## Section 4 — Differential Distributions  
Comparison between signal and background.

## Section 5 — Statistical Separation  
Quantitative discrimination power.

## Section 6 — Conclusions  

---

# 14. Important Note

This is a **truth-level phenomenological analysis**.

Detector simulation is not required for:

- Theoretical shape comparisons
- Angular structure studies
- Threshold behavior analysis
- Likelihood discrimination

Such studies are standard in phenomenology journals (e.g., EPJC, JHEP, PRD).

---

# End of Workflow
