---
title: "Enums"
pre: "5.1. "
weight: 60
date: 2018-08-24T10:53:26-05:00
---

`enum` provides a way to create integer constants. For instance, in
Java we might declare:

```java
public static final int GOLD = 1;
public static final int SILVER = 2;
public static final int BRONZE = 3;
```

..but really what we want is to create a "medal" type that can take
on the values GOLD, SILVER, and BRONZE. Moreover, we
want GOLD to mean "1", SILVER to mean "2", and BRONZE to
mean "3".

(Note: Java does have enums available in its latest version, which are
handled very similarly to how they are in C.)

## Defining Enums
Here's the format for defining an enum in C:

```c
enum typeName {
    value1,
    value2,
    ...
    valueN
} objectList;
```

Here, `typeName` is the name of the new data type we’re
creating. `value1, value2, ..., valueN` are the different
values this type can have. Finally, `objectList` is a list of
variables we want to create of type `typeName`. In this definition,
`typeName` and `objectList` are both optional.

Here's how we would represent medals using an enum:
```c
enum medal {gold, silver, bronze};
```

## Enum Variables
Now, the type of this enum is `enum medal`. All variables of
this type can have a value of either `gold`, `silver`, or
`bronze`. Here's how to declare a variable:

```c
enum medal medal100m;
```

And here's how to give this variable the value `gold`:

```c
medal100m = gold;
```c

We can also use the possible values `gold`, `silver`, and
`bronze` in comparisons:

```c
if (medal100m == gold) {
    printf(“You won!\n”);
}
```

## What’s Going On?
When you declare an enum type, what you’re really doing is
making the enum values into integer constants. For example, in
the medal enum, we're really creating the integer constants:

```c
gold = 0;
silver = 1;
bronze = 2;
```

So, for instance, to set medal100m to gold, we could also say:

```c
medal100m = 0;
```

Then the test:

```c
if (medal100m == gold) {...}
```

would still evaluate to true, since `gold` holds the value 0.

## Changing Enum Values
Our medal example isn't quite right. It has `gold` with the value 0,
`silver` with 1, and `bronze` with 2. But we would like `gold` to
have the value 1, `silver` 2, and `bronze` 3. Fortunately, there's
a way to do that:

```c
enum medal {gold = 1, silver, bronze};
```

Setting `gold` to 1 resets the numbering in an enum, so that
`silver` gets set to 2 and `bronze` to 3. We also could have
explicitly set each value:

```c
enum medal {gold = 1, silver = 2, bronze = 3};
```

Here's another example:

```c
enum example {val1, val2 = 9, val3, val4 = 12, val5};
```

Here's how the integer values were assigned:

```c
val1 = 0;
val2 = 9;
val3 = 10;
val4 = 12;
val5 = 13;
```

An enum tries to keep numbering in order, unless we explicitly set
a value. Then, it uses that value to reset the numbering.

## Examples
There is no bool type in C. However, we can create our own
bool type using an enum:

```c
enum bool {false, true};
```

(Notice that false has the value 0 and true has the value
1). Now we can use "bool variables" like we do in C#:

```c
enum bool flag;
flag = true;
if (flag == true) {...}
```

We can also use an enum to represent grade levels in high
school. We'll start freshman out at 9, and continue the numbering
from there:

```c
enum grade {freshman = 9, sophomore, junior, senior};
```

Now we can use this type:

```c
enum grade class;
class = freshman;
class = 10;         //same as sophomore
```

## Enums inside Structs
Since an enum is a valid type, we can put an enum field inside a
struct. For example, suppose we want to create a student struct
that has a name and a grade level. Here’s how:

```c
//define the enum type
enum grade {freshman = 9, sophomore, junior, senior};

//define the struct
struct student {
    char name[20];
    enum grade class;
};
```

This code works, but it's overkill. Instead of defining the enum
separately, we want to be able to define it inside the struct. In fact,
ALL we want is a variable of that enum type – we don't even care
about naming the type. The enum name is optional, so we'll leave
it off. Here's our revised definition:

```c
struct student {
    char name[20];
    enum {freshman = 9, sophomore, junior, senior} class;
};
```

Now, suppose we want to create a student named Mary who is a
junior. Here's how:

```c
struct student mary;
strcpy(mary.name, "Mary");
mary.class = junior;
```