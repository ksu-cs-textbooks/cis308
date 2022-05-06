---
title: "Linked Lists"
pre: "4.6. "
weight: 55
date: 2018-08-24T10:53:26-05:00
---

We can use structs to help implement all the common data structures in C. For example,
whereas before we would have created a Node class to help us write a linked list, we will now
create a node struct:

```c
struct node {
    int data;
    struct node *next; //pointer to next node in list
};
```

Suppose we want to create a linked list with a single node. First, we declare a head variable:

```c
struct node *head;
```

Then, we allocate memory for the node:

```c
head = malloc(sizeof(struct node));
```

Finally, we initialize the fields in `head`:

```c
head->data = 4;
head->next = NULL;
```

Here's a full C program that inserts values into a linked list and then prints them out:

```c
#include <stdio.h>

struct node {
    int data;
    struct node *next;
};

struct node *head;

void add(int);
void print(void);

int main() {
    head = NULL;
    add(1);
    add(2);
    add(3);
    add(4);

    //prints 1, 2, 3, 4 on separate lines
    print();
    
    return 0;
}

void add(int num) {
    //create new node
    struct node *newnode = malloc(sizeof(struct node));
    newnode->data = num;
    newnode->next = NULL;

    if (head == NULL) {
        head = newnode;
    }
    else {
        //find end of list
        struct node *cur = head;
        while (cur->next != NULL) {
            cur = cur->next;
        }

        //add newnode after cur
        cur->next = newnode;
    }
}

void print(void) {
    struct node *cur = head;
    while (cur != NULL) {
        printf("%d\n", cur->data);
        cur = cur->next;
    }
}
```

Linked lists in C work almost exactly the same as linked lists in Java or C#. The only differences are:

1) We use a struct instead of a class to represent a node
2) We use -> instead of . to access values in the node
