---
title: "Pointers to Pointers in Linked Lists"
pre: "4.7. "
weight: 56
date: 2018-08-24T10:53:26-05:00
---

Let's look at how pointers to pointers can be used to eliminate a nuisance we've had when trying to
insert and delete items in linked lists. For simplicity, we'll consider lists of integers, built using this
structure:

```c
struct node {
    int data;
    struct node *next;
 };
 ```
 
Suppose we're trying to write some code to delete a given integer from a list. The straightforward
solution looks like this:

```c
//delete node containing i from list pointed to by lp
struct node *lp, *prevlp;
for(lp = list; lp != NULL; lp = lp->next) {
    if(lp->item == i) {
        if(lp == list)
            list = lp->next;
        else {
            prevlp->next = lp->next;
        }
        break;
    }
    prevlp = lp;
}
```

This code works, but it has two flaws. One is that it must use an extra variable to keep track of the
node behind the one it's looking at, and the other is that it must use an extra test to special-case the
situation in which the node being deleted is at the head of the list. Both problems arise because the
deletion of a node from the list involves modifying the previous pointer to point to the next node (that
is, the node before the deleted node to point to the one following). But, depending on whether the node
being deleted is the first node in the list or not, the pointer that needs modifying is either the pointer
that points to the head of the list, or the next pointer in the previous node.

To illustrate this, suppose that we have the list (1, 2, 3) and we're trying to delete the element 1. After
we've found the element 1, `lp` points to its node, which just happens to be the same node that the
main list pointer points to, as illustrated in (a) below:

![linkedlistA](/images/linkedListA.png)

To remove element 1 from the list, then, we must adjust the main list pointer so that it points to 2's
node, the new head of the list (as shown in (b) below):

![linkedlistB](/images/linkedListB.png)

If we were trying to delete node 2, on the other hand (as illustrated in (c) below):

![linkedlistC](/images/linkedListC.png)

we'd have to adjust node 1's next pointer to point to 3. 

The `prevlp` pointer keeps track of the previous node we were looking at, since (at other than the first node in the
list) that's the node whose next pointer will need adjusting. (Notice that if we were to delete node 3, we
would copy its next pointer over to 2, but since 3's next pointer is the null pointer, copying it to node 2
would make node 2 the end of the list, as desired.)

There is another way to write the list-deletion code, which is (in some ways, at least)
much cleaner, by using a pointer to a pointer to a `struct node`.

Hint: This pointer will point at the pointer which points at the node we're looking at; it will either
point at the head pointer or at the next pointer of the node we looked at last time. Since this pointer
points at the pointer that points at the node we're looking at, it points at the pointer which
we need to modify if the node we're looking at is the node we're deleting.