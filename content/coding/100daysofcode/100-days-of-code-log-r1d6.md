---
title: "100 Days of Code Log R1D6"
date: 2021-10-03T00:15:01+05:30
draft: false
katex: false
tags: ["Coding", "Fortran"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

Today had been two part work. Initially, I did some Data Structures lessons from Udacity course. Then, at night, I tried to implement the Single objective optimisation method called fibonacci method using Fortran. There is some mistake that I need to correct. I will share the updated code tmw. Here's the faulty one!

```fortran
program fibonacci_method
    use, intrinsic :: iso_fortran_env, only : error_unit, dp=>real64
    implicit none
    ! a - lower bound
    ! b - upper bound
    ! n - number of evaluations
    integer, parameter :: n = 20
    integer :: k = 2
    integer, dimension(n+1) :: fib
    real(dp) :: x1, x2, f1, f2, L, L_star, a = 0, b = 5
    L = b - a
    fib = fibonacci(n)
    print *,"Fibonacci series", fib
    L_star = fib(n-k+1)*L/fib(n+1)
    ! print *, L_star
    do while (k<=n)
        L = b - a

        x1 = a + L_star
        x2 = b - L_star

        f1 = f(x1)
        f2 = f(x2)

        ! print *, x1, x2, f1, f2

        if (f1 > f2) then
            b = x2
        else
            a = x1
        end if
        ! L_star = x2 - x1
        L_star = fib(n-k+1)*L/fib(n-k+3)
        print *, 'The interval at k: ', k, 'is ', a, b, 'with L*', L_star
        k = k+1
    end do

    contains
    real(dp) function f(x)
        real(dp), intent(in) :: x
        f = x**2 + (54/x)
    end function f

    function fibonacci(n) result(f)
        integer,intent(in) :: n
        integer, dimension(n+1) :: f
        integer :: a=1, b = 1, i
        
        if (n <= 0) then
            write(error_unit, *) 'n must be a positive integer'
            stop 1
        end if
        f(1)=a
        f(2)=b
        do i = 2, n
            a=f(i)
            f(i+1) = f(i) + b
            b = a
        end do
    end function fibonacci
end program fibonacci_method
```

The following output is obtained.

```
Fibonacci series           1           1           2           3           5           8          13          21          34          55          89         144         233         377         610         987        1597        2584        4181        6765       10946
 The interval at k:            2 is    0.0000000000000000        3.0901699250867898      with L*   1.9098300749132102     
 The interval at k:            3 is    1.9098300749132102        3.0901699250867898      with L*   1.1803398501735793     
 The interval at k:            4 is    3.0901699250867898        3.0901699250867898      with L*  0.45084973468720563     
 The interval at k:            5 is    3.0901699250867898        2.6393201903995842      with L*   0.0000000000000000     
 The interval at k:            6 is    3.0901699250867898        2.6393201903995842      with L* -0.17220935388803721     
 The interval at k:            7 is    2.9179605711987526        2.6393201903995842      with L* -0.17220906785924670     
 The interval at k:            8 is    2.9179605711987526        2.8115292582588309      with L* -0.10643148971509220     
 The interval at k:            9 is    2.9179605711987526        2.9179607479739231      with L*  -4.0652809186601392E-002
 The interval at k:           10 is    2.9179605711987526        2.9586135571605245      with L*   6.7523562981351993E-008
 The interval at k:           11 is    2.9179605711987526        2.9586134896369614      with L*   1.5527182138176773E-002
 The interval at k:           12 is    2.9179605711987526        2.9430863074987847      with L*   1.5530328392124683E-002
 The interval at k:           13 is    2.9334908995908773        2.9430863074987847      with L*   9.5934629509213543E-003
 The interval at k:           14 is    2.9430843625417986        2.9430863074987847      with L*   3.6688324353763863E-003
 The interval at k:           15 is    2.9467531949771750        2.9430863074987847      with L*   7.4093599471731461E-007
 The interval at k:           16 is    2.9467539359131698        2.9430863074987847      with L*  -1.4103413378424151E-003
 The interval at k:           17 is    2.9453435945753275        2.9430863074987847      with L*  -1.3753606553943976E-003
 The interval at k:           18 is    2.9453435945753275        2.9444616681541791      with L*  -9.0291483061708531E-004
 The interval at k:           19 is    2.9453435945753275        2.9453645829847961      with L*  -2.9397547371612376E-004
 The interval at k:           20 is    2.9453435945753275        2.9456585584585122      with L*   1.0494204734312618E-005
```

The converging point is wrong. Because, for the function defined in code ($f=x^2 + 54/x$), the optima lies at 3. Hence, will try again tomorrow!
