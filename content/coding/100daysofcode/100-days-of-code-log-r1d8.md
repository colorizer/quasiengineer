---
title: "100 Days of Code Log R1D8"
date: 2021-10-04T22:43:48+05:30
draft: false
katex: false
tags: ["Coding","Fortran"]
categories: ["⌨️ Coding", "➿ 100DaysofCode"]
summary: ""
typora-root-url: ../../../static
---

Today has been the beginning of Week 2 in [Fortran for scientific Computing course](https://www.futurelearn.com/courses/fortran-for-scientific-computing). This had the introduction to arrays, mainly, along with elemental procedures. A word or two were mentioned about "pure functions" but those remain a mystery for now. But, here are some highlights. 

### Arrays

1. Arrays in fortran may have particular rank (upto 15 in case of Fortran 2008).

```fortran
real, dimension(5) :: x
real :: A(3,4)
real, dimension(-10:10) :: y
```

2. Arrays are arranged columnwise in Fortran.
3. Array can be indexed in slices in a similar manner to python
4. Array functions may be 
   1. Elemental - operate on each value in array. Example `sin(A)` operates on each element.
   2. Operate on array as a whole - `sum(A)` adds all the elements in the A.
5. The 2nd category of array functions usually have the following optional parameters.
   1. `dim` - The dimension along which to perform the operations. For example, for `A(m,n)`, the operation `sum(A, dim=1)` will return a vector of length `n` with each element being the sum of `m` rows in that column.
   2. `mask` - The condition to consider. Should be passed a logical array of same size of the array in consideration.

```fortran
real :: A(3,4), b(3)
A = reshape( [ (i, i=1,12) ], [3,4])
b = sum(A, dim=2, mask=mod(A,2)/=0)
```

There is count function which counts the number of instances which are true in logical array.

```fortran
count(mask=mod(A,2)/=0)
count(A<0)
```

### Procedures

In a subroutine, if an array dimension `n` is specified, that dimension is the minimum requirement. But, if the passed array is larger, the first `n` values alone are considered.

```fortran
real :: a(5), b(8)
a = 5.
b = 0.
call print_arr(a) ! error
call print_arr(b) ! no error

subroutine print_arr(data)
    implicit none
    real,intent(in) :: data(6)
    print *, data
end subroutine print_arr
```

Also, the fortran allows one to index outside the array but it still doesn't throw error.  I still haven't figured out why the `(1,3)` element comes out to be 8. May be it will be covered tomorrow!

```fortran
integer :: A(2,3)
call fill_array(A)

subroutine fill_array(A)
    implicit none
    integer,dimension(:,:) :: A
    integer :: i,j
    do j = 1, size(A, 1)
        do i = 1, size(A,2)
            A(i,j) = (i-1)*size(A,2) + j
            print *, A(i,j)
        end do
    end do
end subroutine fill_array
```

Also, elemental functions can have either have `intent(in)` or `value` not `intent(out)` nor `intent(inout)`.
