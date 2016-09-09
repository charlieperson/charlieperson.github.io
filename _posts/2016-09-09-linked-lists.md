---
layout: post
title: "Linked Lists in JavaScript"
date: 2016-09-07
---

A linked list is a data structure that is a lot like what it sounds like. A list
of items linked to one another.

Each linked list has a head pointer (a variable pointing to the first item),
a tail (a variable pointing to the last item), and x amount of
items (also called nodes) in between. Each node is comprised of a value, and a reference.
Think of the value as the data that the node holds, and the reference as a pointer
to the next node.

The benefit of using a linked list over an array is that linked lists
never need to be resized. This is because pushing an item to a linked list is always constant.
Linked lists allocate memory per node. Unlike an array, they don't create a certain
amount of spaces of memory, and then allocate more once all of the spaces are filled.

On the contrary, pushing an item to a linked list is always constant. When creating
a linked list, two bits of memory are requested so that the first node can be created.
The first bit stores the value, and the second bit stores the reference, which is
initially empty because there are no other nodes yet. At this point, both the head,
and the tail point to this node (there's only one, so it's the beginning and the end).

If we would like to push another node to our linked list, two more bits of memory
are requested. Then, we set our current tail's reference to point to our new node,
and then reassign our tail to the new node. If we wanted to add another- same story.
Make a node, assign the current tail's reference to the node, and reassign our tail
to the new node.

This is pretty cool. No resizing. However, of course there's a catch. The nature of
linked lists makes looking up particular items in our list less efficient then an array.
If I know the index of the item in an array, I can go straight to that index. But
one cannot simply go to an index of a linked list, because there are no indices.
There are only nodes- each having a value, and a reference to the next one.

Therefore, if I wanted to retrieve a specific node, I would have to start from the
head, check if it's my node, if it's not, follow its reference to the next node,
check if it's my node, if it's not, follow its reference to the next one........ and so on.
Finding the length of a linked also has a linear time complexity for the same reason.
We start at the head, and count one by one until we get to a node with an empty reference
which has to be our tail.

So, enough with the conceptual stuff. To implement a linked list in JavaScript:

Here's our node constructor:
```
var Node = function(value) {
  var node = {};
  node.value = value;
  node.next = null;    
  return node;
};
```
And here's our linked list constructor:
```
var LinkedList = function() {
  var list = {};
  list.head = null;
  list.tail = null;

  list.addToTail = function(value) {
    var node = Node(value);           // make a node with desired value
    if(list.head === null) {          // if it's our first node
      list.head = node;               // set head and tail to point to it
    }
    if(node !== list.head) {          // if our new node is not our head (only true for first node)
      list.tail.next = node;          // set the tail's reference to the new node
    }
    list.tail = node;                 // set the tail to the new node
  };

  return list;
};
```
And that's it! A beautiful linked list implemented in JavaScript.
