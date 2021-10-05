---
title: "100 Days of Code Log R1d9"
date: 2021-10-05T19:25:01+05:30
draft: false
katex: false
tags: ["Coding", "Fortran"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

Continuing with the lessons on fortran, the following stuff were covered today.

## Procedures in detail

### Intents:

A fortran function's parameters may have three possible intents

- `in`
- `out`
- `inout`

```fortran
function one(x) result (y)
	real, intent(inout) :: x(:)
	logical :: y
	x = 1.
	y = .true.
end function one
```

Note that the result variable doesn't (and cannot) have intent.

### Call by reference:

By default, fortran calls by reference. Hence, if a variable is modified in function, it is reflected in the calling program.

### Call by value:

In order to call a parameter by value (that is not to modify orginal variable), the following syntax is followed during declaration inside the procedure.

```fortran
integer, value:: var
```

### Keyword Arguments:

Fortran supports calling procedures with keywords. When done so, the order doesn't matter (need not be the same order as the function/subroutine declaration).

```fortran
call clamp(min_val=0.0, max_val=1.0, val=x)
```

### Optional Arguments:

Add optional arguments to functions and subroutines.

```fortran
call f(x)
call f(x, y)
.
.
subroutine f(x, y)
integer, intent(inout) :: x
integer, intent(in), optional ::y
end subroutine f
```

### Persistent values:

These values are stored and can be retrieved during next function calls.

```fortran
real, save :: per
```

## Pure Procedures:

Compiler generates efficient code when a procedure is declared as pure.

```fortran
pure function f(x)
pure subroutine g(x)
```

To be a pure procedure, the following should be followed.

- All arguments must have intent `in` or `inout` (in case of subroutine).
- no persistent (`save`) variables
- I\O (read, print, write) not allowed.
- stop statement not allowed.
- cannot be recursive.
- if any other procedure is called, that must also be pure.

## Recursion:

In Fortran, recursive functions are usually less efficient than iterative counterparts.

```fortran
recursive function factorial(n) result(fac)
    implicit none
    integer, intent(in) :: n
    integer :: fac

    if (n >= 2) then
        fac = n*factorial(n - 1)
    else
        fac = 1
    end if
end function factorial

```

## Scope:

Scope is usually limited to the main program or module. So, a variable declared in a program will be accessible to the procedures it contains. However, if the same variable name is declared in a function, that variable will have a local scope within that function. 

Modules can be imported (after compiling it first) into another program. It also imports all the corresponding values. Hence, `only` is preferred to limit what we import.

```fortran
use modulename, only : fn1
```

Block statements have the scope limited to within that section.

```fortran
block
    integer :: i = 5
    print *, i
end block
```

# Control Flow Statements

## Select statement:

It's similar to switch case of C and is limited to only integer or character values

```fortran
select case (integer_or_character)
	case (case1)
		...
	case (case2)
		...
	...
	case default
		...
end select
```

## where statement

It's similar to logical indexing in python

```python
A[A<=0] = 0
```

In fortran,

```fortran
where (A <= 0)
	A = 0.
elsewhere (A > 1)
	A =1.
elsewhere
	A = 0.5
end where
```

### merge statement

If there are only two cases, merge can be used.

```fortran
A = merge(A>0, true_value, false_value)
```

## Exit and cycle statements

- `exit` exits the loop it is in
- `cycle` skips the following codes and go to the next iteration.
- `stop` stops the entire program

If the loop is labelled, then exit and cycle can specify which loop it has to consider.

```fortran
outer: do i=1,n
	inner: do, j=1,n
		if (i<j) cycle outer
		if (mod(i,2)== 0) exit inner
	end do inner
end do outer
```

## Forall and do concurrent statements

These statements allow the compiler to optimize the iterations that has to be performed. Hence, the values in each iteration must be independent of previous iteration.

`forall` is restrictive in the sense that it can only be used for assignment of an array.

```fortran
forall (i=1,n, j=1,n, ...., i<=j) ! logical expression is optional
	A(i,j) = i+j
end forall
```

`do concurrent` is more general in that regard.

```fortran
do concurrent (i=1:N, j=i:N)
    A(i, j) = f(i, j)
end do
```

Here is one cool way to develop a band matrix with a width of 3.

```fortran
program band
        integer, dimension(9, 9) :: data = 0
        integer :: i, j
        forall (i = size(data, 1):1:-1, j = -1:1, i+j<=size(data,1) .and. i+j>0)
            data(i, i + j) = 1
        end forall
        do i=1,size(data,1)
                print '(*(i3))', data(i,:)
        end do
end program band
```

That's it, for now!
