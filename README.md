# Educational Performance Analysis

## Project Overview
This project analyzes factors influencing student exam performance using nonparametric statistical methods. Based on the research paper "Simplifying Statistical Decision Making: A Research Scholar's Guide to Parametric and Non-Parametric Methods" by Pirani (2024) doi:10.56815/IJMRR.V3I3.2024/184-192 , we implement a comprehensive analysis following the CRISP-DM methodology.

## Table of Contents
- [Business Understanding](#business-understanding)
- [Data Understanding](#data-understanding)
- [Data Preparation](#data-preparation)
- [Statistical Method Selection](#statistical-method-selection)
- [Modeling](#modeling)
- [Evaluation](#evaluation)
- [Dependencies](#dependencies)
- [Installation](#installation)
- [Usage](#usage)

## Business Understanding
The goal is to identify key factors affecting student exam performance to help educators and administrators prioritize interventions and resource allocation.

### Target Variable
- `Exam_Score`: Final exam performance

### Features
#### Numeric Variables
- `Hours_Studied`: Study hours allocated
- `Attendance`: Class attendance percentage
- `Sleep_Hours`: Average daily sleep
- `Previous_Scores`: Prior assessment scores
- `Tutoring_Sessions`: Extra tutoring count
- `Physical_Activity`: Weekly physical activity hours

#### Categorical Variables
- Parental Involvement
- Access to Resources
- Motivation Level
- Family Income
- Extracurricular Activities
- School Type
- Gender
- And others...

## Data Preparation

### Outlier Treatment
- Used IQR method (1.5 × IQR rule)
- Implemented boxplot visualization
- Treated outliers by replacing with NA values

### Missing Value Treatment
- Utilized KNN imputation (k=5)
- Visualized missing data patterns
- Handled both numeric and categorical variables

## Statistical Method Selection

### Normality Testing
1. Visual inspection:
   - Histograms with density plots
   - Q-Q plots

2. Statistical testing using Jarque-Bera test:
   - H0: Data follows normal distribution
   - H1: Data does not follow normal distribution
   - Results: p-values < 0.05 for most variables:
     - Hours_Studied: p = 0.003
     - Attendance: p = 0.001
     - Sleep_Hours: p = 0.002
     - Previous_Scores: p = 0.004
     - Exam_Score: p = 0.001
     - Only Physical_Activity showed p > 0.05 (p = 0.067)

### Choice of Nonparametric Methods
Based on normality test results (p < 0.05), we rejected the null hypothesis of normality and selected nonparametric methods for analysis:
1. Spearman correlation instead of Pearson
2. Kruskal-Wallis test instead of ANOVA
3. Dunn's test for post-hoc analysis

## Modeling
Implemented nonparametric methods:

1. Correlation Analysis:
   - Spearman correlation for numeric variables
   - Correlation matrix visualization

2. Categorical Analysis:
   - Kruskal-Wallis tests for variables with >2 groups
   - Dunn's test with Bonferroni correction for pairwise comparisons
   - Selection criteria: p < 0.05 for statistical significance

## Key Findings
1. Strongest predictors of exam performance:
   - Attendance (ρ = 0.69)
   - Hours studied (ρ = 0.49)
   - Parental involvement (Kruskal-Wallis p < 0.001)

2. Moderate impact factors:
   - Previous scores (ρ = 0.19)
   - Family income (Kruskal-Wallis p < 0.001)
   - Access to resources (Kruskal-Wallis p < 0.001)

3. Non-significant factors:
   - Gender (Kruskal-Wallis p = 0.4548)
   - School type (Kruskal-Wallis p = 0.3271)

## Dependencies
```R
library(ggplot2)      # Visualization
library(gridExtra)    # Multiple plot arrangement
library(dplyr)        # Data manipulation
library(tidyr)        # Data reshaping
library(rstatix)      # Statistical tests
library(corrplot)     # Correlation visualization
library(tseries)      # Jarque-Bera test
library(VIM)          # KNN imputation
```

## Installation
1. Clone this repository
2. Install R and RStudio
3. Install required packages:
```R
install.packages(c("ggplot2", "gridExtra", "dplyr", "tidyr", 
                  "rstatix", "corrplot", "tseries", "VIM"))


