---
layout: post
title: "Object Oriented"
date: 2016-09-21
---

Ahhh- buzz words. Object Oriented programming languages were built to fulfill the
need to organize unmanageable code bases in a way that resembles the real world.

4 things-

Abstraction means that we can have an idea or a concept that is completely separate from a specific instance.
 - what we do when we make a class
 - we don't make a Joe's Bank Account class and a Sally's Bank Account class. We
   focus on the essential qualities of the idea.
 - focus on the essential qualities of something rather than one specific example
 - ignore the irrelevant
 - ignore the unimportant

Encapsulation- think capsule (the idea of surrounding something)
 - Not just to keep the contents of something together, but also to protect the contents
 - The restriction of access to the inner workings of that class. Data hiding.
 - An object shouldn't reveal anything about itself except what is completely necessary for the rest of the app to work.
  - restrict access to attributes so that it is only accessible inside of an object itself
  - It's about reducing dependencies between different parts of the app.

Inheritance- one class (subclass), inheriting attributes and behaviors from another(superclass).
 - Enables code re-use
 - Makes it easier to think about programs like we do real life.

Polymorphism-
 - Goes hand in hand with inheritance. If an instance of a subclass inherits methods from a
   superclass, but the subclass has a method that needs to work in a slightly different
   way than the one inherited from the superclass, than the subclass can simply
   write it's own method with the same name(shadow) the method, which will override
   the superclass' method.

   For example:

```
  class Person {
    private String name;
    private int age;

    public void drinkMilk() {
     System.out.print('Yum')
    }
  }

  class LactoseIntolerantPerson extends Person {
    public void drinkMilk() {
     System.out.print('BLEHHHHH!!!!!')
    }
  }

```

  - So, in this case, if we made a new Person instance, the instance would have
  name, and age attributes, and a method called drinkMilk that would result in
  'Yum' being printed to System.out. Now, if we made an instance of a LactoseIntolerantPerson,
  it would also have name and age attributes (inherited from the Person class). However,
  if we called drinkMilk on this instance, the result wouldn't be so pretty. BLEHHHHH would
  be printed to System.out because it's drinkMilk method shadows or overrides the superclass'
  drinkMilk method. This is a basic example of how polymorphism can be useful.
