---
layout: default
title: "Jiahao Cao's homepage"
description: MCMC
google_analytics:
theme: jekyll-theme-cayman
---

## 1. Introduction and Examples

### Why we need Monte Carlo Techniques?

Many scientific problems involve the computation of integral for some integral function $g$ (usually in high dimension),

$$I = \int_{\mathcal{D}}g(\mathbf{x})\mathbf{d x}$$

If we can draw $x_i\sim \textbf{Unif}(\mathcal{D})$ i.i.d, then the *law of large number* tells us that as $n\to\infty$:

$$\hat{I}_n = \frac{1}{n}\sum_{i=1}^n g(x_i)\to I,\ \text{almost surely}$$

If we also know that $\mathrm{Var}(g(x))=\sigma^2<\infty$,then the *Central limit theorem* tells us that

$$\sqrt{n}(\hat{I}_n-I)\xrightarrow[]{\mathcal{D}} \mathcal{N}(0,\sigma^2)$$

This **Monte Carlo integration** gives us the convergence rate of this method, which is $\mathcal{O}(n^{-1/2})$ and the rate is **independent with the dimensionality** of $\mathbf{x}$.

Actually, the $\mathcal{O}(n^{-1/2})$ convergence rate is not ideal because other methods such as *Riemann approximation* and *Newton-Costes* give error rate equal to or faster than $\mathcal{O}(n^{-1})$. However, *these techniques do not scale well as the dimensionality of $\mathcal{D}$ increases*. For example using Riemann approximation,  when the dimensionality is $p$, we need to evaluate the function at $\mathcal{O}(n^p)$ points to achieve the same error(approximately) as the error when the dimensionality is $1$.

As for the Monte Carlo integration, here are two intrinsic difficulties:

* $\sigma^2$ can increase with the dimensionality because $g(x)$ can spread out when dimension $p$ is large.
* It may be hard to sample from $\textbf{Unif}(\mathcal{D})$.

**Importance sampling** may help us to deal with the first difficulty:

$$\hat{I}_{\pi, n} = \frac{1}{n}\sum_{i=1}^n \frac{g(x_i)}{\pi(x_i)}$$

where $x_i\sim \pi(x)$ i.i.d.

In this case we have $\sigma_{\pi}^2=\mathrm{Va}r_{\pi} \left(\frac{g(x)}{\pi(x)}\right)$ and if $\pi$ and  $g$ are "similar", the variance can be reduced: $\sigma^2_{\pi}<\sigma^2$.


Thus, our difficulties are converted to the following problems:

* How to find a good $\pi$ which is similar to $g$ ?
* How to sample from distribution $\pi$ ?
