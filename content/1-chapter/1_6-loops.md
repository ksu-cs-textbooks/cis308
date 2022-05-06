---
title: "Loops"
weight: 25
pre: "1.6. "
---

There are three kinds of loops in C – while, do-while, and for. Their syntax is exactly the same as loops in Java and C#.

## While Loop
The code in a while loop executes repeatedly until a specified condition becomes false. If the condition is false before the first execution of the loop, then the entire loop will be skipped. 

This example will read and print every character typed by the user (up until they press enter):

```c
char c = ' ';
printf("Type some text: ");
while (c != EOF) 
{
	c = getchar();
	printf("%c\n", c);
}
```

## Do-While Loop
Like a while loop, the code in a do-while loop executes repeatedly until a specified condition becomes false. However, the condition in a do-while loop is not checked until after the first iteration of a loop. So, a do-while loop always executes at least once. 

Here's the same example using a do-while loop:

```c
char c;s
printf("Type some text: ");
do 
{
	c = getchar();
	printf("%c\n", c);
} while (c != EOF);
```

Notice that we don't have to give `c*`a dummy initial value, as we did in the while loop.

## For-Loop
The syntax of a for-loop is just like it is in other languages:

```c
for (initialization; condition; update) 
{
	//code
}
```

The only caveat is that the loop variable must not be declared in the initialization section (like `int i = 0`). This is because variables in C should only be declared at the beginning of a block (an opening { ). If you forget, your code may compile for you, but it won't necessarily compiler elsewhere.

Here's an example that computes the factorial of a number entered by the user:

```c
int i, num;
int factorial = 1;
printf("Enter a positive integer: ");
scanf("%d", &num);
for (i = 1; i <= num; i++) 
{
	factorial *= num;
}
printf("%d! = %d\n", num, factorial);
```

## Break
The `break` statement immediately stops execution of a loop. For example, this code allows us to get and print 10 numbers, unless the user types a 0:

```c
int i, num;
for (i = 0; i < 10; i++) 
{
	printf("Enter a number: ");
	scanf("%d", &num);
	if (num == 0) break;
	printf("You entered %d\n", num);
}
```

## Continue
The `continue` statement skips the remaining code inside the loop, and continues with the next iteration. For example, this code allows us to add together 10 numbers inputted by the user, except any numbers that are negative:

```c
int i, num;
int sum = 0;
for (i = 0; i < 10; i++) 
{
	printf("Enter a number: ");
	scanf("%d", &num);
	if (num < 0) continue; //Won't add num to sum
	sum+=num;
}
printf("The sum of the positive numbers is %d\n", sum);
```