---
title: "100 Days of Code Log R1D1"
date: 2021-09-27T19:18:20+05:30
draft: false
katex: false
tags: ["Coding",]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

This is my first day in the 100 Days of Code challenge. Today, I had started with the "Fortran for Scientific Computing" course in [Future Learn](https://www.futurelearn.com/courses/fortran-for-scientific-computing). It had been a great start.

I had learnt about the precision available in fortran for various number data types. For example, the follow program deals with the single and double precision for real numbers.

```fortran
program sqrt_2

    use, intrinsic :: iso_fortran_env, only : sp=>real32, dp=>real64
    implicit none

    print *, sqrt(2.0), sqrt(2.0_sp)
    print *, sqrt(2.0) == sqrt(2.0_sp)
    print *, sqrt(2.0) == sqrt(2.0_dp)
    print *, sqrt(2.0_sp) == sqrt(2.0_dp)

    print *, sqrt(2.0_dp)**2
    print *, sqrt(2.0_sp)**2
    print *, sqrt(2.0_dp)**2 - sqrt(2.0_sp)**2

end program sqrt_2
```

It gives out the following result when compiled(`gfortran -0 sqrt_2 sqrt_2.f90`) and run(`./sqrt_2`).

```
   1.41421354       1.41421354
 T
 F
 F
   2.0000000000000004
   1.99999988
   1.1920928999487046E-007
```

Next, I'll be looking into the strings and related operations in Fortran.
