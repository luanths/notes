---
toc: true
comments: true
layout: post
description: A generalization of a math contest problem
categories: [math]
title: Putnam spheres
---

[Putnam][putnam] 2019 A4 asks if there exists a function f(x, y, z) from
$\mathbf{R}^3$ to $\mathbf{R}$, that integrates to zero over the surface of
every unit sphere, but is not identically zero.

[putnam]: https://www.maa.org/math-competitions/putnam-competition

My coworkers were discussing this problem and its generalization: what about in
n-dimensional space?

We think that the answer is yes for all n, and that it's enough for f to be an
axis-aligned plane wave, that is f(x, y, z, ...) = cos(kx) for some frequency k.

Surprisingly (to my intuition), all we need to do is find k such that cos(kx)
integrates to zero over the unit sphere *centered at zero*. If it does, then it
integrates to zero over *any* unit sphere.

This is essentially because you can make any shifted copy of cos(kx) using a
[linear combination][lc] of cos(kx) and sin(kx), and we know that sin(kx)
integrates to zero over the unit sphere centered at zero because sin is an [even
function][even], so all we need is for cos(kx) to integrate to zero for some k.

[lc]: https://en.wikipedia.org/wiki/List_of_trigonometric_identities#Sine_and_cosine
[even]: https://en.wikipedia.org/wiki/Even_and_odd_functions

Does such a k always exist? It seems like it should, because things are
continuous as a function of k. For the particular case of n = 3, k comes out
particularly clean because of a [coincidence in 3 dimensions][archimedes].

[archimedes]: https://www.scottaaronson.com/blog/?p=4432
