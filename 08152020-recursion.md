---
title: Recursion in JavaScript
published: false
---

Have you ever thought about what would happen if you called a function or method from within that function or method? That’s called recursion and can actually make your program more efficient. It can be used for problems that can be broken up into multiple steps, often ones that you would otherwise solve iteratively. It will also be used in some of the traversal and sort algorithms that you will see later.


## Introduction to Recursion

You’ve heard about a trendy new spot that sells fruit sandwiches. What are fruit sandwiches? You have no idea, but you’re eager to find out!

Sadly, when you arrive at the store, the line is out the door and around the block. Undeterred, you hatch a plan to find out how many people are in line before you.

You tap the person in front of you and ask them how many people are ahead of them. They have no idea, (the line is huge!) so they ask you to wait a moment and tap the person in front of them, repeating this process through the line.

Finally, the second to last person taps the person at the front of the line. Nobody is ahead of them, so they reply “It’s just me so: one person!”. Then this message is repeated back down the line.

The next person says “okay, there was one person ahead of me, I’ll add myself… I can tell the person behind me: 2 people in line.”

Each person waiting for a reply:

1. receives the message
1. adds themselves to the count
1. responds to the person tapping them

This chain eventually reaches you with the final number. Your plan was a success!

You executed a recursive strategy. The “function” of asking a person involved asking a person. The self-referential logic can seem like it goes on forever, but each question brings you closer to the front of the line where no more people are asked about the line.

Your approach had two aspects which are essential to recursive thinking. Break the problem into two possibilities:

1. There’s nobody left in line, don’t ask
2. There’s someone in line, ask them

We repeat Step 2 with a different input which brings us closer to Step 1.

![queue](https://s3.amazonaws.com/zweb-s3.uploads/carp/2011/08/iStock_000001999765XSmall.jpg)

<sub>[Image credits to CARP.ca](https://www.carp.ca/2015/10/13/thanks-for-the-long-line-ups-at-the-advance-polls/)</sub>



### Recursion Outline

Recursion is a strategy for solving problems by defining the problem in terms of itself. For example, to sum the elements of a list we would take the first element and add it to the sum of the remaining elements.

How would we get that sum of remaining elements? Easy! We’d take the first element of the remaining elements and add it to the… Maybe you can understand why recursion can be a tricky subject!

In programming, recursion means a function definition will include an invocation of the function within its own body. Here’s a pseudo-code example:

```
define function, speller
  if there are no more letters
    print "all done"
  print the first letter
  invoke speller with the given name minus the first letter
```

If we invoked this function with “Zoe” as the argument, we would see “Z”, “o”, and “e” printed out before “all done”.

We call the function a total of 4 times!

1. function called with “Zoe”
1. function called with “oe”
1. function called with “e”
1. function called with “”

Let’s break the function into three chunks:

```
if there are no more letters
    print "all done"
```

This section is the base case. We are NOT invoking the function under this condition. The equivalent base case from the previous exercise was when we had reached the front of the line.

```
print the first letter
```

This section solves a piece of the problem. If we want to spell someone’s name, we’ll have to spell at least one letter.

```
invoke speller with the given name minus the first letter
```

This section is the recursive step, calling the function with arguments which bring us closer to the base case. In this example, we’re reducing the length of the name by a single letter. Eventually, there will be a function call with no letters given as the argument.

For comparison’s sake, here is pseudo-code for an iterative approach to the same problem:

```
define function, speller
for each letter in the name argument
    print the letter
print "all done"
````

### Call Stacks and Execution Frames

A recursive approach requires the function invoking itself with different arguments. How does the computer keep track of the various arguments and different function invocations if it’s the same function definition?

Repeatedly invoking functions may be familiar when it occurs sequentially, but it can be jarring to see this invocation occur within a function definition.

Languages make this possible with call stacks and execution contexts.

Stacks, a data structure, follow a strict protocol for the order data enters and exits the structure: the last thing to enter is the first thing to leave.

Your programming language often manages the call stack, which exists outside of any specific function. This call stack tracks the ordering of the different function invocations, so the last function to enter the call stack is the first function to exit the call stack

we can think of execution contexts as the specific values we plug into a function call.

```
A function which adds two numbers:

Invoking the function with 3 and 4 as arguments...
execution context:
X = 3
Y = 4

Invoking the function with 6 and 2 as arguments...
execution context:
X = 6
Y = 2
```


Consider a pseudo-code function which sums the integers in an array:

```
function, sum_list 
if list has a single element
    return that single element
otherwise...
    add first element to value of sum_list called with every element minus the first
```

This function will be invoked as many times as there are elements within the list! Let’s step through:


```
CALL STACK EMPTY
___________________

Our first function call...
sum_list([5, 6, 7])

CALL STACK CONTAINS
___________________
sum_list([5, 6, 7])
with the execution context of a list being [5, 6, 7]
___________________

Base case, a list of one element not met.
We invoke sum_list with the list of [6, 7]...

CALL STACK CONTAINS
___________________
sum_list([6, 7])
with the execution context of a list being [6, 7]
___________________
sum_list([5, 6, 7])
with the execution context of a list being [5, 6, 7]
___________________

Base case, a list of one element not met.
We invoke sum_list with the list of [7]...

CALL STACK CONTAINS
___________________
sum_list([7])
with the execution context of a list being [7]
___________________
sum_list([6, 7])
with the execution context of a list being [6, 7]
___________________
sum_list([5, 6, 7])
with the execution context of a list being [5, 6, 7]
___________________

We've reached our base case! List is one element. 
We return that one element.
This return value does two things:

1) "pops" sum_list([7]) from CALL STACK.
2) provides a return value for sum_list([6, 7])

----------------
CALL STACK CONTAINS
___________________
sum_list([6, 7])
with the execution context of a list being [6, 7]
RETURN VALUE = 7
___________________
sum_list([5, 6, 7])
with the execution context of a list being [5, 6, 7]
___________________

sum_list([6, 7]) waits for the return value of sum_list([7]), which it just received. 

sum_list([6, 7]) has resolved and "popped" from the call stack...


----------------
CALL STACK contains
___________________
sum_list([5, 6, 7])
with the execution context of a list being [5, 6, 7]
RETURN VALUE = 6 + 7
___________________

sum_list([5, 6, 7]) waits for the return value of sum_list([6, 7]), which it just received. 
sum_list([5, 6, 7]) has resolved and "popped" from the call stack.


----------------
CALL STACK is empty
___________________
RETURN VALUE = (5 + 6 + 7) = 18
```