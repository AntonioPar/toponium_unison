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


$w_k = \frac{\sigma_d \, L}{W_{\text{gen},d}} \, w_k^{\text{gen}}$


Check:


$\sum_k w_k \approx \sigma_d \, L$


---

# C) DEFINE RECONSTRUCTED REGION $R$

Implement dilepton selection:

- exactly 2 leptons (OS)
- $N_j \ge 2$
- $N_b \ge 1$
- Z-veto for same flavor
- MET cut (if needed)

Apply:


$d \cap R$

Compute yields:


$N_{d,R} = \sum_{k \in d \cap R} w_k$

---

# D) VALIDATE DILEPTON PURITY (INCLUSIVE ONLY)

Compute non-dileptonic contamination:


$f_{\text{non-}\ell\ell}(B) = \frac{\sum_{k \in B_{\text{incl}} \cap R,\ \text{truth}\neq \ell\ell} w_k}{\sum_{k \in B_{\text{incl}} \cap R} w_k}$


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


$S_{\ell\ell} \cap R \quad \text{vs} \quad B_{\ell\ell} \cap R$


Validation set:


$S_{\text{incl}} \cap R,\quad B_{\text{incl}} \cap R$


Check sculpting of $m_{t\bar t}$.

---

# G) BUILD TEMPLATES (NOMINAL = INCLUSIVE)

Choose fit variables:

- $(m_{t\bar t}, \text{NN score})$

Construct binned templates:


$s_i = \sum_{k \in S_{\text{incl}} \cap R \cap i} w_k$



$b_i = \sum_{k \in B_{\text{incl}} \cap R \cap i} w_k$


---

# H) STATISTICAL INFERENCE

Likelihood model:


$n_i \sim \text{Pois}(\mu s_i + b_i)$


Extract:

- $\hat{\mu}$
- $\Delta\mu$

Perform closure and signal injection tests.

---

# K) FINAL DELIVERABLES

- Production cross sections
- Partonic distributions and generator level analysis
- Detector level observables
- NN performance plots
- Template fit and likelihood scan
- Final measurement: $\hat{\mu} \pm \Delta\mu$

---

