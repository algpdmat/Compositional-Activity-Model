
# Compositional Data Analysis of Time-Use (CoDA 600–1440 min)

## Overview

This repository implements a complete Python pipeline for **Compositional Data Analysis (CoDA)** applied to **time-use data** in behavioral epidemiology.
It supports both **600-minute** and **1440-minute** frameworks, representing school-day and full-day contexts, respectively.

The analysis is based on the **isometric log-ratio (ILR) transformation** proposed by **Aitchison (1982, 1986)** and later applied to movement behavior by **Dumuid et al. (2020, 2021)**, **Chastin et al. (2015)**, and collaborators.

The model allows estimation of:

* Relative influences of **Sleep**, **Sedentary Behavior (SB)**, **Light Physical Activity (LPA)**, and **Moderate-to-Vigorous Physical Activity (MVPA)** on health outcomes.
* **Isotemporal reallocations**, i.e., simulated substitutions of minutes between behaviors.
* **Graphical and 3D visualizations** of predicted changes across the compositional space.



## Visualization

The script generates several outputs:

1. **Compositional Means Barplot**
   Displays average daily time-use distribution.

2. **Isotemporal Reallocation Curves**
   For each outcome, simulates ±30-minute reallocations between all pairs of behaviors.

3. **3D Surfaces**
   Displays smooth predictive surfaces where two behaviors vary simultaneously and others adjust to maintain closure.

All plots are rendered using **Matplotlib** and **Seaborn**.

---

## Workflow

1. **Input**:
   Upload `.xlsx` or `.sav` file interactively. The script automatically detects encoding and cleans NaN or zero values.

2. **Choose Model Type**:

   * `600` minutes (school-day composition: SB, LPA, MVPA)
   * `1440` minutes (full-day composition: Sleep, SB, LPA, MVPA)

3. **Execution**:
   Runs full ILR-based regression models, isotemporal simulations, and visual outputs.

4. **Output**:

   * Summary tables and ANOVA
   * Realocation plots and surfaces
   * Optional export to Excel for simulated results

---

## Mathematical Rationale

Because compositional data live on a simplex, differences are **relative**, not absolute.
Thus, interpretations are made in terms of **reallocation effects** — e.g., replacing 30 minutes of SB with 30 minutes of MVPA.

Key properties:

* **Subcompositional coherence**
  Results are invariant to removal of parts.
* **Scale invariance**
  Multiplying all parts by a constant does not change the analysis.
* **Permutation invariance**
  Order of components does not affect the ILR transformation.

---

## References

1. Aitchison, J. (1982). *The Statistical Analysis of Compositional Data*. Journal of the Royal Statistical Society B, 44(2), 139–177.
2. Aitchison, J. (1986). *The Statistical Analysis of Compositional Data*. Chapman & Hall.
3. Dumuid, D. et al. (2020). *The Goldilocks Day for Children’s Skeletal Health: Compositional Data Analysis*. Journal of Bone and Mineral Research, 35(12), 2324–2333.
4. Dumuid, D. et al. (2021). *Physical activity, sleep and sedentary behavior: Compositional data analysis in movement research*. International Journal of Environmental Research and Public Health, 17(2220).
5. Chastin, S. F. M., Palarea-Albaladejo, J., Dontje, M. L., & Skelton, D. A. (2015). *Combined effects of time spent in physical activity, sedentary behaviors and sleep on obesity and cardio-metabolic health markers: A compositional data analysis approach*. PLoS ONE, 10(10): e0139984.

---

## Citation

If you use this code, please cite: PACHECO, A.L.G.



