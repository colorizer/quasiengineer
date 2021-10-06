---
title: "100 Days of Code Log R1D10"
date: 2021-10-06T23:47:49+05:30
draft: false
katex: false
tags: ["Coding", "Fortran"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

Today's learning can be split mainly into the following two sections.

### I/O Formatting

The formatting string in fortran is passed as a string to print or write statements.

```fortran
character(len=10) :: fmt_str
fmt_str = '(*(i3))'
print fmt_str, 900
write (*, fmt_str) 900
```

The following formats are available

- `i<w>.<d>` - Integers
- `f<w>.<d>` - floating point
- `e<w>.<d>e<d2>`, `en`, `es`- edit descriptor (engineering and scientific notation)
- `a<d>` - string
- `l<d>` - logical
- `g<d>` - general

All these can be preceeded by a number to denote how many of that type is present. I believe more info regarding the same can be found here - https://masuday.github.io/fortran_tutorial/format.html

### Implicit Save:

In fortran, declaring a variable in the following way

```fortran
integer :: f = 10
```

is equivalent to doing the following

```fortran
integer, save :: f = 10
```

Hence, the last value of the f variable is remembered for the next function call. This will lead to unexpected bugs. Hence, the following procedure process is necessary while declaring and assigning any variable.

```fortran
integer :: f
f = 10
```



