---
title: "Vectorised Code for RK4 in Octave"
date: 2021-01-08T01:26:42+05:30
draft: false
tags: ["Engineering"]
categories: ["🗃️ Tech", "🛠 Engineering"]
typora-root-url: ../../../static/images
---

RK4 is one of the most prominent computational method used for solving numerical problems.

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

