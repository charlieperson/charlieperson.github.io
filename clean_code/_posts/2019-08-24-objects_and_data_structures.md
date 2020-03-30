---
layout: post
title: "Objects and Data Structures"
date: 2019-08-24
---

## Data Abstraction

Data abstraction is fundamental in object oriented programs. There are things about
our programs that people don't need to know. People should not know about the inner
workings of a class. If I want my car to turn left, I don't have to understand how
the axel connects with the frame, which pivots the two front wheels- and I shouldn't
have to. The complexity of the task's implementation is abstracted away from me. As
long as I get the result I'm looking for, the details are not important.

The means by which we choose to expose our variables and methods says so much about
our system. It is an indication of what the outside world should know about our
program. We must think critically about the best way to represent the data that an
object contains and not just add getters/setters for convenience. Our implementation
should be hidden- and we hide implementation through abstractions.

## Objects vs Data Structures
"Objects hide their data behind abstractions and expose functions that operate on
that data. Data structures expose their data and have no meaningful functions."
  -Uncle Bob

One is not superior over the other. In fact, they are pretty much the opposite of
one another. It is our job, as engineers to determine how to build our programs and
leverage the pros and cons of each given what we are trying to build.

Before determining whether to use a data structure or an object, we must understand
how they differ. Code that uses objects is object-oriented (simple enough), whereas
code that uses data structures is procedural. Data structures have expose their
data to the world to be manipulated by methods in an external class. The consequences
of this type of architecture is that it makes it very easy to add functions without
changing the existing data structures, because we only have to implement them in one
place. However, it's more difficult to create new data structures because, consequently,
all of the functions must change.

The other approach is to use objects. When deciding to use objects, we must consider
how they differ from data structures. When writing object oriented code, it's very
easy to add new objects, however, adding new functions is more difficult due to
the fact that we must implement any new functions in each existing and future object
that we create.

Knowing how these two different approaches work, allows us to make educated decisions
on which one to use. If we care more about being able to add new data types rather
than new functions, than we can feel confident that an O.O. approach will be best.

## The Law Of Demeter
The fundamental basis of the Law of Demeter revolves around separating concerns, and
reducing dependencies in our modules. This means that our objects should have limited
knowledge about other objects. In practice, this means that methods should not call
methods on objects that are returned from methods within the same class. The moment
that we break this rule, we've created a dependency on an external class. The law
only applies to objects though and not to data structures, because data structures
expose their internals by their nature and therefore it is not a smell to access
the internal values.
