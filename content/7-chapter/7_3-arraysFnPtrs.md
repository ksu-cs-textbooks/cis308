---
title: "Arrays of Function Pointers"
pre: "7.3. "
weight: 82
date: 2018-08-24T10:53:26-05:00
---

We can declare arrays of function pointers using the same syntax we use to create arrays of any other type. As we saw in the previous section, it is often easier to first rename our function pointer using `typedef`, and then to use that new type when declaring an array.

Consider our operations functions and newly created `function` type from the previous section:

```c
//'function' is the name of a new function pointer type
//describing a function that returns an int and takes two int arguments
typedef int (*function) (int, int);

int plus(int a, int b) {
    return a + b;
}

int minus(int a, int b) {
    return a - b;
}

int times(int a, int b) {
    return a * b;
}

int divide(int a, int b) {
    return a / b;
}
```

Since each operation function is the same type, we can create an array of these four function pointers. We can then ask the user to enter an array index corresponding to the desired operation, and access the appropriate function pointer to execute the operation:

```c
int main() {
    int num1 = 3;
    int num2 = 4;

    int choice;

    //declares an array of four function pointers
    function allOps[4] = {plus, minus, times, divide};

    printf("Enter 0 for plus, 1 for minus, 2 for times, and 3 for divide: ");
    scanf("%d", &choice);

    printf("Result: %d\n", (allOps[choice])(num1, num2));

    return 0;
}
```

Here, `allOps[choice]` accesses a particular function pointer by array index, and then calls that function (passing `num1` and `num2`). For example, if the user entered `2`, then `allOps[choice]` would access the `times` function. The code would print:

```text
Result: 12
```

Since `times(num1, num2)` would return 12.