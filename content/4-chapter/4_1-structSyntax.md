---
title: "Struct Syntax"
pre: "4.1. "
weight: 50
date: 2018-08-24T10:53:26-05:00
---
C is a procedural programming language, which means that a program is just a collection of
functions – no classes. However, C does have a construct called a struct that is similar to a data
class in Java. A struct is simply a new variable type that is a collection of related data.

## Syntax
Here is the format of a struct declaration:

```c
struct name {
    type1 name1;
    type2 name2;
    ...
} objList;
```

Here, `name` is the optional name for this structure type. This name is needed if you plan to
created any variables of this struct type.
The `type name` elements are fields that you want in your struct. For example, if the struct
represented a person, you might want these fields:

```c
char name[20];
int age;
```

Fields in structs are the same idea as fields in a Java or C# class. 

Finally, `objList` is an optional
list of variable names you want constructed with this struct type.

## First Example
Here is a simple struct:

```c
struct person {
    char name[20];
    int age;
} p1, p2;
```

Now, `struct person` is a new datatype. `p1` and `p2` are variables of type `struct
person`.

## Declaring Struct Variables
You can automatically declare struct variables by listing variable names at the end of the struct
definition. You can also declare them outside the definition just like you do ordinary variables.
The format for declaring variables in C is:

```
type name;
```

The type of the above struct, for example, is `struct person`. So we can declare another
struct variable as follows:

```c
struct person p3;
```

This declaration automatically allocates space for the struct, including space for every field in the
struct.

## Accessing Struct Fields
Accessing a field in a struct variable is exactly like accessing a field in a Java or C#
object:

```c
structVar.fieldName
```

Here, `structVar` is the name of the struct variable and `fieldName` is one of the fields in the
struct. This allows us to access or change that field.
Let's declare another struct person variable, and set the person's name to "Bob" and age to 20.

Here's how:

```c
struct person bobPerson;        //declare struct variable
bobPerson.age = 20;             //set person's age to 20
strcpy(bobPerson.name, "Bob");  //set person's name to "Bob"
```

Notice that if we are initializing a string field, we must use `strcpy`. The following will NOT
compile since name is an array (a constant pointer):

```c
bobPerson.name = "Bob";         //Will not compile!
```