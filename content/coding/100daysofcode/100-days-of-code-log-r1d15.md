---
title: "100 Days of Code Log R1D15"
date: 2021-10-12T01:49:43+05:30
draft: false
katex: false
tags: ["Coding","Fortran", "Generative"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

## Randomly Generated plot in Fortran

I owe this to one of the participants of matlab contest - [Matlab Mini Hack](https://in.mathworks.com/matlabcentral/communitycontests/contests/4/entries) - where this simple but powerful method was shared. Here is my implementation

```fortran
module charchal
    use, intrinsic :: iso_fortran_env, only : wp=>real64
    implicit none
    private
    real, parameter :: pi = 4.*atan(1.)
    public :: plot_charchal

contains
subroutine plot_charchal
    integer(wp), parameter :: m = 2e5
    real(wp) :: a(2,2), b(2), c(2,2), d(2), e(2,2), f(2), x(2), n, data(2, m)
    integer(wp) :: i, clr(m), fn
    call randinit(a)
    call randinit(c)
    call randinit(e)

    b = [0.0, 2*rand()]
    d = [0.0, rand()]
    f = [0.0, rand()]
    x = 0
    clr = 0

    do i = 1, m
        call random_number(n)
        if (n <= 0.85) then
            x = matmul(a, x) + b
            clr(i) = randint(3)
        else if (n <= 0.94) then
            x = matmul(c, x) + d
            clr(i) = randint(3) + 1
        else if (n <= 1) then
            x = matmul(e, x) + f
            clr(i) = 2 +randint(4)
        end if
        data(:, i) = x
!         clr(i) = randint(3)
    end do

    open(newunit=fn, file='charchal.dat')
    do i= 1, m
        write(fn, *) data(:,i), clr(i)
    end do
    close(fn)

    call execute_command_line('gnuplot -p charchal.plt')
end subroutine plot_charchal

subroutine randinit(a)
    real(wp), intent(inout) :: a(2,2)
    call random_number(a)
    a = 2*a - 1
end subroutine randinit

function randint(seed) result(val)
    integer, intent(in) :: seed
    integer :: val
    val = floor(seed*(1+rand()))
end function randint

end module charchal

program main

    use charchal, only : plot_charchal
    implicit none
    call plot_charchal()

end program main
```

And the following goes into the `charchal.plt` file.

```python
set terminal qt
unset key
unset tics
set size square
set object 1 rectangle from screen 0,0 to screen 1,1 fillcolor rgb"black" behind
set title "Randomly!" textcolor rgbcolor "white"
set style data dots
set palette rgbformulae 33, 13, 10
#3,11,6

m = "charchal.dat"
unset colorbox
plot m with dots palette
```

Here are some of the highlights.

![Random 1](/images/2021/100-days-of-code-log-r1d15/random1.png)

![Random 2](/images/2021/100-days-of-code-log-r1d15/random2.png)

![Random 3](/images/2021/100-days-of-code-log-r1d15/random3.png)

![Random 4](/images/2021/100-days-of-code-log-r1d15/random4.png)

![Random 5](/images/2021/100-days-of-code-log-r1d15/random5.png)

![Random 6](/images/2021/100-days-of-code-log-r1d15/random6.png)

:)
