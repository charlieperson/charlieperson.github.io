---
layout: post
title: "Rails Callbacks"
date: 2017-08-05
---

## What is a callback in Rails?
It's just a hook that can be configured to happen before, after, or even around
a particular event related to an ActiveRecord object. Some of these events include
save, validate, create, etc.

## The Pain
So, all of this sounds good right- it might even seem like callbacks are a very
useful feature that Rails provides us, and you would be right. They can be useful.
Especially at the beginning, when applications are small and relatively simple.
The kicker, is when we start to extend our applications. As they expand in complexity,
we often find ourselves having to avoid callbacks given certain situations or
edge cases using conditionals. They have the potential to make our code more difficult to
read, and test. If we are testing our models (as we always should) we will start to
notice callbacks causing us trouble. This is because we often have to stub out callbacks
or create additional objects or data in order for the test to not error out.

```
class FriendRequest < ActiveRecord::Base
  after_save :notify_followers

  def accept
    self.accepted = true
    save
  end

  def notifyRecipient
    requestor.notify
  end

end
```

Take this example for instance. If we were to try and test the accept method, we
would either have to stub out our after_save callback, or we would have to provide
the test FriendRequest object with a requestor attribute, when really, we shouldn't
care about testing our callback in this test (because we should have already done that
in another test). If we did not take one of the precautions mentioned above, we would
run into a nil value error.

## The sad truth
When we see after_save callbacks, or after_update, or really after anything related to
our object, it is more than likely an indication that we are breaking the single
responsibility principle. This is because we usually, save or update our object, and
then need to reach outside of itself to perform some sort of necessary side effect
so that our app performs the way we want it to, and/or doesn't blow up.

## The Conclusion
Callbacks are often smelly because they often break the SRP. Here's a rule we can
follow that will ensure that we use callbacks for good- and not evil. If we only use
callbacks when the logic refers to state internal to the object, we're good. Otherwise,
we probably need to really think about our domain, because we very well may be missing
something.
