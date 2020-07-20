---
toc: true
comments: true
layout: post
description: A matrix can represent a linear map, but it can also do other things.
categories: [math]
title: Three ways to look at a matrix
---

## What can you do with a matrix?

A matrix can be used to represent at least three different things:

1. A linear map from vectors to vectors
2. A bilinear map from pairs of vectors to scalars
3. A combination of outer products of vectors

The linear map is the most familiar, if you learned linear algebra the way I
did. A matrix $M$ represents a linear map which acts according to multiplying a
vector by that matrix, $T(v) = Mv$.

For a while I only knew this way to think about matrices, and while it is the
right way a lot of the time, sometimes people do use matrices to mean something
else and it's confusing to try to interpret them as linear maps. And sometimes
it's helpful to view the same matrix in multiple ways. So I'd like to write a
little about other ways to look at a matrix.

## A matrix as a bilinear map

A [bilinear map][bilinear map] is a function that takes two vectors, returns a
vector, and is linear in each argument separately. For this post we'll only
consider bilinear maps that return 1-dimensional vectors, which are the same as
scalars. Some familiar examples of these are the dot product and the cross
product.

[bilinear map]: https://en.wikipedia.org/wiki/Bilinear_map

If you have a $m$ by $n$ matrix $M$, you can define a bilinear map $T:
\mathbb{R}^m \times \mathbb{R}^n \to \mathbb{R}$ by:

$$T(u, v) = u^T M v$$

You can think of this as a sort of weighted product of $u$ and $v$, where the
$(i,j)$ entry of $M$ is the weight to put on $u_i$ times $v_j$. (Exercise: show
this by expanding the matrix-vector products.)

The dot product is what you get if $M = I$. The cross product in three
dimensions is given by the matrix

$$\begin{pmatrix}
0 & 1 & -1 \\
-1 & 0 & 1 \\
1 & -1 & 0 \\
\end{pmatrix}$$

A bilinear map can be used to define a quadratic function from vectors to
scalars -- a [quadratic form][quadratic form] -- by letting $u$ and $v$ be the
same vector. This happens, for example, in the probability density of a normal
distribution in multiple dimensions:

$$p(x) \propto \exp( -(x - \mu)^T \Sigma^{-1} (x - \mu) )$$

[quadratic form]: https://en.wikipedia.org/wiki/Quadratic_form

where $\mu$ is the mean and $\Sigma$ is the covariance. The thing in the
exponent is a "product" of $x - \mu$ with itself, so this equation says that log
density peaks at $x = \mu$, and it falls off quadratically in each direction at
some rate determined by $\Sigma$.[^psd]

[^psd]: This description depends on the fact that covariance matrices are
    positive definite, which is basically a condition that the "product" of any
    vector with itself is not negative.

If you have a $M$ which represents a linear map $\mathbb{R}^m \to \mathbb{R}^n$,
you can "cast" it into a bilinear map: $u^T M v = u \cdot Mv$. That is, first
apply the linear map to $v$ to get another vector $M v$, and then take the dot
product of that with $u$.

## A matrix as a combination of outer products

Given a pair of vectors $u$ and $v$, the outer product $uv^T$ combines the two
vectors in a bilinear way.

If you have $uv^T$, you can determine the result of $u^T M v$ for any $M$. This
is known as the ["trace trick"][trace trick], because you can prove it by using
the trace operator, but you can also see it by writing out the matrix products:

[trace trick]: https://people.eecs.berkeley.edu/~jordan/courses/260-spring10/other-readings/chapter13.pdf

$$ u^T M v = \sum_{i,j} u_i M_{i,j} v_j = \sum_{i,j} M_{i,j} u_i v_j = \sum_{i,j} M_{i,j} (uv^T)_{i,j} $$

This also makes it clear that $M$ acts *linearly* on the elements of $uv^T$.

It is useful to consider the vector space that you get by allowing linear
combinations of $uv^T$'s, which one might call the tensor product
space[^tensors]. A member of this space is a matrix that summarizes one or more
vector-pairs for the purpose of computing the sum of any bilinear function over
those vector-pairs.

[^tensors]: For more on tensors, see Jeremy Kun's [How to Conquer
    Tensorphobia][tensorphobia1] and [Tensorphobia and the Outer
    Product][tensorphobia2].
    
[tensorphobia1]: https://jeremykun.com/2014/01/17/how-to-conquer-tensorphobia/
[tensorphobia2]: https://jeremykun.com/2016/03/28/tensorphobia-outer-product/

The example I have in mind here is covariance matrices. If $x$ is a random
vector with zero mean, its covariance matrix is $E[xx^T]$. This matrix lets you
compute the expectation of any quadratic function of $x$, that is, anything that
looks like $E[x^T M x]$.[^covar-basis-independent]

