---
title: "Variables"
weight: 21
pre: "1.2. "
---

## Declaring Variables

Variables in C are declared exactly like variables in Java or C#. Just say:

```c
type name;
```

where `type` is the type of the variable, and `name` is its name. The most common types in C are:

```c
int
double
float
char
```

Notice that C does not have a boolean type or a string type. Some examples:

```c
int num;
char c;
double val;
```

## Initializing Variables

To initialize:

```c
name = value;
```

Where `name` is the name of the variable, and `value` is the value you want to store in it. You can also do:

```c
type name = value;
```

to declare and initialize all on one line. Some examples:

```c
int num;
char c = ‘A’;
double val;
num = 2;
val = 4.7;
```

Variables in C are not assigned an initial value. **However, they will hold whatever garbage value was left in the memory spot reserved for the variable.** This is usually a really big or really negative integer. In Java or C#, if you try to use a variable that has not been initialized, you will get a compiler error. The C compiler will NOT complain – it will just use the garbage value left in the memory spot. 

For example:

```c
int num; //holds some garbage value, say 13145687
num = num+1; //compiler error in Java – num not initialized
//in C, num now has the value 13145688
```

You will find that C is far more lenient in compilation than Java or C#. Remember that just because your program compiles doesn’t mean that it’s right!

## Where to Declare

There are probably a hundred different versions of C compilers. Consequently, a program may compile with one compiler (say, on cislinux) but not compile on another (such as when using Visual Studio .NET). Certain compilers require that variables only be initialized at the beginning of a block
(a block begins when a brace { is opened). Because some compilers have this
requirement, please try to uphold this custom in your programs. For example, the following is fine:

```c
int main() 
{
	double a;
	char b = 'T'; //all declarations are together
				  //at the beginning of the block
	a = 7.2;
}
```

But this is not:

```c
int main() 
{
	double a;
	a = 7.2; 		//code begins – this is not a declaration
	char b = 'T'; 	//b is declared AFTER the code begins
}
```

## Operations

Mathematical operations in C work exactly like mathematical operations in Java or C#. You can use +, -, *, /, and %. You can also use things like ++ and +=.

Casting in C is also the same as casting in Java or C#:

```c
int num = 7;
double d = (double) num; //casts num to a double, d is now 7.0
```

## Simulating Booleans
As was mentioned, there is no boolean type in C. Instead, ints are used to
simulate booleans. In this simulation, 0 means false, and anything else means
true. For example:

```c
int flag = 0; //flag is false
flag = 6; //flag is true
```
