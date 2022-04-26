---
title: "Multi-dimensional Dynamic Arrays"
pre: "3.8. "
weight: 47
date: 2018-08-24T10:53:26-05:00
---

We can also create multi-dimensional dynamic arrays using *malloc*. This section will focus on
creating two-dimensional arrays. You can get more dimensions by adapting the following
process:

1. Use *malloc* to create an array of pointers. Each pointer in the array will point to a row
in the two-dimensional array. 

For example:
```c
//Final array will have 3 rows
int **matrix = malloc(3*sizeof(int*));
```

2. Use *malloc* to allocate space for each row:

```c
int i;
for (i = 0; i < 3; i++) {
	//Final array will have 4 columns
	matrix [i] = malloc(4*sizeof(int));
}
```

3. Now we can treat the pointer like a traditional two-dimensional array. For example, we
could set every element to 0:

```c
int j;
for (i = 0; i < 3; i++) {
	for (j = 0; j < 4; j++) {
		matrix [i][j] = 0;
	}
}
```

4. When we are done using a multi-dimensional array, we release the memory in reverse order of
how we allocated it. So, first we release each row:

```c
for (i = 0; i < 3; i++) {
	free(matrix [i]);
}
```

And then we release the top-level array of pointers:

```c
free(matrix);
```