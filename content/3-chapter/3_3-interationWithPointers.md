---
title: "Iteration with Pointers"
pre: "3.3. "
weight: 42
date: 2018-08-24T10:53:26-05:00
---

This is how we have initialized array elements in the past:

```c
int i;
int nums[10];
for (i = 0; i < 10; i++) {
	nums[i] = 0;
}
```

However, now that we can treat arrays like pointers, there is a different way to initialize array
elements:

```c
int *ip;
int nums[10];
for (ip = nums; ip < nums+10; ip++) {
	*ip = 0;
}
```

Here, `ip` is a pointer that starts by pointing to the first element in the array. We loop while the
value of `ip` (the memory address) is less than `nums+10` – which is the address of the last
element in the array. Each time, `ip++` advances `ip` to point at the next element in the array.
Inside the loop, we dereference `ip` to get the current array element, and set that element to 0.