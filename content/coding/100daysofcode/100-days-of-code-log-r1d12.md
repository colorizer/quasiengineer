---
title: "100 Days of Code Log R1D12"
date: 2021-10-09T00:15:34+05:30
draft: false
katex: false
tags: ["Coding", "Fortran"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

It's been a great experience today, solving the tower of hanoi. Though a simple solution, the implementation was hard especially since I made some mistake in variable which took more than an hour (and resorting to gdb) to debug. So, the victory feels sweet. Here's the code. Will try to make it more efficient and make a blog post out of it tomorrow.

```fortran
program towerofhanoi
    use, intrinsic :: iso_fortran_env, only : i8=>int64
    implicit none
    integer, dimension(:), allocatable :: a, b, c
    integer, parameter :: p = 3
    integer(i8) :: n, itr, i, j, k
    itr = 0
    i=1
    print *, "Enter the number of disks"
    read *, n
    j=n+1
    k=n+1
    allocate(a(n+1)); allocate(b(j)); allocate(c(k))
    call fill_array(a)
    print *, a
    a(n+1) = 0; b=0; c=0
    do 
        itr = itr + 1_i8
        if (mod(itr, 100) == 0) print *, itr
        ! A <--> B
        if (mod(n,2) == 0) then
            call move(a, b, i, j)
            call move(a, c, i, k)
            call move(b, c, j, k)
        else
            call move(a, c, i, k)
            call move(a, b, i, j)
            call move(b, c, j, k)
        end if
        if ((c(1)==1) .or. (itr>=5*2_i8**n)) exit
    end do
    print *, "Iterations: ", itr
    print *, 'a:', a
    print *, 'b:', b
    print *, 'c:', c
    print *, 'values :', i, j, k

    contains
    subroutine fill_array(x)
        implicit none
        integer, intent(inout) :: x(:)
        integer :: nn, i
        nn = size(x)
        do concurrent(i=1:nn)
            x(i) = i
        end do
    end subroutine fill_array

    subroutine move(x, y, l,m)
        implicit none
        integer, intent(inout) :: x(:), y(:)
        integer(i8), intent(inout) :: l,m
        if (m>=n+1) then
            call movelr(x, y, l,m)
        else if (l>=n+1) then
            call moverl(x, y, l,m)
        else if (x(l) < y(m)) then
            call movelr(x, y, l,m)
        elseif (x(l) > y(m)) then
            call moverl(x, y, l,m)
        end if
    end subroutine
    subroutine movelr(x, y, l,m)
        implicit none
        integer, intent(inout) :: x(:), y(:)
        integer(i8), intent(inout) :: l,m
        m = m-1
        y(m) = x(l)
        x(l) = 0
        l = l+1
    end subroutine
    subroutine moverl(x, y, l,m)
        implicit none
        integer, intent(inout) :: x(:), y(:)
        integer(i8), intent(inout) :: l,m
        l = l-1
        x(l) = y(m)
        y(m) = 0
        m = m+1
    end subroutine
end program towerofhanoi
```

