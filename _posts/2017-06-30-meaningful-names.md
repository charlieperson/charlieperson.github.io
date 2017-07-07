---
layout: post
title: "Meaningful Names"
date: 2017-06-30
---

As programmers, a huge part of our job consists of coming up with names for things.
Whether it's a variable, method, class, or file, the readability of our code hinges
on using informative names that allow people to make intuitive assumptions about what
our code does. Some people might try and make the case that assumptions are bad.
However, I'd argue that assumptions are inevitable while initially assessing a program and
being able to make accurate assumptions based on well thought-out names can drastically
reduce the time that it takes to familiarize ourselves with new code.

But the benefits don't end there. Taking the time to think about the names that we use in our programs
can fundamentally change the way that we model our domain. By thinking about what a method or class
actually does, we can often drive refactors. For instance, sometimes it is tempting to name a method
doesThisAndThat. If we are tempted to use 'and' in our method names, it is an immediate indication
that the method does not follow the single responsibility principle and is most likely doing too much.
The thought process that we must go through in order to accurately assess what we name things, can
often lead to insights about our code and identify smells.

When naming things, keep in mind these rules of thumb:

- Names should provide clues to an author's intention.

- Make meaningful distinctions between variables and avoid noise words.

- Make names pronounceable - programming is a social activity, and being able to talk
about code with other programmers is crucial.

- The length of a name should correspond with the size of it's scope.

- The only thing worse than a non-descriptive name, is a misleading name.
