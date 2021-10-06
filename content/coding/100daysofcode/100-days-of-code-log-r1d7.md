---
title: "100 Days of Code Log R1d7"
date: 2021-10-03T22:36:29+05:30
draft: false
katex: true
tags: ["Coding","Fortran"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

Today, I found this amazing site for Fortran tutorials - https://masuday.github.io/fortran_tutorial/index.html

I went through the tutorials which was organized in a very neat way. Then I proceeded to implement the following simple code.

Make a tridiagonal matrix with 1 on diagonal and 0 or  on off-diagonal with an arbitrary $n$. See the following example for $n=5$.
$$
\displaystyle{\begin{bmatrix} 1 & 0 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 & 1 \end{bmatrix}  }
$$
The following is my implementation.

```fortran
program tridiagonal
    implicit none
    integer, parameter :: n = 5
    integer :: m(n,n), i

    call tridiag(m, -2)
    do i = 1,n
        print '(*(i3))', m(i,:)
    end do
    
contains
subroutine tridiag(m, r)
    implicit none
    integer,intent(inout) :: m(:,:)
    integer,intent(in), optional :: r
    integer :: order(2), i
    m = 0
    order = shape(m)
    do i = 1, order(1)
        m(i,i) = 1
    end do
    if (present(r)) then
        do i = 1, order(1)-1
            m(i,i+1) = r
            m(i+1, i) = r
        end do
    end if
end subroutine tridiag 
end program tridiagonal
```

