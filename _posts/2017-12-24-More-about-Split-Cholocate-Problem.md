---
layout: post
title: More about Split Chocolate Problem
author: Yiming Pan
category: math probability
date: 2017-12-24 17:00:00 -0004
---

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

Last time I introduced the [split chocolate problem](https://yimingpan.github.io/math%20probability/2017/12/22/Interesting-Probability-Problem-Split-Chocolate-Bar.html). Later that day, when I was discussing this problem with one of my friend, she raised a good question:

If $L=1$, then $X \sim U(0.5, 1)$, which means the probability of any possible value of $L$ is 2. How could a probability value be larger than one?

I was also confused at first. It's weird, but it's a correct solution. So I must have got something wrong. After searching on Google, I found out that we've confused **probability** and **probability density**. Probability is a real value lying in $[0, 1]$, but probability density is not. Probability density is defined upon continuous random variable. According to Wikipedia:

> The probability density function is nonnegative everywhere, and its integral over the entire space is equal to one.

It's a common misunderstanding that a probability density is always less than 1. We may have this wrong understanding because many probability density functions always take on values less than 1, for example, the Gaussian distribution function. But if you consider a uniform distribution $U(a,b)$ with $b-a < 1$, it always take on values greater than one.
