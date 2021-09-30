---
title: "100 Days of Code Log R1d3"
date: 2021-09-29T22:47:15+05:30
draft: false
katex: false
tags: ["Coding",]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

Today I had learnt about the procedures and intrinsic procedures in Fortran. Basically, a procedure can be of two types

- function
- subroutine

## Functions

The functions are procedures which return a value which can either be

1. Given the same name as function name in which case the syntax will be.

```fortran
integer function function_name(inputname)
	implicit none
	integer, intent(in) :: inputname
	.
	.
	function_name = 1234..
end function function_name
```

In this case, the return type is given before function keyword. Also, note that **in fortran, values are passed by reference** by default. Hence, if the input is only an input, `intent(in)` needs to be mentioned. Other intents are `out, inout`.

2. Give a separate variable name for return value

```fortran
function function_name(inputname) result(resultname)
	implicit none
	integer, intent(in) :: inputname
	integer, intent(out) :: resultname
	.
	.
	resultname = 1234..
end function function_name
```

Hence, the `result` keyword is used to specify the return value. There is no `return` keyword in Fortran. Also, fortran can take optional arguments. Inside the function body, these need to be declared with `optional` keyword.

```fortran
integer, optional, intent(in) :: somenumber
```



## Subroutines

Subroutines do not have a return value. They are preferably used when the input values are to be modified though the same can be done in functions. The subroutines are called through

```fortran
call subroutine_name(input)
```

declaring a subroutine is straight forward.

```fortran
subroutine one_adder(input)
	implicit none
	integer :: input
	input = input + 1
end subroutine one_adder
```

## Intrinsic Procedures

There are quite a few intrinsic procedures that are available in Fortran. Many of them are scientific, but few string manipulation procedures are also available. 

[The list  of intrinsic procedures in gcc](https://gcc.gnu.org/onlinedocs/gfortran/Intrinsic-Procedures.html#Intrinsic-Procedures)

I tried to implement the fibonacci optimization method but the current knowledge is not sufficient. Will try again once I learn more about Fortran.
