
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

The script produces a comprehensive set of visual and analytical outputs:

1. **Compositional Means Barplot**
   Displays the average time-use distribution across all behaviors (e.g., Sleep, SB, LPA, MVPA for 1440-min or SB, LPA, MVPA for 600-min). This provides a clear overview of how the sample allocates time across daily activity domains.

2. **Isotemporal Reallocation Curves**
   For each health-related outcome, the model simulates ±30-minute reallocations between all possible pairs of behaviors, predicting how small changes in time distribution affect the dependent variable while maintaining the compositional constraint (sum = 1).

3. **3D Predictive Surfaces**
   Generates smooth surfaces where two behaviors vary simultaneously and the remaining components adjust proportionally to preserve closure. These surfaces reveal nonlinear and joint effects among behaviors on each outcome.

All figures are rendered with **Matplotlib** and **Seaborn**, ensuring clarity and reproducibility across environments.



## Workflow

1. **Input Stage**
   The user interactively uploads a `.xlsx` or `.sav` file. The function automatically detects file type and encoding, cleans missing or zero values, and prepares the dataset for compositional analysis.

2. **Automatic Model Selection**
   The script identifies the appropriate structure:

   * **600-minute model:** school-day composition (SB, LPA, MVPA)
   * **1440-minute model:** full-day composition (Sleep, SB, LPA, MVPA)

3. **Execution Phase**
   Runs the complete analytical pipeline, including:

   * ILR transformation and OLS regression models
   * ANOVA-based model diagnostics
   * Isotemporal substitution simulations (±30 min)
   * Generation of all visual outputs (barplots, reallocation curves, 3D surfaces)

4. **Output Stage**
   Displays:

   * Statistical summaries and ANOVA tables
   * Realocation plots and 3D predictive surfaces
   * Optional export of simulated data and model outputs to Excel for further analysis
  
Perfeito — aqui está uma seção para seu **README** explicando as **condições e requisitos que a base de dados deve atender** para que o script `run_compositional_full()` funcione corretamente.
O texto está em inglês, formal e pronto para inclusão no GitHub:

---

## Data Requirements

To ensure correct execution, the uploaded dataset must follow specific structure and variable conventions. The function automatically detects the model type (600 min or 1440 min) based on column names, but the following conditions must be met:

### 1. Supported File Formats

* **`.sav`** (SPSS format)
  Encoding is automatically detected (`latin1` or `windows-1252`).
* **`.xlsx`** (Excel format)
  Each variable must be stored in columns with headers in the first row.

### 2. Required Variables

#### (a) **600-minute composition (school-day model)**

Dataset must include at least these columns:

```
SB__Butte
LPA_Butte
MVPA_Butte
SEX_1
BMI
TOTALSCORE
LOCOMOTION
MANIPULATION
```

* All compositional variables (`SB__Butte`, `LPA_Butte`, `MVPA_Butte`) must be **positive** and **non-zero**.
* The script automatically removes rows with missing (`NaN`) or zero values.

#### (b) **1440-minute composition (full-day model)**

Dataset must include at least these columns:

```
Sleep_time_min
Avg_sedentary
Avg_light
Avg_MVPA
Sex
BMI
Laps
agility_coord
horizontal_jump
```

* Time-use variables must sum approximately to 1440 minutes per day.
* Missing or zero values in any component are excluded automatically.

### 3. Data Cleaning Rules

Before model fitting, the function:

1. Drops fully empty rows.
2. Removes observations with `NaN` in the compositional variables.
3. Converts non-numeric data to numeric format.
4. Excludes zero or negative values (closure transformation requires strictly positive inputs).

### 4. Automatic Detection

* If the file contains the columns `SB__Butte`, `LPA_Butte`, and `MVPA_Butte`, it is processed as **school-day (600 min)**.
* If it contains `Sleep_time_min`, `Avg_sedentary`, `Avg_light`, and `Avg_MVPA`, it is processed as **full-day (1440 min)**.
* Any other structure will trigger a warning and terminate execution.

### 5. Recommended Format

Each row should represent one participant or observation, with columns corresponding to:

* **Compositional parts** (minutes in each activity)
* **Covariates** (e.g., `sex`)
* **Outcomes** (e.g., `BMI`, `TOTALSCORE`, `agility_coord`, etc.)



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



