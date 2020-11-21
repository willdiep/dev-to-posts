Last Week, we learned about the fundamentals of Heaps. This week, we are goign to learn how to apply the concepts to JavaScript.

### Introduction

A heap data structure is a specialized tree data structure that satisfies the heap condition:

    In a max-heap, for any given element, its parent’s value is greater than or equal to its value.
    In a min-heap, for any given element, its parent’s value is less than or equal to its value.

A heap data structure is commonly implemented as a binary tree. In this lesson, we’re going to implement a min-heap in JavaScript. Min-heaps efficiently keep track of the minimum value in a dataset, even as we add and remove elements.

Heaps enable solutions for complex problems such as finding the shortest path (Dijkstra’s Algorithm) or efficiently sorting a dataset (heapsort).

They’re an essential tool for confidently navigating some of the difficult questions posed in a technical interview.

By understanding the operations of a heap, you will have made a valuable addition to your problem-solving toolkit.

```javascript
class MinHeap {
  constructor() {
    this.heap = [null];
    this.size = 0;
  }

  add(value) {
    this.heap.push(value);
    this.size++;
    this.bubbleUp();
  }

  popMin() {
    if (this.size === 0) {
      return null 
    }
    const min = this.heap[1];
    this.heap[1] = this.heap[this.size];
    this.size--;
    this.heap.pop();
    this.heapify();
    return min;
  }

  bubbleUp() {
    let current = this.size;
    while (current > 1 && this.heap[getParent(current)] > this.heap[current]) {
      this.swap(current, getParent(current));
      current = getParent(current);
    }
  }

  heapify() {
    let current = 1;
    let leftChild = getLeft(current);
    let rightChild = getRight(current);
    // Check that there is something to swap (only need to check the left if both exist)
    while (this.canSwap(current, leftChild, rightChild)){
      // Only compare left & right if they both exist
      if (this.exists(leftChild) && this.exists(rightChild)) {
        // Make sure to swap with the smaller of the two children
        if (this.heap[leftChild] < this.heap[rightChild]) {
          this.swap(current, leftChild);
          current = leftChild;
        } else {
          this.swap(current, rightChild);
          current = rightChild;
        }
      } else {
        // If only one child exist, always swap with the left
        this.swap(current, leftChild);
        current = leftChild;
      }
      leftChild = getLeft(current);
      rightChild = getRight(current);
    }
  }

  swap(a, b) {
    [this.heap[a], this.heap[b]] = [this.heap[b], this.heap[a]];
  }

  exists(index) {
    return index <= this.size;
  }

  canSwap(current, leftChild, rightChild) {
    // Check that one of the possible swap conditions exists
    return (
      this.exists(leftChild) && this.heap[current] > this.heap[leftChild]
      || this.exists(rightChild) && this.heap[current] > this.heap[rightChild]
    );
  }
}

const getParent = current => Math.floor((current / 2));
const getLeft = current => current * 2;
const getRight = current => current * 2 + 1;

module.exports = MinHeap;

```





### MinHeap Class

Our MinHeap class will store two pieces of information:

    An array of elements within the heap.
    A count of the elements within the heap.

To make our lives easier, we’ll always keep one element at the beginning of the array with the value null. By doing this, we can simplify our coding by always referencing our minimum element at index 1 instead of 0 and our last element at index this.size instead of this.size - 1. 

```javascript
const minHeap = new MinHeap();
console.log(minHeap.heap);
// [ null ]
console.log(minHeap.size);
// 0
```


### Bubble Up 

Our MinHeap needs to satisfy two conditions:

    The element at index 1 is the minimum value in the entire list.
    Every child element in the list must be larger than its parent.

Let’s define an .add() method which will allow us to add elements into the .heap array. We will also define .bubbleUp() which will do the work of maintaining the heap conditions as we add additional elements.

```javascript
class MinHeap {
  constructor() {
    this.heap = [ null ];
    this.size = 0;
  }
  
  add(value) {
    this.heap.push(value);
    console.log(`.. Adding ${value}`);
    console.log(this.heap); 
    this.size++;
    this.bubbleUp();
  }
  
  bubbleUp() {
    console.log('Bubble Up');
  }
}
module.exports = MinHeap;

```


### Parent and Child Elements

Great work so far! Our MinHeap adds elements to the internal heap, keeps a running count, and has the beginnings of .bubbleUp().

Before we dive into the logic for .bubbleUp(), let’s review how heaps track elements. We use an array for storing internal elements, but we’re modeling it on a binary tree, where every parent element has up to two child elements.

Child and parent elements are determined by their relative indices within the internal heap. By doing some arithmetic on an element’s index, we can determine the indices for parent and child elements (if they exist).

    Parent: (index / 2), rounded down
    Left Child: index * 2
    Right Child: (index * 2) + 1

These calculations are important for the efficiency of the heap, but they’re not necessary to memorize, so we have provided three helper functions: getParent(), getLeft(), and getRight() in MinHeap.js.

These helpers take an index as the sole parameter and return the corresponding parent or child index.

```javascript
const { MinHeap, getParent, getLeft, getRight } = require('./MinHeap');

// instantiate MinHeap and assign to minHeap
const minHeap = new MinHeap();

// sample content of minHeap
minHeap.heap = [ null, 10, 13, 21, 61, 22, 23, 99 ];

// display content of minHeap
console.log(minHeap.heap);

// display the current value, its parent value, left child value and right child value
// replace null with the correct way to access the values of the parent, left child and right child
const current = 3;
const currentValue = minHeap.heap[current];
console.log(`Current value of ${current} is ${currentValue}`);
console.log(`Parent value of ${currentValue} is ${minHeap.heap[getParent(current)]}`);
console.log(`Left child value of ${currentValue} is ${minHeap.heap[getLeft(current)]}`);
console.log(`Right child value of ${currentValue} is ${minHeap.heap[getRight(current)]}`);
```