[^covar-basis-independent]: I like this because it shows that the covariance
    matrix represents an object that is coordinate-independent; it doesn't just
    tell you the covariance between $x_i$ and $x_j$, which you can get by
    reading off the entries, but also the covariance between linear functions of
    $x$ that are not coordinate-aligned.

## Some things you can do with matrices and what they mean

Matrix multiplication:

* If $A$ and $B$ are matrices representing linear maps, then $AB$ represents the
  linear map of $A$ composed with the linear map of $B$.

* If $A$ represents a linear map and $B$ represents a bilinear map, $A^T B A$
  represents the bilinear map you get by applying $A$ to the each argument
  before applying $B$. $A^T B$ is the one which applies $A$ to the first
  argument only, and $B A$ applies $A$ to the second argument only.

* If $A$ and $B$ represent linear maps, $A^T B$ represents the bilinear map you
  get by applying $A$ to the first argument and $B$ to the second argument, then
  taking a dot product.

Transpose:

* If $A$ is a linear map from $U$ to $V$, $A^T$ is a linear map from $V^*$ to
  $U^*$, where $V^*$ is the dual vector space of $V$: the space of linear maps
  from $V$ to scalars.

* If $A$ is a bilinear map, $A^T$ is the bilinear map you get by switching the
  arguments. If $A$ is a symmetric matrix, its bilinear map is a symmetric
  function of its arguments.

* If $A$ is a linear combination of outer products, $A^T$ is what you get if you
  did the outer products in the other order ($vu^T$ instead of $uv^T$).

Eigenvectors:

* An eigenvector $v$ of $A$, with eigenvalue $\lambda$, is a vector satisfying
  $Av = \lambda v$. That is, the linear map of $A$ acts on the vector $v$ by
  scaling it by $\lambda$.

* If $A$ is a bilinear form, a right eigenvector $v$ of $A$ is a vector that has
  the property that for all $u$, $u^T A v = u^T \lambda v = \lambda (u \cdot
  v)$. A left eigenvector is the same thing but for the left argument. This
  property sounds like just a roundabout way to say $Av = \lambda v$ but it
  means that if you have an orthonormal basis of eigenvectors of $A$, it's easy
  to describe what $A$ does in that basis.

Diagonal:

* A linear map whose matrix is a diagonal matrix is one that acts on each
  coordinate independently.

* A bilinear form whose matrix is diagonal is one that acts on each coordinate
  of the two vectors independently; it has no "cross terms".

All of this except for diagonality is coordinate free, so it works the same if
you change to a different basis. Some of it depends on the dot product, so it
only makes sense if it makes sense to take a dot product. I think it's worth
noticing when you do something that depends on your choice of coordinates, or
your choice of dot product, because it determines whether you can make these
choices arbitrarily or if they matter.[^pca]

[^pca]: An example that comes to mind is [PCA][pca]. PCA cares about the
    Euclidean distances between the points, so it only makes sense when it would
    make to take dot products. In particular this means that if you apply an
    arbitrary scaling to some columns of your data, the result of PCA will be
    different!

[pca]: https://en.wikipedia.org/wiki/Principal_component_analysis

## Bonus: quantum states and observables

(Disclaimer: I'm not a physicist and I don't really know what I'm talking about)

In quantum mechanics, an observable is represented by a linear operator $A$ that
acts on the quantum state $\psi$. The idea is that you write $\psi$ as a linear
combination of eigenstates of $A$, and in each eigenstate the value of $A$ is
given by the corresponding eigenvalue, and when you observe $A$ the state
collapses to one of the eigenstates.

It always seemed a bit weird to me that the result of the linear operator $A$
doesn't have a physical meaning and is hardly ever talked about, as if the
operator exists only to be a bag of eigenstates.

However, the expectation value of $A$ in the state $\psi$ is $\langle \psi | A |
\psi \rangle$ (which is basically physicist's notation for $\psi^T A \psi$). So,
maybe another way to think of $A$ is as a bilinear map, which when applied to a
quantum state gives the expected value of the observable in that state?[^weird]

[^weird]: There is one weird part of this interpretation: we've defined the
    expected value of an observable in every state, but not its whole
    distribution in any state. I think you could fix that by having the bilinear
    map $A$ return the whole probability vector of the observable, rather than
    just the expected value.

If you have an eigendecomposition of $A$, then you can represent any quantum
state as a linear combination of eigenstates, so that the expected value of the
observable in that state is a linear combination of its expected value in each
eigenstate. This explains why eigenstates are important.

This also explains why you want to work with density matrices. The density
matrix corresponding to $\psi$ is $| \psi \rangle \langle \psi |$, which is just
the outer product of $\psi$ with itself. As we've seen, this is enough
information to determine the expected value of any observable $A$. In density
matrix land, you can take linear combinations of pure states to represent mixed
states, and in a mixed state the expected value of any observable factors
through as a linear combination of its expected value in each of the pure
states.
