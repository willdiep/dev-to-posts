---
title: How to Create a Hashmap in JavaScript Part 1
published: false
---

## Basic Hash Maps

Now that we have all of the main ingredients for a hash map, let’s put them all together. First, we need some sort of associated data that we’re hoping to preserve. Second, we need an array of a fixed size to insert our data into. Lastly, we need a hash function that translates the keys of our array into indexes into the array. The storage location at the index given by a hash is called the hash bucket.

Let’s use the following example for our hash map:


| Key: Album Name | Value: Release Year |
| --------------| ------------ |
| People’s Instinctive Travels and the Paths of Rhythm | 1990     |
| The Low End Theory        | 1991     |
| Midnight Marauders   | 1993     |
| Beats, Rhymes and Life      | 1996         |


![saving keys](https://i.stack.imgur.com/zHvEe.jpg)

<sub>[Image credits to StackOverflow post](https://stackoverflow.com/questions/6493605/how-does-a-java-hashmap-handle-different-objects-with-the-same-hash-code)</sub>
