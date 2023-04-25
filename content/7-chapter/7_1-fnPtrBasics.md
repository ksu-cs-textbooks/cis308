---
title: "Function Pointer Basics"
pre: "7.1. "
weight: 80
date: 2018-08-24T10:53:26-05:00
---

## Declaration Syntax

Here is the syntax for declaring a function pointer:

```text
return_type (*ptr_name) (args);
```

This declares `ptr_name` as a pointer to a function that returns something of type `return_type` and that takes the argument types described in `args`. Here, `args` is a comma-separated lists of the argument types for a function. For example, `args` would be `(int, double)` for a function that took two arguments -- an int followed by a double.

The extra parentheses around `(*ptr_name)` are needed because there are precedence relationships in declarations just as there are in expressions. If instead we did:

```text
//THIS IS INCORRECT FOR DECLARING A FUNCTION POINTER!
return_type *ptr_name (args);
```

We would be declaring a function (NOT a function pointer) whose return type was `return_type*`.

## Declaration Example

Suppose we wish to declare a pointer to a function that returns an int and takes two parameters -- an int followed by a char*. We would write:

```c
int (*fn_ptr) (int, char*);
```

Now `fn_ptr` is a variable of type function pointer to a function that returns an int and takes `(int, char*)` as arguments.

## Initialization Syntax

To initialize our `fn_ptr` variable, we need an existing function whose header matches its declaration -- one that returns an int and takes `(int, char*)` as arguments. Suppose we have the following function:

```c
int addToLength(int num, char* str) {
    return num + strlen(str);
}
```

Suppose we also have our `fn_ptr` variable declared in a main method. Now we can initialize `fn_ptr` to point to the beginning of the executable code in the `addToLength` function.

```c
int main() {
    char* test = "hello";       //declares string constant "hello"

    int (*fn_ptr)(int, char*);  //declares our function pointer, fn_ptr

    fn_ptr = addToLength;       //now fn_ptr points to the addToLength function

    return 0;
}
```

Note that when we do:

```c
fn_ptr = addToLength;
```

That we mean: assign to `fn_ptr` the memory address of the beginning of the executable code in the `addToLength` function. We could have more pedantically written:

```c
fn_ptr = &addToLength;
```

To explicitly get the memory address of the `addToLength` function, and assign that to `fn_ptr`. However, the `&` is optional in this case since there is no other way to interpret assigning to a function pointer variable.

## Using Function Pointers

After you have declared and initialized a function pointer variable, you can use it to call the referenced function (passing the necessary arguments). In our example, we could modify our main method to look like:

```c
int main() {
    int result;                 //declare result variable

    char* test = "hello";       //declares string constant "hello"

    int (*fn_ptr)(int, char*);  //declares our function pointer, fn_ptr

    fn_ptr = addToLength;       //now fn_ptr points to the addToLength function

    int ans = fn_ptr(3, test);  //call the function referenced by fn_ptr,
                                //passing 3 and test. Store the returned value
                                //in the ans variable

    printf("%d\n", ans);     //in our example, prints 8
                                //(the length of "hello" plus 3)

    return 0;
}
```

Note that we use `fn_ptr` as follows:

```c
int ans = fn_ptr(3, test);
```

This calls the function referenced by `fn_ptr` (the `addToLength` function), passing the arguments 3 and `test`. The value returned by the referenced (`addToLength`) function is stored in the `ans` variable.

The `fn_ptr` variable holds the memory address of the beginning of the executable code for the `addToLength` function. When we do `int ans = fn_ptr(3, test)`, we want to go to the memory location stored in `fn_ptr`, and begin executing that code. In other words, we wish to dereference `fn_ptr`, which we can do with the `*` operator. We could more precisely write:

```c
int ans = (*fn_ptr)(3, test);
```

To first go to the executable code referenced by `fn_ptr`, and then to start executing that code with arguments `3` and `test`. As with using the `&` operator when initializing function pointers, using the dereferencing operator when using a function pointer is optional. There is no other possible meaning of `fn_ptr(3, test)`, so the function pointer is dereferenced whether we explicitly use the operator or not.

If we do choose to explicitly dereference, we need to be careful with order of operations. If we instead did:

```c
//THIS IS INCORRECT FOR USING A FUNCTION POINTER!
int ans = *fn_ptr(3, test);
```

Then we would first go to the executable code referenced by `fn_ptr` (the `addToLength` function), passing our arguments `3` and `test`. That code would return `8`, which is the sum of and the argument `3` and the string length of `hello`. Finally, we would assign to `ans` the result of dereferencing the `8`. This will lead to either a segmentation fault (the program crashing) or to grabbing an arbirtrary value in memory and claiming it as our answer.