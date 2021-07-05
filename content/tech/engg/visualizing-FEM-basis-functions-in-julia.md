---
title: "Visualizing 1D & 2D FEM Basis Functions in Julia"
date: 2021-07-04T11:15:39+05:30
draft: true
katex: true
plotly: true
tags: ["Engineering"]
categories: ["🗃️ Tech", "🛠 Engg"]
typora-root-url: ../../../static
---

The Finite Element Method (FEM) is a mathematical tool using for solving differential equations. It has been popularly used (also, initially developed) for solving elastostatics problems which is to find the displacement $u$ such that,
$$
\sigma_{ij,j} + f_i = 0 \text{ in the domain }\Omega
$$
To solve this, the domain $\Omega$ is split into finite sub domains $\Omega_e$ in which the solution $u$ is (usually) approximated by a polynomial of certain order which is governed by the regularity requirements of the weak form of above PDE. 

The division into finite elements $\Omega_e$ is usually done as

- Lines for 1D problem (obviously)
- Quadrilaterals in 2D problems
- Hexahedrons in 3D problems

These finite elements are then mapped to a "Natural co-ordinate" system where they accordingly become

- Lines with $\xi_1 \in (-1,1)$
- Square with $\xi_1, \xi_2 \in (-1,1)$
- Cubes with $\xi_1, \xi_2, \xi_3 \in (-1,1)$

where $\xi_1, \xi_2, \xi_3$ are the $x,y,z$ co-ordinates in this bi-unit domain (called so since these values here range from $-1$ to $1$). 

Now, the equation of the solution is obtained by scaling the Lagrangian polynomials in this space by the nodal values of $u$ (it is these nodal values that FEM finally solves for). These Lagrangian polynomials are (usually) the **basis functions** of the finite elements. 

## 1-D Elements

See

![FEM1Delements](images/2021/visualizing-FEM-basis-functions-in-julia/FEM1Delements.png)

The above diagram shows the nodes for 1D elements. There are two main points to be noted:

- There are polynomials for each node of an element. And these polynomials are chosen such a way that these polynomials have value $1$ at that node and $0$ at all other nodes.
- Order of the polynomial $=\text{Number of nodes}-1$

The final solution is the sum of all these polynomials which can be given as 
$$
u(\xi) = \sum_{A=1}^{N_{\text{nodes}}}N_A(\xi)\bf u_A
$$
where,

- $N_A$ is the basis function at node A.
- $\bf u_A$ is nodal degree of freedom (value of displacement).
- $N_\text{nodes}$ is the total number of nodes per element.

The general Lagrangian basis function $N_A$ is given as,
$$
N_A(\xi) = \prod_{B=1 \\\\ B\not=A}^{N_\text{nodes}}\frac {\xi - \xi_B}{\xi_A - \xi_B}
$$
where $B$ iterates through all the nodes except A. It can be observed here that the value of basis function is always zero at all the nodes (except A).

```julia
# The generic Lagrangian basis function is
function N(ξ, order, node)
	ξ_B = range(-1, 1, length=order+1) |> collect
	ξ_A = ξ_B[node]
	N_A = 1
	for i in range(1, order+1)
		if i ≠ node
			N_A *= (ξ - ξ_B[i])/(ξ_A - ξ_B[i])
		end
	end
	N_A
end
```

Note that, we won't be using the generic function for the ease of comparison of various orders. Now that we are moving into plotting of basis functions, let me initialize the prerequisites in Julia.

```julia
using Plots
plotly()

ξ₁ = ξ₂ = range(-1, 1, step=0.01) |> collect
```



### 1D Linear Element

For linear elements, substituting the nodal $\xi$ values in the above basis function, we get the shape functions as follows,
<div>
$$
N_1^1(\xi) = \frac {1-\xi}{2} \\
N_2^1(\xi) = \frac {1+\xi}{2}
$$
</div>

The superscript 1 denotes that it is a linear element. The same basis functions can be obtained by calling the above function as `N(ξ, 1, node)` for each of the respective node. The corresponding plots are,

```julia
N₁1(ξ) = (1-ξ)/2
N₂1(ξ) = (1+ξ)/2
plt1 = plot(N₁1, -1, 1, title="N₁")
plt2 = plot(N₂1, -1, 1, title = "N₂")
plot(plt1, plt2, 
	legend=false,
	xlabel="ξ₁",
	ylabel="N")
```

{{< plotly json="/images/2021/visualizing-FEM-basis-functions-in-julia/1d_linear.json" height="600px" >}}

### 1D Quadratic Element

The quadratic shape function is given as,
<div>
$$
\begin{aligned}
N_1^2(\xi) &= \frac {\xi^2-\xi}{2} \\
N_2^2(\xi) &= \frac {\xi^2}{2} \\
N_2^2(\xi) &= \frac {\xi^2+\xi}{2}
\end{aligned}
$$
</div>
Again, the superscript $2$ denotes that its order is 2. 

```julia
N₁2(ξ) = (ξ-1)ξ/2
N₂2(ξ) = 1-ξ^2
N₃2(ξ)	= (ξ+1)ξ/2
plt1 = plot(N₁2, ξ₁, title="N₁")
plt2 = plot(N₂2, ξ₁, title = "N₂")
plt3 = plot(N₃2, ξ₁, title = "N₃")
plot(plt1, plt2, plt3,
	legend=false,
	xlabel="ξ₁",
	ylabel="N")
```

{{< plotly json="/images/2021/visualizing-FEM-basis-functions-in-julia/1d_quadratic.json" height="600px" >}}

### 1D Cubic Element

The cubic shape function is,
$$
\begin{aligned}
N_1^3(xi) = \frac{-1}{16}(9\xi^3 - 9\xi^2 - \xi + 1) \\
N_2^3(xi) = \frac{1}{16}(81\xi^2 -18 \xi - 1) \\
N_2^3(xi) = \frac{-1}{16}(81\xi^2 +18 \xi - 1) \\
N_4^3(xi) = \frac{1}{16}(27\xi^2 +18 \xi - 1) 
\end{aligned}
$$

