---
layout: post
title: "Class Inheritance in JavaScript"
date: \
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
Therefore, it's possible to take an object oriented approach when working with it.
There are two main methods for the implementation of object oriented JavaScript
depending on whether one is using either the functional or pseudoclassical instantiation pattern.

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

Pseudoclassical-

Here's an example of implementing class inheritance when using the pseudoclassical
instantiation pattern in JavaScript. It's a little bit more complicated due to the
use of the 'this' key word. But it makes sense, and it is quite easy to follow
what's happening as long as we remember what happens under the hood when JavaScript
runs into the 'new' keyword.


In this example, Person will serve as our super class.
```
function Person(name) {
  this.name = name
}
Person.prototype.eat = function(){};
```
Then, we can make a sub-class called BusinessMan.
```
function BusinessMan(name) {
  Person.call(this, name);
}

BusinessMan.prototype.openBriefCase = function(){}
```
Now, think about what will happen when we call ```var mike = new BusinessMan```.

Well, first of all, the 'this' keyword will be set to a brand new objet that delegates
failed lookups to BusinessMan.prototype. Next, we pass 'this' new object into the Person
constructor function WITHOUT the new keyword. Therefore, every time the Person class
refers to 'this'- it is referring to the object that we passed in. This will add a
name property to our BusinessMan object, and set it to the second argument passed into
Person.call().

At this point, if we were to call mike.openBriefCase, we would not find a property
called openBriefCase within the mike object, so it would delegate to BusinessMan.prototype
where it would find the property and call the function. However, if we were to call
mike.eat() we would get an error. This is because we would first look inside of the
mike object for a property called eat but would not find it, so we would delegate up
to the BusinessMan.prototype object, where it would also not find it. Finally, it
would look for the property in Object.prototype and be unsuccessful there too.

We need to delegate failed lookups in BusinessMan.prototype to Person.prototype.
Simple enough-

```
BusinessMan.prototype = Object.create(Person.prototype);
```
So now, if we call mike.eat, we would look in the mike object without any luck,
delegate to BusinessMan.prototype, fail there too, delegate to Person.prototype,
find the property, and call the function. There are just a few things to keep in
mind. Firstly, we are REASSIGNING our BusinessMan.prototype object to point to
a brand new object that delegates failed lookups to Person.prototype. Because of
this, two things are crucial. Firstly, the BusinessMan.prototype constructor property
will no longer be defined so we should explicitly do that after our reassignment.  

Like this:
```
BusinessMan.prototype = Object.create(Person.prototype);
BusinessMan.prototype.constructor = BusinessMan;
```
Finally, we must ensure that any BusinessMan.prototype property assignments happen
after these two lines of code, or they will disappear due to our reassignment.
