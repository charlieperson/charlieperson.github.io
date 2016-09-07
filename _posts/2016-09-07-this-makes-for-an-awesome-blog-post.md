---
layout: post
title: "This makes an awesome blog post"
date: 2016-09-07
---
Let me ask you something- What does x equal in this snippet of code?
```
function inc(x) {
  return x + 1;
}
```
Obviously- we don't know yet because we haven't called it yet! The keyword 'this'
is no different.

If there is no context/subject (in other words-  if there is nothing on the left
side of the dot, in other words free form invocation) this will refer to the global object.
