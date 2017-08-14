---
layout: post
title: "Error Handling"
date: 2017-08-11
---

## Errors

There are things that can happen that are out of our control. A third party server
might hang, a device might run out of power, or two requests could come in simultaneously.
For these types of things- we need error handling. Before we had error handling,
we would either set error flags, or return an error code that could be checked by the
caller. Error handling, when done correctly, massively increases the readability
of our code, and makes for a more robust application.

We can use try-catch-finally blocks to help us elegantly handle our exceptions.
Within the try block, we execute our risky code, within the catch block, we handle
anything that might have gone wrong, and within the finally block, we can execute
code that we want to happen regardless of whether or not an exception was thrown.

```
try {
  // attempt to retrieve a file
} catch(FileNotFoundException e) {
  // throw an error and do any necessary clean up
} finally {
  // continue the execution of the program
}
```

## Use Unchecked Exceptions When Possible
Checked exceptions break the open/closed principle. Plain and simple. If we are
catching an exception three levels above where the code that caused the exception
ran, then that means that a high-level method knows about, and is therefore
coupled to a low-level method that it should not have any dependency on. This completely
breaks encapsulation and creates a dependency chain until we actually handle our exception.
For these reasons, checked exceptions should be avoided when possible.


## Don't return null
Methods that return null guarantee future pain. We find ourselves continuously having
to check if a property exists, and it often forces us to write double the code that
we would have to write otherwise. One thing if our value evaluates to nil, and another
thing if it is anything aside from nil. We should be
