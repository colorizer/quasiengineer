---
title: "100 Days of Code Log R1D14"
date: 2021-10-10T23:29:47+05:30
draft: false
katex: false
tags: ["Coding", "Fortran"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

## Sieve of Eratosthenes

Here's the fortran implementation of [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes), an ancient method for finding prime upto n numbers (and one of the efficient method for finding small primes).

```fortran
program sieve_of_eratosthenes
    use, intrinsic :: iso_fortran_env, only : error_unit
    implicit none

    call prime_sieve_eratosthenes(170)

    contains
    subroutine prime_sieve_eratosthenes(n)
        integer, intent(in) :: n
        logical :: is_prime(2:n) ! Boolean for knowing whether number is prime or not.
        integer :: p, i

        if(n < 1) then
            write(error_unit, *) 'n must be > 1'
            stop 1
        end if

        is_prime = .true.
        p = 2

        do while (p**2 <= n)
            if (is_prime(p)) then
                forall (i = p**2:n:p)
                    is_prime(i) = .false.
                end forall
            end if
            p = p + 1
        end do

        write (*, '("The primes upto ",i0," are: ")', advance='no') n
        do p = 2,n
            if ( is_prime(p) ) write(*, '(i0, ", ")', advance='no') p
        end do
        write (*,*)
    end subroutine prime_sieve_eratosthenes
end program sieve_of_eratosthenes

```

