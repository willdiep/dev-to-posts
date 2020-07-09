---
title: What Are Doubly Linked Lists
published: false
---

In my previous blog post, I went over Memory, Arrays, & Linked Lists. This was a gentle introduction to Singly Linked Lists and how it applied to memory stored on the computer.

For this week, I'd like to build on top of it by giving a tutorial of Doubly Linked Lists.

![Alt Text](https://personalzone-hulgokm2zfcmm9u.netdna-ssl.com/wp-content/uploads/2017/07/doubly-linked-list-illustration.jpg)
<sub>[Image credits to thecodingdelight](https://www.thecodingdelight.com/doubly-linked-list/)</sub>

While a singly linked list consists of nodes with links from the one node to the next, a doubly linked list also has a link to the node before it. These `previous` links, along with the added `tail` property, allow you to iterate backward through the list as easily as you could iterate forward through the singly linked list. We will go over how to add and remove nodes: 

![Alt Text](https://personalzone-hulgokm2zfcmm9u.netdna-ssl.com/wp-content/uploads/2017/07/doubly-linked-list-node-pointer-diagram.jpg)
<sub>[Image credits to thecodingdelight](https://www.thecodingdelight.com/doubly-linked-list/)</sub>

## Adding to the List

![Alt Text](https://personalzone-hulgokm2zfcmm9u.netdna-ssl.com/wp-content/uploads/2017/07/inserting-data-to-front-of-doubly-linked-list.jpg)
<sub>[Image credits to thecodingdelight](https://www.thecodingdelight.com/doubly-linked-list/)</sub>

In a doubly linked list, adding to the list is a little complicated as we have to keep track of and set the node’s previous pointer as well as update the tail of the list if necessary.


### Adding to the Head
![Alt Text](https://personalzone-hulgokm2zfcmm9u.netdna-ssl.com/wp-content/uploads/2017/07/inserting-data-to-front-of-doubly-linked-list.jpg)
<sub>[Image credits to thecodingdelight](https://www.thecodingdelight.com/doubly-linked-list/)</sub>

When adding to the head of the doubly linked list, we first need to check if there is a current head to the list. If there isn’t, then the list is empty, and we can simply make our new node both the head and tail of the list and set both pointers to `null`. If the list is not empty, then we will:

* Set the current head’s previous pointer to our new head
* Set the new head’s next pointer to the current head
* Set the new head’s previous pointer to `null`

### Adding to the Tail
![Alt Text](https://personalzone-hulgokm2zfcmm9u.netdna-ssl.com/wp-content/uploads/2017/07/inserting-data-to-back-of-doubly-linked-list.jpg)
<sub>[Image credits to thecodingdelight](https://www.thecodingdelight.com/doubly-linked-list/)</sub>

Similarly, there are two cases when adding a node to the tail of a doubly linked list. If the list is empty, then we make the new node the head and tail of the list and set the pointers to `null`. If the list is not empty, then we:

* Set the current tail’s next pointer to the new tail
* Set the new tail’s previous pointer to the current tail
* Set the new tail’s next pointer to `null`




## Removing from the Head and Tail

Due to the extra pointer and tail property, removing the head from a doubly linked list is slightly more complicated than removing the head from a singly linked list. However, the previous pointer and tail property make it much simpler to remove the tail of the list, as we don’t have to traverse the entire list to be able to do it.

### Removing the Head
![Alt Text](https://personalzone-hulgokm2zfcmm9u.netdna-ssl.com/wp-content/uploads/2017/07/removing-head-node-doubly-linked-list-1.jpg)
<sub>[Image credits to thecodingdelight](https://www.thecodingdelight.com/doubly-linked-list/)</sub>

Removing the head involves updating the pointer at the beginning of the list. We will set the previous pointer of the new head (the element directly after the current head) to `null`, and update the head property of the list. If the head was also the tail, the tail removal process will occur as well.


### Removing the Tail
![Alt Text](https://personalzone-hulgokm2zfcmm9u.netdna-ssl.com/wp-content/uploads/2017/07/removing-tail-node-doubly-linked-list.jpg)
<sub>[Image credits to thecodingdelight](https://www.thecodingdelight.com/doubly-linked-list/)</sub>

Similarly, removing the tail involves updating the pointer at the end of the list. We will set the next pointer of the new tail (the element directly before the tail) to `null`, and update the tail property of the list. If the tail was also the head, the head removal process will occur as well.


## Removing from the Middle of the List

![Alt Text](https://personalzone-hulgokm2zfcmm9u.netdna-ssl.com/wp-content/uploads/2017/07/remove-from-middle-doubly-linked-list.jpg)
<sub>[Image credits to thecodingdelight](https://www.thecodingdelight.com/doubly-linked-list/)</sub>

It is also possible to remove a node from the middle of the list. Since that node is neither the head nor the tail of the list, there are two pointers that must be updated:

* We must set the removed node’s preceding node’s next pointer to its following node
* We must set the removed node’s following node’s previous pointer to its preceding node

There is no need to change the pointers of the removed node, as updating the pointers of its neighboring nodes will remove it from the list. If no nodes in the list are pointing to it, the node is orphaned.
