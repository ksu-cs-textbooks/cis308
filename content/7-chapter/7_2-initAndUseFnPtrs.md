---
title: "Initializing and Using Function Pointers"
pre: "7.2. "
weight: 81
date: 2018-08-24T10:53:26-05:00
---

Recall our function pointer type (a pointer to a function that returns an int) from the previous section:

```c
typedef int (*funcptr)();
```

And our declared variable of our new type:

```c
funcptr pfi;
```

## Initializing Function Pointers
Once	declared,	a	function	pointer	can	of	course	be	set	to	point	to	some	function.	If	we	declare	
some	functions:

```c
int f1();
int f2();
int f3();
```

then	we	can	set	our	pointer `pfi` to	point	to	one	of	them:

```c
pfi = &f1;
```

or	to	one	or	another	of	them	depending	on	some	condition:

```c
if(condition) {
    pfi = &f2;
}
else {
    pfi = &f3;
}
```

(Of	course,	we're	not	restricted	to	these	two	forms;	we	can	assign	function	pointers	under	any	
circumstances	we	wish.	The	second	example	could	be	rendered	more	compactly	using	the	
conditional	operator: `pfi = condition ? &f2 : &f3` .)

In	these	examples,	we've	used	the & operator	as	we	always	have,	to	return	the	address	of	the	
variable.	However,	when	getting	the	address	of	a functions,	the & is	optional,	because	when	
you	mention	the	name	of	a	function	but	are	not	calling	it,	there's	nothing	else	you	could	
possibly	be	trying	to	do	except	generate	a	pointer	to	it.	So,	most	programmers	write

```c
pfi = f1;
```

or

```c
if(condition) {
    pfi = f2;
}
else {
    pfi = f3;
}
```

(or,	equivalently,	using	the	conditional	operator, `pfi = condition ? f2 : f3` ).

## Using Function Pointers
Finally,	once	we	have	a	function	pointer	variable	which	does	point	to	a	function,	we	can	call	the	
function	that	it	points	to.	Broken	down	to	a	near-microscopic	level,	this,	too,	is	a	three-step	
procedure.	First,	we	write	the	name	of	the	function	pointer	variable:

```c
pfi
```

This	is	a	pointer	to	a	function.	Then,	we	put	the * operator	in	front,	to mean	*take	the	contents	of	the	
pointer**:

```c
*pfi
```

Now	we	have	a	function.	Finally,	we	append	an	argument	list	in	parentheses,	along	with	an	
extra	set	of	parentheses	to	get	the	precedence	right,	and	we	have	a	function	call:

```c
(*pfi)(arg1, arg2)
```

The	extra	parentheses	are	needed	here	for	almost	the	same reason	as	they	were	in	the	
declaration	of `pfi`.	Without	them,	we'd	have

```c
//WRONG, for pointer-to-function
*pfi(arg1, arg2)
```

and	this	would	say,	*call	the	function `pfi` (which	had	better	return	a	pointer),	passing	it	the	
arguments `arg1` and `arg2`,	and	take	the	contents	of	the	pointer	it	returns.*	However,	what	
we	want	to	do	is	take	the	contents	of `pfi` (which	is	a	pointer	to	a	function)	and	call	the	
pointed-to	function,	passing	it	the	arguments `arg1` and `arg2`.	Again,	the	explicit	parentheses	
override	the	default	precedence,	arranging	that	we	apply	the * operator	to `pfi` and then do	
the	function	call.

Just	to	confuse	things,	though,	parts	of	the	syntax	are	optional	here	as	well.	There's	nothing	you	
can	do	with	a	function	pointer	except	assign	it	to	another	function	pointer,	compare	it	to	
another	function	pointer,	or	call	the	function	that	it	points	to.	If	you	write:

```c
pfi(arg1, arg2)
```

it's	obvious,	based	on	the	parenthesized	argument	list,	that	you're	trying	to	call	a	function,	so	
the	compiler	goes	ahead	and	calls	the	pointed	to	function,	just	as	if	you'd	written:

```c
(*pfi)(arg1, arg2)
```

When	calling	the	function	pointed	to	by	a	function	pointer,	the * operator	(and	hence	the	extra	
set	of	parentheses)	is	optional.	I	prefer	to	use	the	explicit *,	because	that's	the	way	I	learned	it	
and	it	makes	a	bit	more	sense	to	me	that	way,	but	you'll	also	see	code	which	leaves	it	out.
