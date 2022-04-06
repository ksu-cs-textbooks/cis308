---
title: "Selection Structures"
weight: 24
pre: "1.5. "
---

C has if-statements and switch statements that work just like those in Jav and C#. 

Here is a sample if-statement:

```c
int age;
//initialize age
//print either Child, Teenager, or Adult, depending on age
if (num < 11) 
{
	printf("Child\n");
}
else if (num < 18) 
{
	printf("Teenager\n");
}
else printf("Adult\n");
```

Here is a sample switch statement. The expression in the switch clause must evaluate to either a character or an integer:

```c
char grade;
printf("Enter your grade: ");
grade = getchar();
getchar(); //read and discard newline character

switch (grade) 
{
	case 'A':
		printf("Excellent\n");
		break;
	case 'B':
		printf("Good\n");
		break;
	case 'C':
		printf("Average\n");
		break;
	case 'D':
		printf("Poor\n");
		break;
	case 'F':
		printf("Failing\n");
		break;
	default:
		printf("Invalid grade\n");
}
```