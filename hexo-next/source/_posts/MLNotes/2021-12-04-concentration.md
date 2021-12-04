---
title: Concentration of Measure Inequalities
date: 2021-12-04 14:34:52
updated: 
categories:
  - Reading
tags:
  - Mathematics
  - Probability Theory
mathjax: true
---

<!--
post_link
phd/2020-04-12-Hexo-Troubles.md
phd/2021-01-02-Hexo-Problems.md

Configure, (Configurate,) Configuration
Declaimer:
  - Machine Learning
-->


***Chapter 2. Concentration of Measure Inequalities***
NB. This note is based on [Machine Learning at DIKU](https://sites.google.com/diku.edu/machine-learning-courses/ml).

Concentration of measure inequalities are one of the main tools for analysing learning algorithms. This chapter is devoted to a number of concentration of measure inequalities that form the basis for the results discussed in later chapters.


# Markov's Inequality

Markov's inequality is the simplest and relatively weak concentration inequality.

**Theorem 2.1** (Markov's Inequality). *For any non-negative random variable $X$ and $\varepsilon >0$,* 
$$\mathbf{Pr}( X \geqslant \varepsilon ) \leqslant \frac{ \mathbf{E}[X] }{\varepsilon} .$$

*Proof.* {% post_link MLNotes/2021-12-04-concentration-part-a Markov's-inequality %}

By denoting the right hand side of Markov's inequality by $\delta$ we obtain the following equivalent statement. For any non-negative random variable $X$,
$$\mathbf{Pr}\left( X\geqslant \tfrac{1}{\delta} \mathbf{E}[X] \right)\leqslant\varepsilon .$$

We note that even though Markov's inequality is weak, there are situations in which it is tight.


# Chebyshev's Inequality

Our next stop is Chebyshev's inequality, which exploits variance to obtain tighter concentration.

**Theorem 2.2** (Chebyshev's inequality). *For any $\varepsilon >0$,*
$$\mathbf{Pr}( |X-\mathbf{E}[X]| \geqslant\varepsilon ) \leqslant\tfrac{\mathbf{Var}[X]}{\varepsilon^2} .$$

*Proof.* {% post_link MLNotes/2021-12-04-concentration-part-a Chebyshev's-inequality %}


# Hoeffding's Inequality


# Basics of Information Theory


# kl Inequality


# Sampling Without Replacement

