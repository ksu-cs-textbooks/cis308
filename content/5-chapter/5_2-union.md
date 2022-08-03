---
title: "Unions"
pre: "5.2. "
weight: 61
date: 2018-08-24T10:53:26-05:00
---

A *union* is a construct in C that can hold one of several types. A
union variable can only hold one value at a time, unlike a struct,
but that value is not restricted to a single type. 

Here's the format for declaring a union:

```text
union modelName {
    type1 name1;
    type2 name2;
    ...
    typeN nameN;
} objectList;
```

Here, `modelName` is the name of the type you're creating, each
`type name` is a type you want to be able to store in this union
plus a name for it, and `objectList` is a list of variables you
want to create with this union type. Both `modelName` and
`objectList` are optional.

## Defining Unions
Suppose I want a type that will allow me to store money as dollars
(in a double field) or as yen (in an int field). Here's how I'd do
that:

```c
union money {
    double dollars;
    int yen;
} price;
```

This creates a variable called `price` that has type `union money`. 

I could also create a variable called `price2` like this:

```c
union money price2;
```

## Union Fields
To access a field in a union, use the . notation – just like with a
struct:

```c
variableName.fieldName
```

(`variableName` is the name of the union variable, and
`fieldName` is the name of the field that we want to access.) If
we had a pointer to a union variable, we would use the -> notation
to access a field.

For example, I can make the `price` variable hold 17 yen:

```c
price.yen = 17;
```

Or I can make the `price` variable hold $4.20:

```c
price.dollars = 4.20;
```

Note that when I change the value of `price` from 17 yen to $4.20,
I lose the information about 17 yen. A union variable can only
hold one value at a time, but that value can have different types.

## Unions and Enums
Suppose we have a variable of type `union money`, and we want
to print out its value (in either dollars or yen, depending on what is
stored). With what we've done so far, there is no way to tell
WHICH type is stored in a union variable – it might be yen and it
might be dollars. If we do:

```c
union money cost;
cost.yen = 17;
printf("Dollars: %lf\n", cost.dollars);
```

which sets the `yen` field but then prints the `dollars` field, the
behavior is undefined. This code is likely to crash or at least have
unpredictable results.

To solve this problem, we need to keep track of which type we're
storing in a union variable. The most common way to do this is
with an enum. For example, we could declare:

```c
enum costK {dollarsK, yenK};
```

Then if we did:

```c
union money cost;
cost.yen = 17;
```

We could also do:

```c
enum costK costEnum;
costEnum = yenK;
```

Then we could tell which type was stored in our union variable by
checking the value of our enum variable:

```c
if (costEnum == yenK) }
    printf("Yen: %d\n", cost.yen);
}
else if (costEnum == dollarsK) {
    printf("Dollars: %lf\n", cost.dollars);
}
```

We will print the value of the field that we're currently using in the
union.

## Structs inside Unions
A struct is a valid type, so we can have a struct be a field in a
union. For example, suppose we wanted to create an animal union
that could be either a dog (struct type) or a cat (struct
type). Furthermore, we want to keep track of the name and breed
of the dog, and the name and color of the cat. 

Here's how:

```c
union animal {
    struct {
        char name[20];
        char breed[20];
    } dog;
    struct {
        char name[20];
        char color[20];
    } cat;
};
```

Notice that we don't name the `dog` struct or the `cat` struct because
we only want a single variable of that type. Instead, we create a
single `dog` variable and a single `cat` variable. Here's how we create
a union variable that holds an orange cat called Tiger:

```c
union animal kitty;
strcpy(kitty.cat.name, "Tiger");
strcpy(kitty.cat.color, "orange");
```

## Unions inside Structs
Similarly, we can put a union inside a struct. For example,
suppose we wanted to keep track of someone's name, what country
they're from, and how much their bill is (in the appropriate
currency). We could store the country with an enum, and the bill
(with different currency) as a union. Here’s how:

```c
struct guest {
    char name[20];
    enum {USA, France, Japan} country;
    union {
        double dollars;
        double euro;
        int yen;
    } cost;
};
```

Now if we want the guest Maria from France, who paid 100 euro,
here's what we'd do:

```c
struct guest maria;
strcpy(maria.name, "Maria");
maria.country = France;
maria.cost.euro = 100.0;
```

## Unions as Inheritance
The union construct allows us to simulate inheritance from other languages. For
example, suppose we defined the following abstract class in C#:

```csharp
public abstract class Person {
    public string name;
    public int age;
}
```

Suppose as well that we have two C# classes, `Student` and
`Employee`, which extend `Person`:

```csharp
public class Student : Person {
    public string major;
    public double gpa;
}

public class Employee extends Person {
    public string division;
    public int yearsWorked;
}
```

The equivalent in C would be a person structure that holds a name,
age, and a union field. The union field could hold either a student
struct (which has a major and gpa) or an employee struct
(which has a division and a yearsWorked). We would also
need an enum field that keeps track of which type in the union is
active. 

Here's what it would look like:

```c
struct person {
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
};
```

Suppose a student has the following information:

- Name: Bob Jones
- Age: 18
- Major: CMPEN
- GPA: 3.2

Here's how we would create a variable to represent that student:

```c
struct person bob;
strcpy(bob.name, "Bob Jones");
bob.age = 18;
strcpy(bob.type.student.major, "CMPEN");
bob.type.student.gpa = 3.2;
bob.typeK = studentK;
```