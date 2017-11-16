---
layout: post
title: The covariance of any N 2D points which form a perfect polygon is zero
author: Yiming Pan
category: math
date: 2017-11-16 12:30:00 -0004
---

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

In this post, I'll prove the following statement:

If $N$ data points in a 2D dimension space is exactly the N vertices of a perfect polygon, their covariance is zero.

---

**Proof**

Here is the N data points set: $D = \{(x_1, y_1), (x_2, y_2), ... , (x_N, y_N)\}$. $x_i$ and $y_i$ are observations of random variable $X$ and $Y$.

Without loss of generality, We make this data points centered at origin, which means $E(X)=0$ and $E(Y) = 0.$

Rotating every point in this counter-clockwisely by $\theta$, we get a rotated data set. Let's say the coordinate of point $(x, y)$ after rotation is $(x', y')$, then we have:

$$
\begin {align}
x' = x cos(\theta) - y sin(\theta) \\
y' = x sin(\theta) + y cos(\theta)
\end{align}
$$

The covariance of the rotated data points is

$$
\begin{align}
Cov(X', Y') & = \frac1N \sum_{i=1}^N x'y' - E(X')E(Y')
\end{align}
$$

It's not hard to see that $E(X')$ and $E(Y')$ are both zero:

$$
\begin{align}
E(X') & = E(X cos(\theta) - Y sin(\theta)) = E(X) cos(\theta) - E(Y) sin(\theta) = 0 \\
E(Y') & = E(X sin{\theta} + Y cos(\theta)) = E(X) sin(\theta) + E(Y) cos(\theta) = 0
\end{align}
$$

So only the first term in the expression of $Cov(X', Y')$ is left. Plugging in the expression of $x'$ and $y'$ and simplifying it, we have:

$$
Cov(X', Y') = \frac1N \sum_{i=1}^N [(x_i^2 - y_i^2)sin\theta cos\theta + x_i y_i (cos^2\theta - sin^2 \theta)]
$$

Now, our target is to prove that the above equation is always zero regardless of rotation angle $\theta$. This can be done by separately proving the following two equation under the constraint that points $\{x_i, y_i\}^N_{i=1}$ are N vertices of a perfect polygon.

$$
\begin{align}
\sum_{i=1}^N (x^2_i - y^2_i) & = 0 & (1)\\
\sum_{i=1}^N (x_i y_i) & = 0 & (2)
\end{align}
$$

So the rest of our proof is plugging the coordinates of the N vertices into equation (1) and (2), doing some mathematical works and showing that they are true. The coordinates of these vertices are easy to get, because in out problem setting we have constrained them to be the N vertices of a **perfect polygon**, which means once we set the coordinates of the first vertex, the coordinates of the rest can be known simply by rotating the first vertex. For the sake of simplicity, we represent the vertices with polar coordinate.

Suppose the first vertex $(r_1, \theta_1) = (1, 0)$, the coordinates of all N vertices are as follow:

$$
\begin{align}
(r_1, \theta_1) & = (1, 0) \\
(r_2, \theta_2) & = (1, \alpha) \\
(r_3, \theta_3) & = (1, 2\alpha) \\
... \\
(r_N, \theta_N) & = (1, (N-1) \alpha)
\end{align}
$$

where $\alpha = 2\pi / N​$.

Plugging them into equation (1) and (2), we get

$$
\begin{align}
\sum_{i=1}^N (x^2_i - y^2_i) & = \sum_{k=0}^{N-1} (cos^2 k \alpha - sin^2 k \alpha) \\
& = \sum_{k=0}^{N-1} cos 2k \alpha \\
& = \sum_{k=0}^{N-1} cos \frac{4k\pi}N & (3) \\
\sum_{i=1}^N (x_i y_i) & = \sum_{k=0}^{N-1} cos(k\alpha) sin(k \alpha) \\
& = \sum_{k=0}^{N-1} \frac12 sin2k\alpha & (4)
\end{align}
$$

We can show that both equation (3) and (4) equal to zero by using the following formula [^1][^2]:

$$
\begin{align}
\sum_{k=1}^N sinkx & = \frac{cos (x/2) - cos((N+1/2) x)}{2sin(x/2)} & (5) \\
\sum_{k=0}^N coskx & = \frac12 + \frac{sin((N+1/2)x)}{2sin(x/2)} & (6)
\end{align}
$$

Therefore, if $N$ data points in a 2D dimension space is exactly the N vertices of a perfect polygon, their covariance is zero.

Q.E.D.

---


[^1]: https://www.math.upenn.edu/~kazdan/202F09/sum-sin_kx.pdf
[^2]: https://math.stackexchange.com/questions/225941/proving-sum-limits-k-0n-coskx-frac12-frac-sin-frac2n12x
