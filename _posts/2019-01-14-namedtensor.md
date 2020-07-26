---
toc: false
comments: true
layout: post
description:
categories: [programming]
title: Named tensors and labeled arrays
---

[NamedTensor](http://nlp.seas.harvard.edu/NamedTensor) is a proposal from
Harvard NLP researchers for enhancing tensors -- multi-dimensional arrays which
are the central object in many deep learning frameworks -- with named
dimensions. For anyone who's written code to work with multi-dimensional arrays
and had to deal with knowing which axis is which and making sure they line up, I
think this sort of thing can help a lot with maintainability and usability.

Many commenters on the NamedTensor post pointed out the similarity to
[xarray](http://xarray.pydata.org/en/stable/), which is an existing library that
brings labeled dimensions to numpy. I've been using xarray recently for some
work projects and I've found that it lets me write code that feels a lot cleaner
and more robust compared to the axis twiddling I would've done in raw numpy.
