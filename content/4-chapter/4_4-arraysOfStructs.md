---
title: "Arrays of Structs"
pre: "4.4. "
weight: 53
date: 2018-08-24T10:53:26-05:00
---

You can create arrays of structs in C just like you can create arrays of any other type. The
format for creating constant-sized arrays is:

```c
type name[size];
```

Consider the person struct again:

```c
struct person {
    char name[20];
    int age;
};
```

Here's how to create a 3-slot array of type `struct person` called `group`:

```c
//"struct person" is the type; "group" is the array name
struct person group[3];
```

When you create an array of type struct, C allocates space for each struct element (and its fields)
in the array.

We can get out a particular struct element using an array index:

```c
group[0]        //the first struct person in the array
```

For example, here's how we could set the first person's name to "Bob" and age to 20:

```c
strcpy(group[0].name, "Bob");
group[0].age = 20;
```