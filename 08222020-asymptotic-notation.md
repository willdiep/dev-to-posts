---
title:  Asymptotic Notation (Part 1)
published: true
---

When writing programs, it’s important to make smart programming choices so that code runs most efficiently. Computers seem to take no time evaluating programs, but when scaling programs to deal with massive amounts of data, writing efficient code becomes the difference between success and failure. In computer science, we define how efficient a program is by its runtime.

We can’t just time the program, however, because different computers run at different speeds. My dusty old PC does not run as fast as your brand new laptop. Programming is also done in many different languages, how do we account for that in the runtime? We need a general way to define a program’s runtime across these variable factors. We do this with Asymptotic Notation.

With asymptotic notation, we calculate a program’s runtime by looking at how many instructions the computer has to perform based on the size of the program’s input. For example, if I were calculating the maximum element in a collection, I would need to examine each element in the collection. That examining step is the same regardless of the language used, or the CPU that’s performing the calculation. In asymptotic notation, we define the size of the input as N. I may be looking through a collection of 10 elements, or 100 elements, but we only need to know how many steps are performed relative to the input so N is used in place of a specific number. If there is a second input, we may define the size of that input as M.

There are varieties of asymptotic notation that focus on different concerns. Some will communicate the best case scenario for a program. For example, if we were searching for a value within a collection, the best case would be if we found that element in the first place we looked. Another type will focus on the worst case scenario, such as if we searched for a value, looked in the entire dataset and did not find it. Typically programmers will focus on the worst case scenario so there is an upper bound of runtime to communicate. It’s a way of saying “things may get this bad, or slow, but they won’t get worse!”

In this next module, we will learn more about asymptotic notation, how to properly analyze the runtime of a program through asymptotic notation, and how to take into consideration the runtime of different data structures and algorithms when creating programs. Learning these skills will change the way you think when you design programs and it will prepare you for the software engineering world where creating efficient programs is an essential skill.

## What is Asymptotic Notation?

Cheetahs. Ferraris. Life. All are fast, but how do you know which one is the fastest? You can measure a cheetah’s and a Ferrari’s speed with a speedometer. You can measure life with years and months.

But what about computer programs? In fact, you can time a computer program, but different computers run at different speeds. For example, a program that takes 12 nanoseconds on one computer could take 45 milliseconds on another. Therefore, we need a more general way to gauge a program’s runtime. We do this with Asymptotic Notation.

Instead of timing a program, through asymptotic notation, we can calculate a program’s runtime by looking at how many instructions the computer has to perform based on the size of the program’s input: N.

For instance, a program that has input of size N may tell the computer to run 5N2+3N+2 instructions. (We will get into how we get this kind of expression in future exercises.) Nevertheless, this is a still a fairly messy and large expression. For asymptotic notation, we drop all of our constants (the numbers) because as N becomes extremely large, the constants will make minute differences. After changing our constants, we have N2+N. If we take each of these terms in the expression and graph them, we see that the N2 term grows faster than the N term. 

![queue](https://secureservercdn.net/160.153.137.40/662.aa9.myftpupload.com/wp-content/uploads/2019/11/Time-Complexity.png)

<sub>[Image credits to Algorithms And Me](https://algorithmsandme.com/common-time-complexities-of-functions/)</sub>

For example, when N is 1000:

- the N2 term is 1,000,000
- the N term is 1,000

As you can see, the N2 term is much more significant than the N term. When N is larger than 1000, the difference becomes even more significant. Because the difference is so enormous, we don’t even need to consider the N term when calculating the runtime. Thus, for this program, we would describe the runtime in terms of N2. There are three different ways we could describe the runtime of this program: big Theta or Θ(N2), big O or O(N2), big Omega or Ω(N2). 

## Big Theta (Θ)  

The first subtype of asymptotic notation we will explore is big Theta (denoted by Θ). We use big Theta when a program has only one case in term of runtime. But what exactly does that mean? Take a look at the pseudocode for a function that prints the values in a list below:

```
Function with input that is a list of size N:
   For each value in list:
    Print the value
```

The number of instructions the computer has to perform is based on how many iterations the loop will do because if the loop does more iterations, then the computer will perform instructions. Now, let’s see how many iterations the loop will do dependent on the value of N.

As we can see in every case, with a list of size N, the program has a runtime of N because the program has to print a value N times. Thus, we would say the runtime is Θ(N).

Let’s look at a more complicated example. In the following pseudocode program, the function takes in an integer, N, and counts the number of times it takes for N to be divided by 2 until N reaches 1.

```
Function that has integer input N:
  Set a count variable to 0
  Loop while N is not equal to 1:
      Increment count
      N = N/2
  Return count
```

But what happens when there are multiple runtime cases for a single program? Stay tune for part 2 next week!