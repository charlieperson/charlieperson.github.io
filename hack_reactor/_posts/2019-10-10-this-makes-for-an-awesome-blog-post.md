---
layout: post
title: "This makes an awesome blog post"
date: 2019-10-10
---
Let me ask you something- What does x equal in this snippet of code?
```
function inc(x) {
  return x + 1;
}
```
Obviously- we don't know yet because we haven't called it yet! The keyword 'this'
is no different.

If there is no context/subject (if there is nothing on the left
side of the dot, or the function is called by means of free form invocation),
```
this
```
will refer to the global object window.

Take this example:

```
var ourObj = {
  g: 40,
  inc: function() { return this.g + 1; }
}

ourObj.inc()
```
Here, we do have a context/subject because ourObj is to the left of our function invocation
dot. Therefore the keyword ```this``` will be bound to ourObj while the function runs.
So, when inc is invoked, it does a lookup of the ```g``` property on ourObj, finds
that g points to a value of 40, increments it by one, and returns 41. This is by far
the most common usage of the keyword this, and most of the time knowing this rule
will be enough to find out what ```this``` is referring to in our code.

However, this is not always the case, and it's important to understand the other ways
that ```this``` can be bound to our functions. There are three main ways that we can
explicitly assign a function's reference to ```this```.
