# Adaptability Stability in Watermelon

This repository presents the data and scripts that support the research published in the journal CBAB - http://dx.doi.org/10.1590/1984-70332026v26n2a17.

The journal Crop Breeding and Applied Biotechnology (CBAB) uses a Creative Commons Attribution 4.0 International License (CC BY 4.0).
# Database

The file _data.txt_ contains the raw data used in the analysis described in the article. The column labeled AMB represents the environments (12 evaluated); GEN indicates the genotype (15 evaluated); BLO represents the block or repetition (3 for each genotype in each of the environments). The variable of interest evaluated was Yield (PROD).

# Script for analysis

This script implements classical and Bayesian methods for adaptability and stability analysis in multi-environment trials, following Toler (1998).
The file "_script_adap_stab_WM.ipynb_" shows the script used to perform the inferences.

### Objective

This script performs adaptability and stability analysis in multi-environment trials using:

- Classical ANOVA (Randomized Complete Block Design across environments)
- Iterative frequentist estimation of environmental index (Toler method)
- Bayesian inference using PyMC
- Stability parameter (S²d) computation

The method is suitable for genotype × environment experiments.

### Workflow

The analysis is performed in the following steps:

1. Data loading and preprocessing
2. Classical ANOVA (to obtain QMR and CV%)
3. Iterative estimation of environmental index (frequentist method)
4. Bayesian inference (linear model with common beta)
5. Bayesian inference (segmented model)
6. Stability parameter (S²d) computation

### Input Data Format

The dataset must contain the following columns:

- AMB  → Environment
- GEN  → Genotype
- BLO  → Block (replication)
- PROD → Yield (response variable)

The design assumes a randomized complete block design within each environment.

### ANOVA Model

$Y_{ijk} = \mu + E_j + G_i + (GE)_{ij} + B_k(E_j) + \epsilon_ijk$

Where:
- $E_j$ = environment effect
- $G_i$ = genotype effect
- $GE_{ij}$ = genotype × environment interaction
- $B_k(E_j)$ = block within environment
- $\epsilon_{ijk}$ = experimental error

### Bayesian Segmented Model (Toler, 1998)

For each genotype:

$Y_{ij} = α_i + β1_i μ_j^- + β2_i μ_j^+ + \epsilon_{ij}$

Where:
- $μ_j$ is the environmental index
- $μ_j^- = μ_j if μ_j ≤ 0$
- $μ_j^+ = μ_j if μ_j > 0$
- $ε_ij \sim Normal(0, σ²)$

### Stability Parameter ($S^2_d$)

$S^2_d = \frac{(QMD_i ~ \times ~ r − QMR)}{r}$

Where:
- $QMD_i$ = mean square deviation from regression
- $QMR$ = residual mean square from global ANOVA
- $r$ = number of replications

QMR is obtained from the classical ANOVA model.

### Requirements

Python 3.10+

Required packages:

- numpy
- pandas
- matplotlib
- seaborn
- statsmodels
- pymc
- arviz
  
### How to Run

1. Adjust the file path in the data loading section.
2. Run cells sequentially:
   - Data loading
   - ANOVA
   - Frequentist parameter estimation
   - Bayesian Step 1
   - Bayesian Step 2
3. Results will be saved in:
   /bayesian_adaptability_toler_step2/

### Important Notes

- The notebook must be executed sequentially.
- QMR_global and r are computed only once and reused.
- The data must contain replication within environments.
- The model assumes balanced design.

### Citation

If you use this code, please cite:

Pereira CCA, Lima MMF, Martins AF, Lima FF, Almeida NTB, Silva EM, Silveira LM and Glauber Henrique de Sousa Nunes GHS (2026) Bayesian estimation of adaptability and stability parameters in watermelon genotypes using the Toler model. Crop Breeding Applied Biotechnology xx: xxx-xxx. http://dx.doi.org/10.1590/1984-70332026v26n2a17 (_This article is in the process of being published; the reference will be updated when it is published_)

