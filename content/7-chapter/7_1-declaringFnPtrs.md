---
title: "Declaring Function Pointers"
pre: "7.1. "
weight: 80
date: 2018-08-24T10:53:26-05:00
---

To	declare	a	variable	which	can	hold	a	pointer	to	a	function	it	ends	up	being	a	somewhat	
complex	declaration.	A	simple	function	pointer	declaration	looks	like	this:

```c
int (*pfi)();
```

This	declares `pfi` as	a	pointer	to	a	function	which	will	return	an int.	As	in	other	declarations,	
the * indicates	that	a	pointer	is	involved,	and	the	parentheses () indicate	that	a	function	is	
involved.	But	what	about	the	extra	parentheses	around `(*pfi)`?	They're	needed	because	there	
are	precedence	relationships	in	declarations	just	as	there	are	in	expressions,	and	when	the	
default	precedence	doesn't	give	you	what	you	want,	you	have	to	override	it	with	explicit	
parentheses.	In	declarations,	the () indicating	functions	and	the [] indicating	arrays	*bind*	more	
tightly	than	the *'s	indicating	pointers.	Without	the	extra	parentheses,	the	declaration	above	
would	look	like

```c
//WRONG for pointer-to-function
int *pfi(); 
```

and	this	would	declare	a	function	returning	a	pointer	to int.	With	the	explicit	parentheses,	
however, `int (*pfi)()` first tells	us	that `pfi` is	a	pointer,	and	that	what	it's	a	pointer	to	
is	a	function,	and	what	that	function	returns	is	an int.

It's	common	to	use	`typedef` with	complicated	types	such	as	function	pointers.	For	example,	
after	defining:

```c
typedef int (*funcptr)();
```

the	identifier `funcptr` is	now	a	synonym	for	the	type	*pointer	to	function	returning	int*.	This	
typedef would	make	declaring	pointers	such	as `pfi` considerably	easier:

```c
funcptr pfi;
```