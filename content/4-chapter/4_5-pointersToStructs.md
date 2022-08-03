---
title: "Pointers to Structs"
pre: "4.5. "
weight: 54
date: 2018-08-24T10:53:26-05:00
---

You can declare a pointer to a struct just like you declare a pointer to another element type. The
format for declaring a pointer is:

```text
type* name;
```

So, to declare a pointer to a `struct person` element, we could say:

```c
struct person* personPtr;
```

Suppose we have another `struct person` variable:

```c
struct person p1;
strcpy(p1.name, "Jill");
p1.age = 18;
```

Then we can make `personPtr` point to `p1`:

```c
personPtr = &p1;
```

## Allocating Memory
We can also create struct variables by:

1) Declaring a pointer to a struct
2) Allocating memory for the struct

This approach (using pointers instead of standard variables) is handy when building data
structures like linked lists.

To create a struct person in this way, we first declare a pointer:

```c
struct person* personPtr;
```

Then we allocate memory for the struct, and give `personPtr` the address of that memory. We
can use `sizeof(struct person)` to get the number of bytes needed to store a variable of
type `struct person`:

```c
personPtr = malloc(sizeof(struct person));
```

Now, `personPtr` points to a `struct person`, which has space for the `name` and `age` fields.

## Accessing Fields
We can get at the struct person object itself by dereferencing `personPtr`:

```c
*personPtr
```

We can then initialize the fields:

```c
(*personPtr).age = 18;
```

This line does two things:
1) Dereferences the pointer to get at the `struct person` object
2) Changes the person’s age to 18

Do NOT write something like this:

```c
*personPtr.age = 18;    //BAD!
```

The compiler will try to resolve the "." operator first. Because `personPtr` is a pointer and not
a struct, using a . doesn’t make sense. This line will result in a compiler error. We need to
dereference the pointer before we can access any fields.

Pointers to structs are very common in C, and you’ll often find yourself dereferencing a struct
pointer and then accessing one of the fields. Because of this, there is a shortcut notation:

```c
personPtr->age = 18;

//Is equivalent to:
(*personPtr).age = 18;
```

