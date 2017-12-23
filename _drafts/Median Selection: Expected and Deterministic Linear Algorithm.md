---
layout: post
title: "Median Selection: Expected and Deterministic Linear Algorithm"
author: Yiming Pan
category: algorithm
date: 2017-12-22 21:00:00 -0004
---

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Problem Definition

Given an unsorted integer array, how fast can we find its [median](https://en.wikipedia.org/wiki/Median)? For the sake simplicity, we assume all elements in the array are **distinct**, and the size of the array is **even**. Once you understand how to deal with this simplified case, I think you are confident to extend it to somewhat more complicated case.

## Break Down the Problem

Finding the median of a n-size array is equivalent to finding the $\frac{n}2$-th and $\frac{n}2 + 1$-th largest integer separately and computing their mean. How to select out the k-th largest integer then?

We have to make the array somewhat sorted so that we could know how large an integer is. Okay, one direct solution is first sorting the entire array, and the k-th largest element can be selected out in $O(1)$ time. Since sorting can be done no faster than $O(nlogn)$, the complexity of this solution is $O(nlogn)$.

It looks good enough. Can we do better?

## Randomized Solution (Expected Linear Algorithm)

The randomized solution is motivated by the **Randomized QuickSort Algorithm**, in which the pivot is selected randomly among all elements. 

