---
layout: post
title: "Interesting Probability Problem: Split Chocolate Bar"
author: Yiming Pan
category: math probability
date: 2017-12-22 21:00:00 -0004
---

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Problem Definition

I have a bar of chocolate whose length is L. If I randomly split it into two pieces, can you tell me the **expected** length of the larger piece? An equivalent question is, what is the resulting length of the larger piece **on average**?

Note: when I split the chocolate, I always cut the L-length edge, and the cut is parallel to the other edge.

## Solution

Essentially, this problem asks us to compute the expectation of a random variable, which is the length of the larger piece. Let's represent this random variable as letter $X$. The implication of "I randomly split it into two pieces" is that X satisfies [uniform distribution](https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)) $U(L/2, L)$.

Since the expectation of $U(a, b)$ is $(a+b)/2$, the expected length of the larger piece of chocolate is $3L/4$.
