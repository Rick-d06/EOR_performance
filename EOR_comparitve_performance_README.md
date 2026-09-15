# Enhanced Oil Recovery (EOR) Screening & Economic Simulator

A Python-based reservoir engineering simulation model that evaluates and compares production performance, cumulative recovery factors ($RF$), and incremental project economics across secondary and tertiary displacement mechanisms.

---

## Overview

The simulator models fluid flow and displacement efficiency in an oil-bearing reservoir, comparing baseline waterflooding against two primary Enhanced Oil Recovery (EOR) techniques implemented after 3 years of secondary production:

1. **Base Case — Waterflooding:** Governed by an unfavorable mobility ratio ($M > 1$) with baseline viscous fingering and residual oil saturation ($S_{orw} = 0.30$).
2. **Chemical EOR — Polymer Flooding:** Viscosifies the injected water phase from $0.8\text{ cp}$ to $8.0\text{ cp}$, significantly reducing the mobility ratio, improving areal and vertical sweep efficiency, and mitigating early water breakthrough.
3. **Gas EOR — Miscible $\text{CO}_2$ Injection:** Establishes multiple-contact miscibility (MCM) to lower interfacial tension, swell remaining oil, and achieve a low residual oil saturation ($S_{orc} = 0.12$).

---

## Reservoir & Fluid Characterization

| Parameter | Symbol | Value | Unit |
|---|---|---|---|
| Drainage Area | $A$ | 640 | acres |
| Net Pay Thickness | $h$ | 50 | ft |
| Porosity | $\phi$ | 22 | % |
| Initial Water Saturation | $S_{wi}$ | 25 | % |
| Permeability | $k$ | 120 | mD |
| Oil Formation Volume Factor | $B_o$ | 1.25 | RB/STB |
| Live Oil Viscosity | $\mu_o$ | 15.0 | cp |
| Formation Water Viscosity | $\mu_w$ | 0.8 | cp |
| Viscosified Polymer Viscosity | $\mu_p$ | 8.0 | cp |
| Original Oil in Place (OOIP) | — | **~26.86** | MMSTB |

---

## Methodology & Formulation

* **Volumetrics (OOIP):**
  $$\text{OOIP (STB)} = \frac{7758 \times A \times h \times \phi \times (1 - S_{wi})}{B_o}$$

* **Fractional Flow Theory:**
  Implements Corey-style normalized water saturation ($S_w^*$) to compute phase relative permeabilities ($k_{rw}, k_{ro}$) and mobility ratio $M$:
  $$f_w = \frac{1}{1 + \left(\frac{k_{ro}}{k_{rw}}\right) \left(\frac{\mu_w}{\mu_o}\right)}$$

* **Recovery Profiles:**
  Empirical exponential recovery dynamics calibrated to theoretical maximum displacement targets:
  $$RF(t) = RF_{\max} \cdot \left(1 - e^{-\lambda t}\right)$$

* **Economic Screening:**
  Calculates gross project revenue based on benchmark oil price ($\$75/\text{bbl}$), accounting for differential CAPEX and OPEX adders to determine net economic gain over secondary waterflooding.

---

## Installation & Requirements

Ensure you have Python 3.8+ installed, then install the dependencies:

```bash
pip install numpy pandas matplotlib
