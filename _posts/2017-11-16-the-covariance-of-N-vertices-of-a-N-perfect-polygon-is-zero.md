---
layout: post
title: An interesting fact about covariance
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

I believe you're more or less confused by the title. Indeed, it's not easy to summarize all the stuff I discuss below in the title, which is too short. So first things first, let me explain the title in detail, which is a claim I proved last semester when I was learning course 10-601 - Introduction to Machine Learning.

## The story behind it

Last semester I took course 10-601 - Introduction to Machine Learning. The instructor was Roni Rosenfeld, a very nice and lovely man. In the first lecture on Bayesian Estimation, when Roni reviewed covariance for us, one student asked:

How will the covariance of a 2D dataset change if all data points in the set are rotated by a same angle?

Its answer is not easily seen. What Roni said that day is he thought it would not change. But this turned out to be incorrect, as can be disproved by an simple experiment. Then in the next lecture, Roni changed his statement and said if all data points form a perfect polygon, their covariance may not change. The motivation of this guess is that a perfect polygon shaped data points are centrosymmetric, and a centrosymmetric dataset usually has zero covariance (in fact I have not find any contradiction yet). Let me rephrase Roni's hypothesis in a slightly more formal way:

The covariance of any N 2D points which are N vertices of a perfect polygon is zero.

This really triggered my interest, and I started to work on it under Roni's guidance. First I loosely verified this claim by generating datasets having this property and calculating their covariance, and it turned out that all covariances are either 0 or a floating number very close to 0, like 1e-17. Good, we were at the right direction. Roni was happy on this and asked for a formal proof. Then I proved it, and **my proof was later attached to his teaching notes!**

## Proof

**Claim:** If $N$ data points in a 2D dimension space is exactly the $N$ vertices of a perfect polygon, their covariance is zero.

**Proof.** Here is the N data points set: $D = \{(x_1, y_1), (x_2, y_2), ... , (x_N, y_N)\}$. $x_i$ and $y_i$ are observations of random variable $X$ and $Y$.

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

So the rest of our proof is plugging the coordinates of the N vertices into equation (1) and (2), doing some mathematical works and showing that they are true. The coordinates of these vertices are easy to get, because in our problem setting we have constrained them to be the N vertices of a **perfect polygon**, which means once we set the coordinates of the first vertex, the coordinates of the rest can be known simply by rotating the first vertex. For the sake of simplicity, we represent the vertices with polar coordinate.

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

where $\alpha = 2\pi / N$.

Plugging them into equation (1) and (2), we get

$$
\begin{align}
\sum_{i=1}^N (x^2_i - y^2_i) & = \sum_{k=0}^{N-1} (cos^2 k \alpha - sin^2 k \alpha) \\
& = \sum_{k=0}^{N-1} cos 2k \alpha \\
& = \sum_{k=0}^{N-1} cos \frac{4k\pi}N & (3) \\
\sum_{i=1}^N (x_i y_i) & = \sum_{k=0}^{N-1} cos(k\alpha) sin(k \alpha) \\
& = \sum_{k=0}^{N-1} \frac12 sin2k\alpha \\
& = \sum_{k=0}^{N-1} \frac12 sin \frac{4k\pi}N & (4)
\end{align}
$$

We can show that both equation (3) and (4) equal to zero by using the following formula [^1][^2]:

$$
\begin{align}
\sum_{k=1}^N sinkx & = \frac{cos (x/2) - cos((N+1/2) x)}{2sin(x/2)} & (5) \\
\sum_{k=0}^N coskx & = \frac12 + \frac{sin((N+1/2)x)}{2sin(x/2)} & (6)
\end{align}
$$

Okay, so far, so good? Now let's work on that.

**Prove (3) holds with (6)**

$$
\begin{align}
\sum_{i=1}^N (x^2_i - y^2_i) & = \sum_{k=0}^{N-1} cos \frac{4k\pi}N \\
& = \frac12 + \frac{sin(N-1+\frac12) \frac{4\pi}N}{2sin \frac{2\pi}N} \\
& = \frac12 + \frac{sin(-\frac{2\pi}N)}{2sin \frac{2\pi}N} \\
& = \frac12 - \frac12 \\
& = 0
\end{align}
$$

**Prove (4) holds with (5)**

$$
\begin{align}
\sum_{i=1}^N (x_i y_i) & = \sum_{k=0}^{N-1} \frac12 sin \frac{4k\pi}N \\
& = \frac12 sin0 + \sum_{k=1}^{N-1} \frac12 sin \frac{4k\pi}N \\
& = 0 + \frac12 \sum_{k=1}^{N-1} sin \frac{4k\pi}N \\
& = \frac12 \cdot \frac{cos \frac{2\pi}N - cos(N-1+\frac12) \frac{4\pi}N}{2sin \frac{2\pi}N} \\
& = \frac12 \cdot \frac{cos \frac{2\pi}N - cos(4\pi - \frac{2\pi}N)}{2sin \frac{2\pi}N} \\
& = \frac12 \cdot \frac{cos \frac{2\pi}N - cos\frac{2\pi}N}{2sin \frac{2\pi}N} \\
& = 0
\end{align}
$$

Therefore, if $N$ data points in a 2D dimension space is exactly the N vertices of a perfect polygon, their covariance is zero.

Q.E.D.

---


[^1]: https://www.math.upenn.edu/~kazdan/202F09/sum-sin_kx.pdf
[^2]: https://math.stackexchange.com/questions/225941/proving-sum-limits-k-0n-coskx-frac12-frac-sin-frac2n12x
