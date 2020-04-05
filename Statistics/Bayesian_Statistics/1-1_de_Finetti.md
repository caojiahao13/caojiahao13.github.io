---
layout: default
title: "Jiahao Cao's homepage"
description: Bayesian Statistics
theme: jekyll-theme-cayman
---

This section is based on [conditional expectation and martingales](https://galton.uchicago.edu/~lalley/Courses/313/Martingales.pdf). The author is galton  from Uchicago.

## de Finetti and exchangeable

Many (including me) can be confused about **why we can use prior** in Bayesian statistics. There indeed exists some interpretations and they are quite reasonable, but a theoretical derivation is needed to make us(at least for me) feel confident to use prior.

In this part I will state the basic process to proof.

#### Theorem 1: de Finetti
For any exchangeable sequence $$\{X_n\}_{n\geq 1}$$ of Bernoulli random variables. There is a unique Borel probability measure $μ$ on the unit interval $[0,1]$ such that for any finite sequence $\{e_j\}_{j\leq n}$ of $0$s and $1$s,  


$$P\left\{X_k=e_k,\ \forall k\leq n\right\} = \int_{\left[0,1\right]} p^{\sum_{i=1}^n e_i}(1-p)^{n-\sum_{i=1}^n e_i}\mu(dp) = $$


#### Theorem 2: Hewitt-Savage-de Finetti
$$\{X_n\}_{n\geq 1}$$ is an exchangeable sequence of random variables and $\mathcal{F}_e$ is the exchangeable $\sigma$-algebra. Then the (regular) conditional distribution given $\mathcal{F}_e$ is almost surely a product measure. Or we can say that condition on $\mathcal{F}_e$,$$\{X_n\}_{n\geq 1}$$ are i.i.d.

We can prove theorem 1 with theorem 2. So here we're going to prove the Hewitt-Savage-de Finetti theorem.

* **outline of the proof:**

First, a Borel space is a measurable space $(\mathcal{X},\mathcal{G})$ such that there is a bijective, bi-measurable mapping  $T:\mathcal{X}\to[0,1]$.

> see [Borel space](https://en.wikipedia.org/wiki/Borel_space) and [Borel isomorphism](https://en.wikipedia.org/wiki/Borel_isomorphism). I did not know the definition here. I used to treat  random variables as some measurable mappings so the image space just has $\sigma$-algebra structure. Here we restrict that it should be a Borel space.

> Why we can do this? Because Borel space is such a large class spaces, smaller that $\sigma$-field of course, that including space like $\mathbb{R}^k$ and its measurable subspace.

> [Here]((https://www.math.tamu.edu/~thomas.schlumprecht/descriptive_set_theory.pdf)) is an article about those spaces and relationships.

> Actually, [We can show that every uncountable Polish space is Borel isomorphic to the real numbers](https://planetmath.org/proofofpolishspacesuptoborelisomorphism), where [polish space](https://en.wikipedia.org/wiki/Polish_space) is a separable completely metrizable topological space(of course including $\mathbb{R}^k$).

Hence, without loss of generality, we may assume that the random variables $X_n$ are *real-valued*.

Also there two facts:

1.the sequence space $\mathbb{R}^{\mathbb{N}}$, with the usual Borel sets, is a Borel space

>

2.If a random variable $Z$ takes values in a Borel space then it has a regular conditional distribution given any $\sigma$−algebra. Thus, the sequence $$\{X_n\}_{n\geq 1}$$ has a regular conditional distribution given $\mathcal{F}_e$ .

> you can find the definition of regular conditional distribution [here](http://galton.uchicago.edu/~lalley/Courses/385/ConditionalExpectation.pdf)(also by galton).

> I admit, my mathematical background is absolutely not enough... When you need to learn almost everything, you may just choose to remember the result...

To show that the conditional distribution is, with probability one, a product measure it suffies to show that for any bounded, Borel measurable function $\psi_j:\mathbb{R}\to\mathbb{R}$, we have

$$E\left(\prod_{j=1}^m\psi_j(X_j)|\mathcal{F}_e\right) =\prod_{j=1}^mE\left(\psi_j(X_1)|\mathcal{F}_e\right) $$

> This can be checked by definition of product measure.


* Fact(1): for exchangeable sequence of integrable random variables $Y_1,Y_2,\cdots$, then  

$$\lim_{n\to\infty}\frac{1}{n}\sum_{j=1}^n Y_j = E\left(Y_1|\mathcal{F}_e\right)\quad\text{almost surely}$$

> This is the result of proposition 14 in [conditional expectation and martingales](https://galton.uchicago.edu/~lalley/Courses/313/Martingales.pdf).

* Fact(2): for exchangeable sequence of integrable random variables $Y_1,Y_2,\cdots$ and let $h: \mathbb{R}^d\to\mathbb{R}$ be any measurable function such that $h(Y_1,\cdots,Y_d)$ is integrable, Then

$$\lim_{n\to\infty}\frac{1}{n^d}\sum_{i_1,\cdots,i_d=1}^{n}h(Y_{i_1},\cdots,Y_{i_d}) = E(h(Y_1,\cdots,Y_d)|\mathcal{F}_e)$$

> This is the result of proposition 15 in [conditional expectation and martingales](https://galton.uchicago.edu/~lalley/Courses/313/Martingales.pdf).

Now, since

$$\sum_{i_1,\cdots,i_d=1}^{n} \prod_{j=1}^m\psi_j(X_{i_j})=  \prod_{j=1}^m\left(\sum_{i=1}^{n}\psi_j(X_{i})\right)$$

Write $$h_m(y_1,\cdots,y_m)=\prod_{j=1}^m y_i$$ , then by fact 2 we have

$$\lim_{n\to\infty}\frac{1}{n^m}\sum_{i_1,\cdots,i_m=1}^{n}\prod_{j=1}^m \psi_j(X_{i_j})=E\left(\prod_{j=1}^m\psi_j(X_j)|\mathcal{F}_e\right) $$

By fact 1 we have

$$\lim_{n\to\infty}\frac{1}{n^m}\sum_{i_1,\cdots,i_m=1}^{n}\prod_{j=1}^m \psi_j(X_{i_j}) = \lim_{n\to\infty}  \prod_{j=1}^m\left(\frac{1}{n}\sum_{i=1}^{n}\psi_j(X_{i})\right)=\prod_{j=1}^mE\left(\psi_j(X_1)|\mathcal{F}_e\right)$$

Finally we have

$$E\left(\prod_{j=1}^m\psi_j(X_j)|\mathcal{F}_e\right) =\prod_{j=1}^mE\left(\psi_j(X_1)|\mathcal{F}_e\right) $$
