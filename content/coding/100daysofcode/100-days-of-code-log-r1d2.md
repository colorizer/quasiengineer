---
title: "100 Days of Code Log R1D2"
date: 2021-09-28T21:42:56+05:30
draft: false
katex: false
tags: ["Coding", "Fortran", "Scientific Computing"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

Today I had continued with [Fortran for Scientific Computing](https://www.futurelearn.com/courses/fortran-for-scientific-computing/) and learned about

- Character datatype
- Logical datatype and operators
- Conditional Statements

### Character Datatypes

The character dataypes are declared as either a single character or as an array of particular length.

```fortran
character :: c
character(len=5) :: str
```

Two main points about strings are that,

- if the length of string input is less than specified, the remaining is filled by space.
- If it greater than the specified length, only the specified length is read and rest is discarded.

Also, I learnt about functions such `achar`, `iachar`, `trim`, `len_trim` and so on.

### Logical statements

The logical statements are verbose and hence it is very easy to read how they work. In the following code, read `.eqv.` as "equivalent" and `.neqv.` as not equivalent. The rest will be easy to understand.

```fortran
logical function is_it_leap_year(year)
	
	integer :: year
	is_it_leap_year = (mod(year, 400)==0) .or. (mod(year, 4)==0) .and. .not. (mod(year, 100)==0)

end function is_it_leap_year
```

### Conditional Statements

The fortran code has two ways of having if statements

#### Multiline

```fortran
if (x< 3) then
	x = x+3
end if
```

#### Inline (logical if)

```fortran
if (x<3) x = x+3
```

### Iterations

The iterations are carried through either 

```fortran
! do loops

do i = 1, 11, 2 ! 1 - start; 11 - end; 2 - step size
	print *, i, i**2
end do
```

or the

```fortran
! while loops
integer :: i = 0
do while (i < 10)
	print *, i, i**2
	i = i + 2
end do
```

I also attempted the quizzes which gave insights to the various little things by which fotran may differ from, say, python.
