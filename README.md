# GLM_Hackathon_Summer_2023
Data science works on GLM and scRNA-seq during summer intern 2023

---

## Contents
- [GLM\_Hackathon\_Summer\_2023](#glm_hackathon_summer_2023)
  - [Contents](#contents)
  - [Part 1: Overview](#part-1-overview)
  - [Part 2: File documentations](#part-2-file-documentations)
    - [1. Logistic regression from scratch](#1-logistic-regression-from-scratch)
      - [1.1 Variables](#11-variables)
      - [1.2 The logistic function (sigmoid function)](#12-the-logistic-function-sigmoid-function)
      - [1.3 Log likelihood](#13-log-likelihood)
    - [2. Negative binomial regression](#2-negative-binomial-regression)
    - [3. NB regression test on datasets](#3-nb-regression-test-on-datasets)
    - [4. Cell clustering and finding marker genes with scanpy](#4-cell-clustering-and-finding-marker-genes-with-scanpy)
  - [Part 3: Achievements](#part-3-achievements)
  - [Part 4: Future directions](#part-4-future-directions)

---

## Part 1: Overview

This is a repository for part of my work during the summer research internship 2023, supervised by Prof. Huang Yuanhua.

During the first one month and a half, I learned [foundamental data science skills][1] and read some materials on machine learning[^1][^2]. I have built a logistic regression model from scratch by implementing gradient descent, and a negative binomial regression model which fits the parameters $\beta$ and dispersion factor $\phi$ by using the [optimize function by statsmodels][2].

Additionally, I used my models to analyze some public datasets and got decent results, which are introduced in detail in [Part 2: File documentations](#part-2-file-documentations).

Meanwhile, I learned the basic procedures of scRNA-seq analysis and got familiar with some important tools such as docker and [scanpy][3]. As a small project, I used scanpy to cluster and find marker genes to annotate a public dataset and compared with the author's results, which aligned relatively well.


[1]: https://github.com/StatBiomed/GLM-hackathon

[2]: https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.minimize.html

[3]: https://scanpy-tutorials.readthedocs.io/en/latest/#

[^1]: [**_Probabilistic Machine Learning: An Introduction_** by *Kevin P Murphy*](https://probml.github.io/pml-book/book1.html)

[^2]: [**_An Introduction to Statistical Learning_**](https://www.statlearning.com)

---

## Part 2: File documentations


### 1. Logistic regression from scratch

#### 1.1 Variables
   
   **features:** 
   ```math
   \boldsymbol{x} = 
   \begin{bmatrix}
   x_1\\
   x_2\\
   \vdots\\
   x_n 
   \end{bmatrix}
   ```
   where $x_i = \left(x_{i1}, x_{i2}, ..., x_{ip}\right)$ is *p* dimentional

   **parameters:**
   ```math
    \boldsymbol{\beta} = \begin{bmatrix}
    \beta_1\\
    \beta_2\\
    \vdots\\
    \beta_n
    \end{bmatrix}
   ```

   **observed variables:**
   ```math
   \boldsymbol{y} = \begin{bmatrix}
    y_1\\
    y_2\\
    \vdots\\
    y_n
    \end{bmatrix}
   ```
   
   
   **linear predictor:**
   ```math
   \eta = \boldsymbol{\beta^Tx} = \beta_1x_1 + \beta_2x_2 + ... + \beta_px_p
   ```

#### 1.2 The logistic function (sigmoid function)

   $$\sigma\left(z\right) = \frac{1}{1 + exp\left(-z\right)}$$

  The range of $\sigma(z)$ is $\left[0, 1\right]$, which converts the dicision boundary $\boldsymbol{\beta^Tx} \in \left[-\infty, +\infty\right]$ to a probability:

  $$P(y = 1 | \beta, x) = \sigma\left(\boldsymbol{\beta^Tx}\right)$$
  which is desired for prediction.

  The deision boundary is

  ```math
  \hat{y} = \left\{
    \begin{aligned}
    1, \quad if \ P\left(y = 1 | \beta, x\right) \geq 0.5 \\
    0, \quad if \ P\left(y = 1 | \beta, x\right) < 0.5
    \end{aligned}
  \right.
  ```

  As $\sigma(0) = 0.5$, this is equivalent to 

  ```math
  \hat{y} = \left\{
    \begin{aligned}
    1, \quad if \ \boldsymbol{\beta^Tx} \geq 0 \\
    0, \quad if \ \boldsymbol{\beta^Tx} < 0
    \end{aligned}
  \right.
  ```

  Additionally, the derivative of $\sigma(z)$ is 

  $$\sigma^\prime(z) = \sigma(z) \cdot (1 - \sigma(z)) $$

  which will be useful in deriving the gradient of the loss function.

#### 1.3 Log likelihood

**The likelihood function:**
$$
\begin{split}
L(\beta) & = \prod_{i=1}^{N} Ber(y_i | \mu_i = \sigma(\boldsymbol{\beta^Tx_i}))\\
& = \prod_{i=1}^{N} P(y_i = 1 | \beta, x_i)^{y_i}
(1 - P(y_i = 1 | \beta, x_i))^{y_i}
\end{split}
$$

**Log likelihood:**
$$
LL(\beta) = \sum_{i=1}^{N} [ y_i log(\mu_i) + (1 - y_i) log(1 - \mu_i)]
$$

**Negative log likelihood, scaled by dataset size N:**
$$
NLL(\beta) = - \frac{1}{N} \sum_{i=1}^{N} [ y_i log(\mu_i) + (1 - y_i) log(1 - \mu_i)]
$$
which can be minimized to find $\beta$.

### 2. Negative binomial regression

### 3. NB regression test on datasets

### 4. Cell clustering and finding marker genes with scanpy
---


## Part 3: Achievements

---

## Part 4: Future directions