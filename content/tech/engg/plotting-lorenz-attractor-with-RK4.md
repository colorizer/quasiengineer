---
title: "Plotting Lorenz Attractor With RK4"
date: 2021-06-16T21:33:04+05:30
draft: false
katex: true
tags: ["Engineering"]
categories: ["🗃️ Tech", "🧰 Engg"]
typora-root-url: ../../../static
---

One of the classical example of chaos is always the Lorenz attractor. No matter how carefully you choose the values, however close they are, the end result is always different. And the fact that this never intersecting, unique set of values are bound within a domain which looks like a butterfly links it uniquely to the famous quote,

> It has said that something as small as the flutter of a butterfly's wing can ultimately cause a typhoon halfway around the world.

There is this [small article](https://www.americanscientist.org/article/understanding-the-butterfly-effect) in American Scientist which shines some lights on it. More than that, the following video from Veritasium goes in depth, which actually got me into plotting it out.
{{< youtube fDek6cYijxI >}}

I wanted to implement the Lorenz attractor, which is found in the front page of [Julia Plots](https://docs.juliaplots.org/latest/), but using the GLMakie package which I am trying to learn.

```julia
using GLMakie

Base.@kwdef mutable struct Lorenz
    h::Float64 = 0.01
    σ::Float64 = 10
    ρ::Float64 = 28
    β::Float64 = 8/3
    t::Float64 = 0
    x::Float64
    y::Float64
    z::Float64
end
```

I've followed the same struct setup of the Julia plots site but I'm implementing it using RK4 instead of Forward Euler followed by that site. I'll follow the similar setup I had followed for [RK4 implementation in GNU Octave / Matlab]({{<ref "rk4-for-coupled-odes-in-octave">}}) but the code is considerably smaller given this is implemented in Julia (and recording of all data is not necessary).

```julia
function RK4(h::Float64, f::Function, vals::Array{Float64})::Array{Float64}
    tn, xn, yn, zn = vals
    k1 = h*f(tn, xn, yn, zn)
    k2 = h*f(tn+h/2, xn+k1[1]/2, yn+k1[2]/2, zn+k1[3]/2)
    k3 = h*f(tn+h/2, xn+k2[1]/2, yn+k2[2]/2, zn+k2[3]/2)
    k4 = h*f(tn+h, xn+k3[1], yn+k3[2], zn+k3[3])
    newvals = vals.+[h; (k1+2k2+2k3+k4)/6]
    return newvals
end
```

Consider a simplified model for the fluid circulation in a fluid layer that is heated from below and cooled from above. This is given by the following set of three coupled ordinary differential equations

<div>
$$
\begin{aligned}
\frac{dx}{dt}&= \sigma (y-x) \\
\frac{dy}{dt} &= x(\rho - z) \\
\frac{dz}{dt} &= xy - \beta z
\end{aligned}
$$
</div>

This is defined within the step function below. Actually, here we will plot three Lorenz attractors, each with slightly different initial condition than the other. Let's see how they grow!

```julia
function step!(l::Lorenz)
    dx(t,x,y,z) = l.σ*(y-x)
    dy(t,x,y,z) = x*(l.ρ-z)
    dz(t,x,y,z) = x*y-l.β*z
    v(t,x,y,z) = [dx(t,x,y,z), dy(t,x,y,z), dz(t,x,y,z)]
    vals = [l.t, l.x, l.y, l.z]
    l.t, l.x, l.y, l.z = RK4(l.h, v, vals)
end

attractor1 = Lorenz(x=1, y=1, z=1)
attractor2 = Lorenz(x=1.1, y=1.1, z=1.1)
attractor3 = Lorenz(x=1.2, y=1.2, z=1.2)
```

GLMakie uses a function called `Node()` to give numbers special power. That is, all these nodes, when updated, will update the functions which uses them (my current understanding; please correct if I'm wrong!).  Hence, what I've done is to implement each point as a Node so that we step through the attractor, we can update these points and hence the plot gets updated. This update is passed to the record function along with the figure and it records the animation at a configured frame rate. Also, I've made the variable `az` a node so that I can update azimuth (rotation) of camera for each frame. If further clarification is needed, one can refer to this [youtube tutorial](https://www.youtube.com/watch?v=UXVH7yEDf58) or [GLMakie docs](https://makie.juliaplots.org/stable/animation.html).

```julia
fig = Figure(resolution=(1920,1080))
az = Node(1.01π)
ax = Axis3(fig[1,1], limits=(-30, 30, -30, 30, 0, 60),azimuth=az, perspectiveness=0.0)
hidedecorations!(ax)
hidespines!(ax)
points1 = Node(Point3f0[(attractor1.x, attractor1.y, attractor1.z)])
points2 = Node(Point3f0[(attractor2.x, attractor2.y, attractor2.z)])
points3 = Node(Point3f0[(attractor3.x, attractor3.y, attractor3.z)])
lines!(ax, points1, color=:orangered2)
lines!(ax,points2, color=:purple3)
lines!(ax,points3, color=:green3)
frames = 1:600

record(fig, "lorenz.mp4", frames; framerate=30) do i
    for j in 1:4
        step!(attractor1)
        step!(attractor2)
        step!(attractor3)
        new_point1 = Point3f0(attractor1.x, attractor1.y, attractor1.z)
        new_point2 = Point3f0(attractor2.x, attractor2.y, attractor2.z)
        new_point3 = Point3f0(attractor3.x, attractor3.y, attractor3.z)
        points1[] = push!(points1[], new_point1)
        points2[] = push!(points2[], new_point2)
        points3[] = push!(points3[], new_point3)
    end
    az[] = az[] + 0.01
end
```

This is the end result.

{{< youtube EFBq2tZKOEE >}}

Note how the three curves, initially together, diverge and continue to follow different paths!
