# Toponium-like Dilepton Analysis — COMPLETE TO-DO LIST  
(Delphes + NN + Combine + Partonic Study)

---

# A) INPUTS

Four MC samples:

- `B_incl`      : $pp \to t\bar t$ inclusive  
- `B_{\ell\ell}` : $pp \to t\bar t$ dileptonic-only  
- `S_{\text{incl}}` : $pp \to \text{toponium-like} \to t\bar t$ inclusive  
- `S_{\ell\ell}` : toponium-like dileptonic-only  

Target luminosity: $L$

For each sample $d$ extract:

- $\sigma_d$ (pb)
- generator weights $w_k^{\text{gen}}$
- total weight $W_{\text{gen},d} = \sum_k w_k^{\text{gen}}$

---

# B) MC NORMALIZATION

Define per-event physics weight:

\[
w_k = \frac{\sigma_d \, L}{W_{\text{gen},d}} \, w_k^{\text{gen}}
\]

Check:

\[
\sum_k w_k \approx \sigma_d \, L
\]

---

# C) DEFINE RECONSTRUCTED REGION $R$

Implement dilepton selection:

- exactly 2 leptons (OS)
- $N_j \ge 2$
- $N_b \ge 1$
- Z-veto for same flavor
- MET cut (if needed)

Apply:

\[
d \cap R
\]

Compute yields:

\[
N_{d,R} = \sum_{k \in d \cap R} w_k
\]

---

# D) VALIDATE DILEPTON PURITY (INCLUSIVE ONLY)

Compute non-dileptonic contamination:

\[
f_{\text{non-}\ell\ell}(B) =
\frac{\sum_{k \in B_{\text{incl}} \cap R,\ \text{truth}\neq \ell\ell} w_k}
{\sum_{k \in B_{\text{incl}} \cap R} w_k}
\]

Same for $S$.

---

# E) RECONSTRUCT PHYSICS OBSERVABLES

Inside $R$ compute:

- $m_{t\bar t}$
- $m_{\ell\ell}$
- $\Delta\phi_{\ell\ell}$
- MET
- optional spin observable $c_{\text{hel}}$

Store dataset:

- feature vector $x$
- label $y$
- weight $w_k$

---

# F) TRAIN NEURAL NETWORK

Training set:

\[
S_{\ell\ell} \cap R \quad \text{vs} \quad B_{\ell\ell} \cap R
\]

Validation set:

\[
S_{\text{incl}} \cap R,\quad B_{\text{incl}} \cap R
\]

Check sculpting of $m_{t\bar t}$.

---

# G) BUILD TEMPLATES (NOMINAL = INCLUSIVE)

Choose fit variables:

- $(m_{t\bar t}, \text{NN score})$

Construct binned templates:

\[
s_i = \sum_{k \in S_{\text{incl}} \cap R \cap i} w_k
\]

\[
b_i = \sum_{k \in B_{\text{incl}} \cap R \cap i} w_k
\]

---

# H) STATISTICAL INFERENCE

Likelihood model:

\[
n_i \sim \text{Pois}(\mu s_i + b_i)
\]

Extract:

- $\hat{\mu}$
- $\Delta\mu$

Perform closure and signal injection tests.

---

# I) PARTONIC STUDY (NEW SECTION)

Goal: Understand **which partons inside the proton produced the process** and how signal differs from background.

---

## I.1 Extract partonic initial state

From generator-level information (LHE or GenParticles):

For each event extract:

- incoming parton flavors $f_1, f_2$
- momentum fractions $x_1, x_2$
- factorization scale $Q$
- partonic invariant mass $\hat{s}$

Compute:

\[
\hat{s} = (p_1 + p_2)^2
\]

\[
x_{1,2} = \frac{\sqrt{\hat{s}}}{\sqrt{s}} e^{\pm y}
\]

where $y$ is rapidity of the $t\bar t$ system.

---

## I.2 Identify production channels

For each event classify:

- $gg \to t\bar t$
- $q\bar q \to t\bar t$
- $gq \to t\bar t + X$

Compute fractions:

\[
F_{gg} = \frac{\sum_{k \in gg} w_k}{\sum_k w_k}
\]

\[
F_{q\bar q} = \frac{\sum_{k \in q\bar q} w_k}{\sum_k w_k}
\]

Compare for:

- $B_{\text{incl}}$
- $S_{\text{incl}}$

---

## I.3 Study $x_1$, $x_2$ distributions

Plot weighted distributions:

\[
\frac{d\sigma}{dx_1},\quad \frac{d\sigma}{dx_2}
\]

Compare signal vs background.

Look for:

- threshold enhancement
- shift in $x$ region
- dominance of gluon PDF

---

## I.4 Study $\hat{s}$ near threshold

Plot:

\[
\frac{d\sigma}{d\hat{s}}
\]

Zoom near:

\[
\hat{s} \approx (2m_t)^2
\]

Check if toponium shows enhancement in:

\[
E = \sqrt{\hat{s}} - 2m_t
\]

---

## I.5 Compare partonic luminosities

Using PDFs $f_i(x,Q)$:

\[
\mathcal{L}_{ij}(\tau) =
\int dx_1 dx_2\, f_i(x_1,Q)\, f_j(x_2,Q)\,
\delta(x_1 x_2 - \tau)
\]

with:

\[
\tau = \frac{\hat{s}}{s}
\]

Study:

- gluon–gluon luminosity
- quark–antiquark luminosity

Evaluate dominance at threshold.

---

## I.6 Differential channel study inside $R$

Repeat channel fractions **after selection**:

\[
F_{gg}^{(R)},\quad F_{q\bar q}^{(R)}
\]

See how reconstruction biases partonic composition.

---

# J) OPTIONAL: NN INCLUDING PARTONIC FEATURES

Add as inputs:

- $x_1, x_2$
- channel label (encoded)
- $\hat{s}$

Train classifier at parton-level to understand physics separability.

---

# K) FINAL DELIVERABLES

- Cutflow tables
- Partonic channel fractions
- $x$ distributions (signal vs background)
- $\hat{s}$ distributions
- NN performance plots
- Template fit and likelihood scan
- Final measurement: $\hat{\mu} \pm \Delta\mu$

---

