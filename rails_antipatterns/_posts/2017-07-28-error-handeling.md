---
layout: post
title: "Error handling in Ruby"
date: 2017-07-15
---

An exception is an instance of a special type of class called Exception, or one of its
sub-classes. They indicate when something goes wrong in our programs. Most importantly,
if our program raises one of these exceptions, they will crash, unless we handle them.

### What does it mean to 'handle' an error?

Well, in programming, sometimes our applications will throw errors that
are out of our control. In these situations, it's our responsibility to handle
the potential error that may surface, and the more precise we can be in doing
so, the better.

##### Precise...?

Yes. There are all kinds of different exceptions that can be raised, but only a subset
of these that our programs can actually be responsible for. All of those in which
our program can potentially throw are within the StandardError subclass of the Exception
class. There are subclasses within the StandardError subclass as well. The goal is
to always rescue the most specific type of error that we expect in which also
encapsulates all possible errors. For example, a sub-class of StandardError is IndexError
which has two sub-classes- KeyError and StopIteration. Therefore, if we were rescuing
for a potential error that could be either a KeyError or a StopIteration error, then
we would rescue for IndexError. However, if the only potential error was a KeyError,
then we would just rescue for KeyError.

#### The bottom-line

We should never rescue for the generic Exception class, because within the Exception
class, there are errors that are impossible for our programs to raise. All of the
errors that our programs could potentially be responsible for raising are are sub-classes
of the StandardError class, and therefore should be the most generic type of error
that we ever rescue for.
