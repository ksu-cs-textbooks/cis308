---
title: "typedef"
pre: "5.3. "
weight: 62
date: 2018-08-24T10:53:26-05:00
---
It gets a bit cumbersome to use types called `struct person`
and `enum grade`. It would be much nicer to be able to call
them just `person` or `grade`. With C's typedef construct, we
can do just that. 

The format of typedef is:

```c
typedef oldType newType;
```

Here, we rename `type oldType` to the new name `newType`. We
can now create variables using the name `newType`. For example:

```c
typedef char letterGrade;
letterGrade g;
g = 'A';
```

Notice that we treat our new `letterGrade` type just like it was a
char. The only difference is that when we declare the variable, we
can use `letterGrade` as the type instead of char.

## Typedef with Structs, Unions, and Enums
We can do a similar thing to rename structs, unions, and
enums. For example, consider the following struct:

```c
struct person {
    char name[20];
    int age;
};
```

The formal type of the struct is `struct person`. Now, we
want to rename the type to be just `person`:

```c
//typedef oldType newType
typedef struct person person;  
```

Alternatively, we can declare the struct and rename it with typedef
all on the same line:

```c
//typedef oldType newType
typedef struct person {
    char name[20];
    int age;
} person;
```

However, we don't need to name the struct now, since we're
always going to be using the new type name when creating
variables of this type:

```c
typedef struct {
    char name[20];
    int age;
} person;
```

Now we can declare and use a `person` variable:

```c
person p;
strcpy(p.name, "Bill");
p.age = 22;
```

We can do a similar thing to rename unions and enums. Consider
the following union:

```c
union money {
    double dollars;
    int yen;
};
```

We can rename the union type to `money`:

```c
typedef union {
    double dollars;
    int yen;
} money;
```

Now we can use `money` as the type name instead of `union
money`. Similarly, consider the following enum:

```c
enum grade{freshman = 9, sophomore, junior, senior};
```

We can rename the enum type to `grade`:

```c
typedef enum {freshman = 9, sophomore, junior, senior} grade;
```

Now we can use `grade` as the type name instead of `enum
grade`.

## Typedef with Linked Lists
Consider the following structure for a node in a linked list:

```c
struct node {
    int data;
    struct node *next;
};
```

We can try to rename the `struct node` type to `node` using
typedef:

```c
typedef struct {
    int data;
    node *next;
} node;
```

However, this will give us a compiler error. The reason is that this
struct is self-referential. When we declare the field `node
*next` in the struct, the compiler hasn't yet seen that we're
renaming the type to `node`. If instead we list the field as:

```c
struct node *next;
```

we will also get a complaint, as we left off the name of the struct.
If you're using typedef on a self-referential struct, you need to
include BOTH the name of the struct and the name of the renamed
type. The fixed node struct looks like:

```c
typedef struct node {
    int data;
    struct node *next;
} node;
```

Here's how we'd use it:

```c
node *head = malloc(sizeof(node));
head->data = 4;
head->next = malloc(sizeof(node));
head->next->data = 7;
head->next->next = NULL;
```

This creates the linked list 4->7.