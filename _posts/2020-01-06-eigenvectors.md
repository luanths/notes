---
toc: false
comments: true
layout: post
description: An intuition using covariance matrices
categories: [math]
title: Eigenvectors from eigenvalues
---

"Eigenvectors from eigenvalues" ([Quanta article][quanta], [Terry Tao blog
post][tao]) is a recent result showing an unexpected relationship in basic
linear algebra.

[quanta]: https://www.quantamagazine.org/neutrinos-lead-to-unexpected-discovery-in-basic-math-20191113/
[tao]: https://terrytao.wordpress.com/2019/08/13/eigenvectors-from-eigenvalues/

I was trying to develop some intuition for this result and I initially found the
proofs hard to read and understand, but after some studying I think I get it.
I've written a quick explanation below; I think this would be much improved with
pictures, but I don't want to figure that out right now. Maybe another time.

Suppose $A$ is a covariance matrix. Let $\lambda$ be the largest eigenvalue of
$A$, with eigenvector $v$. We know $\lambda$ and we'd like to learn about $v$.

Consider $\lambda I - A$ as a covariance matrix. Its variance in each direction
is $\lambda$ minus the variance that $A$ has in that direction. In particular,
it has zero variance in the $v$ direction. If you imagine samples from a
Gaussian distribution with covariance $\lambda I - A$, it'll be a point cloud
shaped like a flat ellipse that is perpendicular to $v$.

Now if we look at this flat ellipse from the $j$-th coordinate direction, how
big is its "silhouette"? That is, what is the area of the projection of the
ellipse onto the $j$-th coordinate plane?

If the $j$-th axis is parallel to $v$, then it's like looking at a pancake
head-on: the area of the projection is the area of the whole ellipse. But if the
$j$-th axis is perpendicular to $v$, then it's like looking at a pancake
sideways: the area of the projection is zero.

In general we have a linear combination of these two cases, so we can figure out
the component of $v$ that is along the $j$-th axis by taking the ratio of the
projection's area to the ellipse's area. And that's effectively what the
eigenvectors-from-eigenvalues formula does.

(This geometric interpretation only works with the largest eigenvalue, because
variances and areas have to be positive, but the math works out regardless.)

What's notable to me is how helpful it was to my intuition to think of $A$ as a
covariance matrix, rather than as a linear transformation, which is the more
usual role of matrices in linear algebra. I think this applies to many uses of
matrix math I see. More on this later, maybe?
