---
toc: false
comments: true
layout: post
description: Monad tutorial not included
categories: [ppl]
title: Links on computational abstractions
---

Here are some links relating to a few different threads I've been thinking about
lately, which for me tie into a common theme of "functional programming
abstractions on which to build a probabilistic modeling language".

## Algebraic effects

[Adding an Effect System to OCaml][ocaml-effects] (video). I had seen this talk
before but had since forgotten the idea of algebraic effects, so I read up on
them again. My one-sentence summary: effects are like resumable exceptions that
are tracked by the type system.

[ocaml-effects]: https://www.janestreet.com/tech-talks/effective-programming/

I've worked with OCaml code that uses monads to model effects, so I was
interested in how that compares to this kind of effect system. (Sorry, I'm not
going to explain monads here.) It seems to me that the behaviors that can be
implemented with effects are a subset of those that can be implemented with
monads: those where each piece of code is run at most once. The upshot is that
effect handling can be implemented efficiently in the compiler, without
allocating many intermediate closures like monadic code tends to do.

The other benefit is that different effect types can be mixed with each other
and with non-effectful functions more easily. This is basically the same idea
as [Freer Monads and Extensible Effects][freer].

[freer]: http://okmij.org/ftp/Haskell/extensible/

Also interesting: [Algebraic effect handling in numerical Python with Jax][jax].

[jax]: https://twitter.com/sigfpe/status/1296196451152703488?s=20

Effect handling is one approach for implementing inference operations that
operate on probabilistic programs. As one example, [Pyro is implemented with
effect handlers][pyro] in a limited form.

[pyro]: http://pyro.ai/examples/effect_handlers.html

## Build systems and incremental computation

[The Success and Failure of Ninja][ninja] (blog post). This is an interesting
retrospective on maintaining a popular software project. Most of it is not too
related to the other stuff I'm putting together here, except as a link to...

[ninja]: http://neugierig.org/software/blog/2020/05/ninja.html

[Build Systems à la Carte][build-systems] (2018 paper). I'd read this paper
before: it inspired the design of a library for describing incremental
computation graphs that I've worked with in my day job.

[build-systems]: https://www.microsoft.com/en-us/research/uploads/prod/2018/03/build-systems-final.pdf

The main idea is that a computation graph is described by a set of keys, and a
function that takes a key and builds a value associated with that key given a
way to build its dependencies. In the paper, this is called a "task
description".

A build system implements a function that takes a task description and uses it
to update a persistent key-value store. The rest of the paper compares different
build systems viewed in this way.

## Incremental state machines and the arrow calculus

[Bonsai][bonsai] is an OCaml web framework developed at Jane Street based on the
idea of components as incremental state machines.

[bonsai]: https://github.com/janestreet/bonsai

Bonsai's API has gone through a few interesting evolutions, the latest iteration
of which is something called [Bonsai.Proc][proc]. The story is this: Bonsai's
primary abstraction is the *arrow*, which is like a monad, but with more
restricted control flow allowing for more static analysis. However, the Bonsai
team found that arrow combinators are a bad API, so they found a way to mostly
get rid of them.

[proc]: https://github.com/janestreet/bonsai/blob/master/docs/proc.md

The proc API is inspired by the [Arrow Calculus][arrow-calculus] (2010 paper),
an equivalent formulation of arrows that enables composition using lambda-like
abstractions rather than combinators. The result is something that is nicer to
program with and similar to a monad interface.

[arrow-calculus]: http://homepages.inf.ed.ac.uk/slindley/papers/arrow-calculus.pdf

Incidentally, the [Dune build system][dune] also used to use an arrow
abstraction internally, and they *also* dropped the arrow combinators in favor
of [a different abstraction][selective-functors]. I guess there is a good reason
that arrows haven't caught on very much even in functional programming.

[dune]: https://dune.build/
[selective-functors]: https://www.staff.ncl.ac.uk/andrey.mokhov/selective-functors.pdf

Anyway, I'm interested in Bonsai because the core abstraction -- of composable
building blocks that maintain their own internal state and implement incremental
computations -- is very similar to the feature set we were aiming for in my
previous work on probabilistic programming interfaces. I'd like to explore the
idea of a "probabilistic component" framework for composing models and inference
algorithms.
