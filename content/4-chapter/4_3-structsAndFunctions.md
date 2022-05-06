---
title: "Structs and Functions"
pre: "4.3. "
weight: 52
date: 2018-08-24T10:53:26-05:00
---

We could have also written the [point example]({{<ref "4-chapter/4_2-structExample.md" >}})
by passing the point structs to the `getSlope` and
`getIntercept` functions (instead of passing their fields). This works just like passing other
variable types, except `struct point` will be an argument type.
Here's the example when we pass the points to the functions:

```c
#include <stdio.h>

struct point {
    int x;
    int y;
}; //No variables declared here

double getSlope(struct point, struct point);
double getIntercept(struct point, double);

int main() {
    struct point p1;
    struct point p2;
    double slope;
    double intercept;

    printf("Enter point1, e.g. (1, 2): ");
    scanf("(%d, %d)", &(p1.x), &(p1.y));
    printf("Enter point2, e.g. (1, 2): ");
    scanf("(%d, %d)", &(p2.x), &(p2.y));

    slope = getSlope(p1, p2);
    intercept = getIntercept(p1, slope);

    //prints equation in form y = mx + b
    //m: slope, b: y-intercept
    printf("y = %.2lfx + %.2lf\n", slope, intercept);

    return 0;
}

double getSlope(struct point p1, struct point p2) {
    //slope = change in y / change in x
    return (p2.y-p1.y)/(p2.x-p1.x);
}

double getIntercept(struct point p, double slope) {
    //if y = mx + b, b = y - mx
    return p.y - slope*p.x;
}
```