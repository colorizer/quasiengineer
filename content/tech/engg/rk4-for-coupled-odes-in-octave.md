---
title: "RK4 for solving Coupled ODEs in GNU Octave"
date: 2021-01-08T01:26:42+05:30
draft: false
tags: ["Engineering", "RK4", "GNU Octave", "Matlab", "Numerical Computations" ]
categories: ["🗃️ Tech", "🛠 Engg"]
typora-root-url: ../../../static
---

Runge-Kutta methods are one of the most widely used methods for numerically solving differential equations. In this post, I will explain how to implement the vectorised code for solving coupled ODEs using fourth order RK methods in GNU-Octave. The same code can be easily translated to matlab with minimal changes. 

You can directly jump to the code by [clicking here](#code).

The explanation for the code is provided below. **Note** that this is ***not*** a 100% vectorised implementation. RK methods are, of course, iterative algorithms. The aim is to eliminate unnecessary loops through vectorisation. If this code can be improved further, please let me know in the comments section below.

##### RK4 Method

Consider a set of coupled, first order, Ordinary Differential Equations of the general form,
$$
\displaystyle{\frac{dx}{dt}=f_x\left( t,x, y,z \right) }
$$

$$
\displaystyle{\frac{dy}{dt}=f_y\left( t,x, y,z \right) }
$$

$$
\displaystyle{\frac{dz}{dt}=f_z\left( t,x, y,z \right) }
$$

whose initial conditions $t_0,x_0,y_0,z_0$ are known. Then, for a step size $\displaystyle{h= t_{n+1}-t_n}$, the RK4 method is given by
$$
\displaystyle{x_{n+1} = x_n + \frac{1}{6}\left( {k_1}_x+2{k_2}_x+2{k_3}_x+{k_4}_x \right) }
$$

$$
\displaystyle{y_{n+1} = y_n + \frac{1}{6}\left( {k_1}_y+2{k_2}_y+2{k_3}_y+{k_4}_y \right) }
$$

$$
\displaystyle{z_{n+1} = z_n + \frac{1}{6}\left( {k_1}_z+2{k_2}_z+2{k_3}_z+{k_4}_z \right) }
$$

where,

$\displaystyle{n = 0,1,2,3,\ldots}$

$\displaystyle{{k_1}_x=hf_x\left( t_n, x_n, y_n, z_n \right) }$

$\displaystyle{{k_2}_x=hf_x\left( t_n + \frac{h}{2}, x_n+\frac{{k_1}_x}{2} \right) }$

$\displaystyle{{k_3}_x=hf_x\left( t_n+\frac{h}{2}, x_n +\frac{{k_2}_x}{2} \right) }$

$\displaystyle{{k_4}_x=hf_x\left( t_n+h, x_n +{k_3}_x \right) }$

and similarly for $y, z$ as well. [^1]

##### Idea

The key idea is to generate a $K$ matrix of the form,

$$
\displaystyle{K= \begin{bmatrix}{k_1}_x & {k_1}_y & {k_1}_z \\\\{k_2}_x & {k_2}_y & {k_2}_z \\\\{k_3}_x & {k_3}_y & {k_3}_z \\\\{k_4}_x & {k_4}_y & {k_4}_z \\\\ \end{bmatrix} }
$$

Then, we will be able to simplify the process to,

$$
\displaystyle{\begin{bmatrix} x_{n+1} & y_{n+1} & z_{n+1} \end{bmatrix} = \begin{bmatrix} x_n & y_n & z_n \end{bmatrix}+\begin{bmatrix} w_1 & w_2 & w_3 & w_4 \end{bmatrix}\begin{bmatrix}{k_1}_x & {k_1}_y & {k_1}_z \\\\{k_2}_x & {k_2}_y & {k_2}_z \\\\{k_3}_x & {k_3}_y & {k_3}_z \\\\{k_4}_x & {k_4}_y & {k_4}_z \\\\\end{bmatrix} }
$$


where $\displaystyle{\begin{bmatrix} w_1 & w_2 & w_3 & w_4   \end{bmatrix}= \begin{bmatrix} \frac{1}{6} & \frac{2}{6} & \frac{2}{6} & \frac{1}{6}   \end{bmatrix}}$. 

##### Single Iteration

In this code, we will implement the idea to generate $\begin{bmatrix} {k}_x & {k}_y & {k}_z \end{bmatrix}$ simultaneously. This will eliminate need for multiple for loops.  Consider a single iteration of RK4. We will create a function $\displaystyle{f = \begin{bmatrix} f_x & f_y & f_z \end{bmatrix} }$.  Then, 
$$
k = h.f(v)
$$

1. For $k_1$, this takes in a vector $\displaystyle{v=\begin{bmatrix} t_n & x_n & y_n & z_n \end{bmatrix} }$  and generates an output. This output, when multiplied with $h$, will provide $\displaystyle{k_1= \begin{bmatrix} {k_1}_x & {k_1}_y & {k_1}_z \end{bmatrix} }$.
2. For $k_2$, this takes in the vector $\displaystyle{\begin{bmatrix} t_n+\frac{h}{2} & x_n+\frac{{k_1}_x}{2} & y_n+\frac{{k_1}_y}{2} & z_n+\frac{{k_1}_z}{2} \end{bmatrix} }$.  Output of this iteration multiplied with $h$ to generate $\displaystyle{k_2= \begin{bmatrix} {k_2}_x & {k_2}_y & {k_2}_z \end{bmatrix} }$. 
3. Similarly, to generate $k_3$, we will use $\displaystyle{\begin{bmatrix} t_n+\frac{h}{2} & x_n+\frac{{k_2}_x}{2} & y_n+\frac{{k_2}_y}{2} & z_n+\frac{{k_2}_z}{2} \end{bmatrix} }$
4. For $k_4$, we will use $\displaystyle{\begin{bmatrix} t_n+h & x_n+{k_3}_x & y_n+{k_3}_y & z_n+{k_3}_z \end{bmatrix} }$

Also note that, to implement each step we need the output of previous step. Hence, we cannot vectorise this process. Now, consider the step #2 from above. It can be rewritten as,
$$
\displaystyle{v_2 =\begin{bmatrix} t_n & x_n & y_n & z_n \end{bmatrix} + c \begin{bmatrix} h & {k_1}_x & {k_1}_y & {k_1}_z \end{bmatrix}}
$$
where, $c = \frac{1}{2}$. 

This can be generalised as,
$$
\displaystyle{v_j = v + c_j \begin{bmatrix} h & {k_{j-1}}_x & {k_{j-1}}_y & {k_{j-1}}_z \end{bmatrix}}
$$
where $\displaystyle{j \in \left \\{ 2, 3, 4 \right \\} }$. This has been implemented in the code as

```octave
for j = 1:4
    if j == 1
    inputs = [t(i) values(i, :)];
    else
    inputs = [t(i)+c(j)*h (values(i,:) + c(j)*K(j-1,:,i) )];
    endif
    K(j,:,i) = h*fns(inputs);
endfor
```

Finally, I have stacked the $K$ matrix for the $n-1$ iterations of RK4. This results in the following code.

##### Code

```octave
function [values, K] = multi_rk4(@fns, in_val, t, h) 
% The inputs are
% fns(tn, xn, yn, zn ...) is a function which outputs [fx_n fy_n fz_n ...]
% in_val = [x0 y0 z0 ... ]   % Initial values.
% No of values 'm = length(in_val)'
% t = [t0 tn] %tn being the last value of t
% h is the time step h = t_n+1 - t_n

% The outputs are
% values = [n x m] matrix
% EXAMPLE
% values =  [x0 y0 z0;
%  			 x1 y1 z1;
%			 .
%			 .
%			 xn yn zn]
% K = [4 x m x n-1] matrix. Its [4 x m] matrix stacked for n-1 iterations.

  %-----weight vectors-----%
  weights = [1/6, 2/6, 2/6, 1/6];
  c = [0 0.5 0.5 1];
  %-----eo vectors-----%
 
  %-----initialize-----%
  t = t(1):h:t(2);
  n = length(t);
  m = length(in_val);
  values = zeros(n, m); 
  values(1,:) = in_val;
  K = zeros(4, m, n-1);
  %-----eo initialize-----%
  
  for i = 1:n-1
    
    for j = 1:4
      if j == 1
        inputs = [t(i) values(i, :)];
      else
        inputs = [t(i)+c(j)*h (values(i,:) + c(j)*K(j-1,:,i) )];
      endif
      K(j,:,i) = h*fns(inputs);
    endfor
    
    values(i+1, :) = values(i,:) + weights*K(:,:,i);
    
  endfor
  
endfunction
```

I have written this code as a part of my learning experience. If there can be any improvements or clarifications, please let me know in the comments section below.

---

[^1]: Please note that, in the above implementation, I have made $k = hf$ which is different from the general implementations as seen in [Wikipedia]

[Wikipedia]: https://en.wikipedia.org/wiki/Runge%E2%80%93Kutta_methods#The_Runge%E2%80%93Kutta_method "The Runge–Kutta method"
