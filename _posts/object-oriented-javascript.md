---
layout: post
title: "Class Inheritance in JavaScript"
date: 2016-09-12
---

Object oriented (OO) languages traditionally use class inheritance as a way to organize,
reuse, and give their code a more natural feel. For example, I might have a Person
class with functions inside of it that are common between all different types of
people like 'eat' or 'sleep'. Person is considered a super class in this example.

Then, I might make sub-classes that inherit from the Person class, like FigherFighter,
or Developer. The idea is, that these classes will have functions that are more
specific to that sub-class. Instances of the FigherFighter class might have a
function called 'putOutFire', whereas instances of the Developer class might have
a function called 'code'. However, both sub-classes will have access to their parent
class' functions as well, because hey- we all gotta eat right?

JavaScript is not an OO language by design, however- it's a very flexible language.
Therefore, it's possible to take an object oriented approach when using working with it.
There are two main methods for the implementation of object oriented JavaScript
depending on whether one is using functional instantiation or pseudoclassical.

Functional-

Here's an example of implementing class inheritance when using the functional
instantiation pattern in JavaScript.

This is going to be our superclass.

```
function Car(model) {
  var obj = {};
  obj.model = model;
  obj.miles = 0;
  obj.drive = function(distance) {obj.miles += distance}
  return obj;
}
```
Next, we'll create a sub-class that will get all of the characteristics of a car,
but also make some special characteristics unique to trucks.

```
function Truck(model) {
  var obj = Car(model);
  obj.tow = function(){console.log("Towing a car")}
  return obj;
}
```
