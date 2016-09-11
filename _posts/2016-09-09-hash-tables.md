---
layout: post
title: "Hash tables"
date: 2016-09-09
---

Hash function- one-way, single direction
(Input) => Hash(Ideally a number)

Encryption- two-way, both directions

If you've ever used an object in JavaScript, you've used a hash table. Essentially,
it's an array of buckets. Each bucket can either be another array, or a linked list.
Buckets are used to store key/value pairs. The time complexity of retrieving or
deleting a value from a hash table is constant

For a hash table to insert, retrieve, or delete a key value pair. it must implement a hash function. A hash function accepts
a string (or key) as input

it's a data structure that is traditionally built with an array of linked lists.
