---
layout: post
title: "Hash tables"
date: 2019-09-03
---

If you've ever used an object in JavaScript, you've used a hash table. Essentially,
it's an array of buckets. It is traditionally built with an array of linked lists.
The time complexity of retrieving or deleting a value from a hash table is constant,
while inserting into a hash table is amortized constant.

For a hash table to insert, retrieve, or delete a key value pair. It must use a hashing function.
To insert into a hash table. A key and a value is provided as input. The key is sent
to the hashing function, which returns a unique number for that specific key. The modulus operator
can be used to get the remainder of this unique number divided by the number of buckets
in the hash table. If the index is undefined (which it will be the first time a bucket is used),
a linked list is created at that index and the key/value pair is then added to it.

To retrieve of delete a value from a linked list. A key is provided. The key then
goes through the hashing function, which returns that key's unique number. The modulus operator
can be used to get the remainder of the unique number divided by the number of buckets
in the hash table. This will provide the index of which bucket that key can be found in.
Once we get our bucket's index, we can iterate through the linked list, until we get to
our key. If we are trying to retrieve the key's value we can simply return it.

However, if we want to delete a value, we must iterate through our linked list, and check
each object's next property to see if it is our desired key. If it is, then we must store
that object in a variable (let's call it 'first'). Next, our iterator will be the object
we want to delete. So, we must then set another variable to
store the iterator's next property (call it 'third'). Finally, we can reassign 'first's
next property to point to 'third'. This essentially cuts out the object we wanted to
delete from our linked list. With no reference to it anymore, it will eventually
get garbage collected.
