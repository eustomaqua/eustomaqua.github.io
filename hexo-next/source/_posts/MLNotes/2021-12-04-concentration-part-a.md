---
title: Proof of Markov's and Chebyshev's inequalities
date: 2021-12-04 15:46:37
updated: 
categories:
  - Reading
tags:
  - Mathematics
  - Probability Theory
mathjax: true
---

NB. This note is based on [Machine Learning at DIKU](https://sites.google.com/diku.edu/machine-learning-courses/ml).



# Markov's Inequality

*Proof of* **Theorem 2.1**. Define a random variable $Y= \mathbb{1}(X \geqslant \varepsilon)$ to be the indicator function of whether $X$ exceeds $\varepsilon$. Then $Y \leqslant \frac{X}{\varepsilon}$. Since $Y$ is a Bernoulli random variable, $\mathbf{E}[Y] = \mathbf{Pr}(Y=1)$. We have:
$$\mathbf{Pr}(X \geqslant \varepsilon) = \mathbf{Pr}(Y=1) = \mathbf{E}[Y] \leqslant \mathbf{E}\left[\tfrac{X}\varepsilon\right] = \tfrac{\mathbf{E}[X]}{\varepsilon} .$$
Q.E.D.

<font color="4169E1">
Note that $Y=\mathbb{1}\left(\frac{X}{\varepsilon} \geqslant 1\right) \in[0,1]$, and that $\frac{X}{\varepsilon} \in[0,+\infty)$ due to the non-negativity of $X$. 

1. If $\tfrac{X}{\varepsilon} \in[0,1)$, then $Y=0$, and $Y\leqslant \tfrac{X}{\varepsilon}$;
2. If $\tfrac{X}{\varepsilon} =1$, then $Y=1$, and $Y= \tfrac{X}{\varepsilon}$;
3. If $\tfrac{X}{\varepsilon} \in(1,+\infty)$, then $Y=1$, and $Y< \tfrac{X}{\varepsilon}$.

Overall, $Y\leqslant \frac{X}{\varepsilon}$. Then $\mathbf{Pr}\big( X\geqslant \frac{1}{\delta} \mathbf{E}[X] \big) \leqslant \frac{\mathbf{E}[X]}{ \delta\mathbf{E}[X] } = \delta$. 
</font>



# Chebyshev's Inequality

*Proof of* **Theorem 2.2**. The proof uses a transformation of a random variable. We have that $\mathbf{Pr}( |X-\mathbf{E}[X]| \geqslant\varepsilon )=\mathbf{Pr}\left( (X-\mathbf{E}[X])^2 \geqslant\varepsilon^2 \right)$, because the first statement holds if and only if the second holds. In addition, using Markov's inequality and the fact that $(X-\mathbf{E}[X])^2$ is a non-negative random variable we have
$$\mathbf{Pr}(|X-\mathbf{E}[X]|\geqslant\varepsilon) = \mathbf{Pr}\left((X-\mathbf{E}[X])^2\geqslant\varepsilon^2\right) \leqslant\tfrac{\mathbf{E}\left[(X-\mathbf{E}[X])^2\right]}{\varepsilon^2} =\tfrac{\mathbf{Var}[X]}{\varepsilon^2} .$$
Q.E.D.


In order to illustrate the relative advantage of Chebyshev's inequality compared to Markov's consider the following example. Let $X_1,...,X_n$ be $n$ independent identically distributed Bernoulli random variables and let $\hat{\mu}_n$ 

by more than $\varepsilon$ (this is the central question in machine learning). We have $\mathbf{E}[\hat{\mu}_n] = \mathbf{E}[X_1]=\mu$ 

and by independence of $X_i$-s and Theorem B.26 we have $\mathbf{Var}[\hat{\mu}_n]$ 

$= \frac{1}{n^2}\mathbf{Var}[n\hat{\mu}_n] = \frac{1}{n^2}\sum_{i=1}^n\mathbf{Var}[X_i] = \frac{1}{n}\mathbf{Var}[X_1]$. By Markov's inequality,

$$\mathbf{Pr}(\hat{\mu}_n-\mathbf{E}[\hat{\mu}_n] \geqslant\varepsilon) = \mathbf{P}(\hat{\mu}_n\geqslant\mathbf{E}[\hat{\mu}_n]+\varepsilon) \leqslant\frac{\mathbf{E}[\hat{\mu}_n]}{\mathbf{E}[\hat{\mu}_n]+\varepsilon} = \frac{\mathbf{E}[X_1]}{\mathbf{E}[X_1]+\varepsilon} .$$

Note that as $n$ grows the inequality stays the same. By Chebyshev's inequality we have

$$\mathbf{Pr}(\hat{\mu}_n-\mathbf{E}[\hat{\mu}_n]\geqslant\varepsilon) \leqslant\mathbf{P}(|\hat{\mu}_n-\mathbf{E}[\hat{\mu}_n]|\geqslant\varepsilon) \leqslant\frac{\mathbf{Var}[\hat{\mu}_n]}{\varepsilon^2} =\frac{\mathbf{Var}[X_1]}{n\varepsilon^2} .$$


