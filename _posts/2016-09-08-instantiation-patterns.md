---
layout: post
title: "Instantiation patterns"
date: 2016-09-07
---
The difference between an object decorator and a class is only that a class creates
the object that it is augmenting.

Let me be clear- a class is any construct capable of creating many similar objects that all
conform to an interface. Because JavaScript is such a flexible language, there
are many ways to make classes. We will cover four of the most common ones:

## Functional Class Pattern:
```
function Car(model) {
  var car = {};
  car.position = 0;
  car.model = model;
  car.move = function move() { car.position += 1 };

  return car;
}
```
Pros: very simple, readable, and speaks for itself.  
Cons: duplication of methods for each instance. *This is only a concern when
thousands and thousands of instances will be created in an application which is
usually not the case, and typically well worth the simplicity if you ask me*

## Functional Shared Class Pattern:
```
function Car(model) {
  var car = {};
  car.model = model;
  Object.assign(car, CarMethods)
  return car;
}

CarMethods = {
  move: function(){ this.position += 1; },
  honk: function(){ console.log("Beep!"); };
}
```
Pros: reusing the same methods for each instance.  
Cons: using keyword 'this' in our methods can be confusing and cause problems depending on how
the method is called. Also, Object.assign is an ES6 feature.

## Prototypal Class Pattern:
This pattern takes advantage of instances delegating up the prototypal chain.
For instance: *(that was a code joke in case you missed it)*
```
function Car(model) {
  var car = Object.create(CarMethods);
  car.model = model;                    
  return car;
}

CarMethods = {
  move: function(){ this.position += 1; },
  honk: function(){ console.log("Beep!"); };
}
```
Here, each instance of Car delegates failed lookups to CarMethods.

Pros- We can take advantage of Prototype chains, and even mask methods higher in the chain.
Cons- using keyword 'this' in our methods can be confusing and cause problems depending on how
the method is called.

## Pseudoclassical Class Pattern:
```
function Car(model) {
  this.model = model;
}

  Car.prototype.move: function(){ this.position += 1; },
  Car.prototype.honk: function(){ console.log("Beep!"); };
```
When the ```new``` keyword is used to create a new instance of Car e.g. ```var ford = new Car('ford')```
it runs the function in "constructor mode" which means that the interpreter implicitly
changes the code to look like this:
```
function Car(model) {
  this = Object.create(Car.prototype);
  this.model = model;
  return this;
}

  Car.prototype.move: function(){ this.position += 1; },
  Car.prototype.honk: function(){ console.log("Beep!"); };
```
Fundamentally, this is no different from the prototypal pattern. We are simply
substituting instances' delegation to the CarMethods object, to the Car.prototype
object.

Now, you may be wondering, why we did not create ```Car.prototype = {}```. That's
because each new function ships with an empty ```.prototype``` property that is intended for
storing methods. *NOTE:* There is nothing special about this ```.prototype``` property.
A lookup of Car.move or Car.honk would give us undefined. Car DOES NOT have any
sort of special delegation to it's own prototype property-
like all other functions, it delegates failed property lookups where all functions
delegate failed property lookups - Function.prototype

Pros- We can take advantage of Prototype chains and Object delegation.  
Cons- The awful naming convention of prototype can lead people to believe that
there is something special about a function's .prototype property, when really
there isn't. Also, using keyword 'this' in our methods can be confusing and cause problems depending on how
the method is called.
