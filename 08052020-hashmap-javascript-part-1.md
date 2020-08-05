---
title: How to Create a Hashmap in JavaScript (Part 1)
published: true
---

## Intro to Hash Maps

Hash maps are data structures that serve as efficient key-value stores. They are capable of assigning and retrieving data in the fastest way possible. This is because the underlying data structure that hash maps use is an array.

A value is stored at an array index determined by plugging the key into a hash function. Because we always know exactly where to find values in a hash map, we have constant access to any of the values it contains.

This quick access to values makes a hash map a good choice of data structure whenever we need to store a lot of values but need fast look-up time.

In JavaScript, objects are often used to map keys to values as in a hash map, but in this lesson, you’ll create your own implementation of a hash map by building out a HashMap class. You’ll build methods to hash and compress a given key, assign an index at which to store a value, and retrieve that value.

To implement a hash map, the HashMap constructor method will create an empty array that will hold values. A hashing function will return an index in the array where the value will be stored. While going through the following exercises, remember that the purpose of this lesson is to gain a deeper understanding of the data structure rather than creating a production-quality data structure.

```javascript
class HashMap {
  constructor(size = 0) {
    this.hashmap = new Array(size)
      .fill(null);
  }
}
```

## Hashing

The hashing function is the secret to efficiently storing and retrieving values in a hash map. A hashing function takes a key as input and returns an index within the hash map’s underlying array.

This function is said to be deterministic. That means the hashing function must always return the same index when given the same key. This is important because we will need to hash the key again later to retrieve the stored value. We won’t be able to do this unless our hashing function behaves in a predictable and consistent way.

Getting an integer representing an index can be done by summing the character codes, or integer representation, of all the characters in the key, a string. A variable can be used to keep track of the running total of the character codes until .hash() is finished looping over the key and the sum can be returned.

The code for the hashing function should look something like this:

```
declare hashCode variable with value of 0

for each character in the key
  add the character code value to hashCode

return hashCode
```

```javascript
class HashMap {
  constructor(size = 0) {
    this.hashmap = new Array(size)
      .fill(null);
  }

  hash(key) {
    let hashCode = 0;

    for (let i = 0; i < key.length; i++) {
      hashCode += hashCode + key.charCodeAt(i);
    }

    return hashCode
  }
}
```

## Compression
The current hashing function will return a wide range of integers — some of which are not indices of the hash map array. To fix this, we need to use compression.

Compression means taking some input and returning an output only within a specific range.

In our hash map implementation, we’re going to have our hashing function handle compression in addition to hashing. This means we’ll add an additional line of code to compress the hashCode before we return it.

The updated .hash() should follow these steps:

```
initialize hashCode variable to 0

for each character in the key
   add the character code and hashCode to hashCode

return compressed hashCode
```

```javascript
class HashMap {
  constructor(size = 0) {
    this.hashmap = new Array(size)
      .fill(null);
  }

  hash(key) {
    let hashCode = 0;
    for (let i = 0; i < key.length; i++) {
      hashCode += hashCode + key.charCodeAt(i);
    }
    return hashCode % this.hashmap.length;
  }
}
```








