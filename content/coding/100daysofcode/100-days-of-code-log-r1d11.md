---
title: "100 Days of Code Log R1d11"
date: 2021-10-07T22:53:41+05:30
draft: false
katex: false
tags: ["Coding", "Fortran"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

Today's venture was rather short. I reimplemented the logistic map with elemental function. Here's the code.

```fortran
program logisticmap
    use, intrinsic :: iso_fortran_env, only : dp=>real64, error_unit
    implicit integer(i-k)
    integer, parameter :: l=2001, b = 2001
    real(dp) :: r(l), x0(b), x(l, b)
    integer :: fileno, istat, n
    character(len=1024) :: msg
    print *, "No of iterations: "
    read *, n
    x0 = linspace(0._dp, 1._dp, b)
    r = linspace(3.5_dp, 4._dp, l)

    forall (i=1:l)
        x(i,:) = lm(x0, r(i), n)
    end forall
    print *, "Calculations done"

    open(newunit=fileno, file='logisticmap.dat', iostat=istat, iomsg=msg)
    if (istat /= 0) then
        write(error_unit, '(*(A))') trim(msg)
        stop 1
    end if
    do i=1,l
        write(fileno, *) r(i), x(i, :)
    end do
    close(fileno)
    call execute_command_line('gnuplot -p logisticmap.plt')

    contains
    elemental function lm(x0, r, n) result(xn)
        integer, intent(in) :: n
        real(dp), intent(in) :: x0, r
        real(dp) :: xn
        integer :: i

        xn = x0
        do i = 1, n
            xn = r*xn*(1-xn)
        end do
    end function lm

    function linspace(x0, xn, n) result(x)
        integer, intent(in) :: n
        real(dp), intent(in) :: x0, xn
        real(dp) :: x(n), step
        step = (xn-x0)/(n-1)
        do concurrent(i=1:n)
            x(i) = x0 + step*(i-1)
        end do
    end function linspace
end program logisticmap
```

And here's the plot generated.

![logisticmap](/images/2021/100-days-of-code-log-r1d11/logisticmap.png)

Tomorrow, I'll try to address the Tower of Hanoi problem. 
