---
layout: post
title: "Where should ActiveRecord queries go?"
date: 2017-07-21
---

## In our models.

### Why?

Because it's an ActiveRecord query and we should not be making queries directly
inside of our controllers.

.where as well as other ActiveRecord queries should not be inside of our controllers.
because our controllers should not know about the inner workings of our
models. We should tell our models to give us what we want. This type of logic should
always go inside of our models. There are two ways
to extract this logic into the model level. The first way is to use scopes, and the
second way is to use class methods.

What's the difference? Good question. Under the hood, there actually isn't one.
ActiveRecord converts our scopes into class methods anyway, so scopes are really just
syntactic sugar.

Soooooo what's the point?

Well, let's take an example. Like a friend request that can be either pending,
accepted, or declined. We might want to filter all of a user's requests by a certain
parameter that they supply to us. The scope might look like this:

```
class Request < ActiveRecord::Base
  scope :by_status, -> status { where(status: status) }
end
```

ActiveRecord would translate this to:

```
def self.by_status(status)
  where(status: status)
end
```
Not much of a difference here. Just more lines of code. However, what if the parameter
is required? With scopes, it's simple.

```
scope :by_status, -> status { where(status: status) if status.present? }
```

This way, when we pass our scope an empty string or nil, it returns an empty ActiveRecord
relation. However, if we had a class method like this:

```
def self.by_status(status)
  if status
    where(status: status)
  end
end
```

and then we called:

```
Request.by_status(nil)
```
Then it simply returns undefined. This example highlights the main benefit of using
scopes over class methods, which is that they can be chained together with confidence
knowing that you will not get a ```NoMethodError```.

## To conclude

One is not necessarily superior to the other. Certain circumstances may make scopes
a more appropriate choice, while others may call for class methods. When making
that decision keep in mind the following:

- Scopes are good for small queries, are chain-able, and better for extensibility
- Once logic begins to get complex, it may be better to use a class method for readability
