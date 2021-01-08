---
title: "Vectorised RK4 for solving Coupled ODEs"
date: 2021-01-08T01:26:42+05:30
draft: false
tags: ["Engineering"]
categories: ["🗃️ Tech", "🛠 Dev"]
typora-root-url: ../../../static
---

Runge-Kutta methods are one of the most widely used methods for numerically solving differential equations. In this post, I will explain how to implement the vectorised code for solving coupled ODEs using fourth order RK methods in GNU-Octave. The same code can be easily translated to matlab with minimal changes. 

**Note**: This is ***not*** a 100% vectorised implementation. RK methods are, of course, iterative algorithms. The aim is to eliminate unnecessary loops through vectorisation. If this code can be improved further, please let me know in the comments section below.

Consider a set of coupled, first order, Ordinary Differential Equations of the general form,
$$
\displaystyle{\frac{dx}{dt}=f_1\left( t,x, y,z \right) } 
$$

$$
\displaystyle{\frac{dy}{dt}=f_2\left( t,x, y,z \right) } 
$$

$$
\displaystyle{\frac{dz}{dt}=f_3\left( t,x, y,z \right) }
$$



whose initial conditions $t_0, x_0, y_0, z_0$ are known. Then, for a step size $\displaystyle{h= t_{n+1}-t_n}$, the RK4 method is given by
$$
\displaystyle{x_{n+1} = x_n + \frac{1}{6}h\left( k_{1_x}+2k_{2_x}+2k_{3_x}+k_{4_x} \right) }
$$

$$
\displaystyle{y_{n+1} = y_n + \frac{1}{6}h\left( k_{1_y}+2k_{2_y}+2k_{3_y}+k_{4_y} \right) }
$$

$$
\displaystyle{z_{n+1} = z_n + \frac{1}{6}h\left( k_{1_z}+2k_{2_z}+2k_{3_z}+k_{4_z} \right) }
$$



where,

$\displaystyle{n = 0,1,2,3,\ldots}$

$\displaystyle{k_{1_x} = f_1\left( t_n, x_n, y_n, z_n \right) }$

$\displaystyle{k_{2_x} = f_1 \left( t_n+\frac{h}{2}, x_n +h\frac{k_{1_x}}{2} \right) }$

$\displaystyle{k_{3_x} = f_1\left( t_n+\frac{h}{2}, x_n +h\frac{k_{2_x}}{2} \right) }$

$\displaystyle{k_{4_x} = f_1\left( t_n+h, x_n +hk_{3_x} \right) }$

and similarly for $y, z$ as well.

This can be represented graphically by

!["Source: Wikimedia"](/images/2021/vectorised-code-for-rk4-in-octave/800px-Runge-Kutta_slopes.svg.png "Source: Wikimedia")

**Aim**: T

```octave
function [values, k] = multi_rk4(fns, in_val, t, h)
  %easiness shortforms
  weights = [1/6, 2/6, 2/6, 1/6];
  k_wt = [0 0.5 0.5 1];
  s = @squeeze;
  %eo easiness
  
  %initialize
  t = t(1):h:t(2);
  values = zeros(length(t), 3);
  values(1,:) = in_val;
  k = zeros(length(t),4, 3);
  %eo initialize
  
  for i = 1:length(t)-1
    
    for j = 1:4
      if j == 1
        inputs = [t(i) values(i, :)];
      else
        inputs = [t(i)+0.5*h (values(i,:) + k_wt(j)*s(k(i,j-1,:))')];
      endif
      k(i,j,:) = h*fns(inputs);
    endfor
    
    values(i+1, :) = values(i,:) + weights*s(k(i,:,:));
    
  endfor
  
endfunction
```

