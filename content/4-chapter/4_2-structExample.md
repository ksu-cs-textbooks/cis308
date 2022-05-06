---
title: "Struct Example"
pre: "4.2. "
weight: 51
date: 2018-08-24T10:53:26-05:00
---

Structs can be declared at any point in a C program, but they are usually declared with the global
variables (right after the include statements). This way, the struct type can be used throughout
the file.

Here is an example that uses a struct to store a two-dimensional point (x, y location). It gets two
points as input, and then prints the equation that passes through the points.

```c
#include <stdio.h>
struct point {
    int x;
    int y;
}; //No variables declared here

double getSlope(int, int, int, int);
double getIntercept(int, int, double);

int main() {
    struct point p1;
    struct point p2;
    double slope;
    double intercept;

    printf("Enter point1, e.g. (1, 2): ");
    scanf("(%d, %d)", &(p1.x), &(p1.y));
    printf("Enter point2, e.g. (1, 2): ");
    scanf("(%d, %d)", &(p2.x), &(p2.y));

    slope = getSlope(p1.x, p1.y, p2.x, p2.y);
    intercept = getIntercept(p1.x, p1.y, slope);

    //prints equation in form y = mx + b
    //m: slope, b: y-intercept
    printf("y = %.2lfx + %.2lf\n", slope, intercept);

    return 0;
}

double getSlope(int x1, int x2, int y1, int y2) {
    //slope = change in y / change in x
    return (y2-y1)/(x2-x1);
}

double getIntercept(int x, int y, double slope) {
    //if y = mx + b, b = y - mx
    return y - slope*x;
}
```