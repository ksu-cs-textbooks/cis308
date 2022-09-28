---
title: "User-Defined Types with Pointers"
pre: "6.4. "
weight: 73
date: 2018-08-24T10:53:26-05:00
---
Consider the following struct:

```c
typedef struct {
    char name[20];
    int age;
    union {
        struct {
            char major[20];
            double gpa;
        } student;
        struct {
            char division[20];
            int yearsWorked;
        } employee;
    } type;
    enum {employeeK, studentK} typeK;
} person;
```

Suppose we want to create a pointer to a struct variable with the
following information:
- Name: Bob Jones
- Student
- Age: 18
- Major: EECE
- GPA: 3.2

First, we'd declare a pointer of type `person`:

```c
person *p;
```

Then we'd allocate memory:

```c
p = malloc(sizeof(person));
```

And then we would initialize the fields:

```c
strcpy(p->name, "Bob Jones");
p->age = 18;
strcpy(p->type.student.major, "EECE");
p->type.student.gpa = 3.2;
p->typeK = studentK;
```

Notice that we use a -> to access any fields in the struct (since our
variable is a pointer). After we are inside an internal field like a
union, we switch to . notation (since the union is not a pointer).