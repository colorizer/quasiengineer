---
title: "My First Post 😃"
date: 2021-01-03T16:32:44+05:30
draft: true
tags: ["Engineering"]
categories: ["🗃️ Tech", "🛠 Engineering"]
---

### Limits imposed by Local Buckling

The competition between failure modes results in local buckling if shape is optimised for other failure modes

Example, thin walled tubes are stiff but buckle locally.

![/images/quasiengineer_plain.png]("/images/quasiengineer_plain.png")


Hence we need the *upper limit for the shape efficiency.*($EI$)

$$\displaystyle{\phi ^B_{max} = 2.3 \left( \frac{E}{\rho} \right) ^{\frac{1}{2}}}$$

$$\displaystyle{\phi ^B_{max}= \sqrt{\phi ^E_{max}} }$$

Hence we use the method of **four quadrant of charts** to decide the limits imposed on one by other.


1. Choose the material and mark its $\displaystyle{E, \rho}$
2. Decide its stiffness in the Stiffness chart ($EI$)
3. Decide upon the Shape in the Shape factor chart ($A/I$)
4. Finally, it provides the performance for that combination in the 3rd quadrant.


#### Strength-limited Design


### Material Indices that Include Shape

Most indices don't need this refinement - the performance they characterise doesn't depend on shape. But stiffness and strength-limited design do.

The above chart method is clumsy. Better way is to include them into the Material indices.

##### Elastic bending & twisting of Shafts

$$\displaystyle{m = \rho A L}$$

Where L is a constraint.

We try to eliminate the free variable A here with

Stiffness is given by $$\displaystyle{S_B = C_1 \frac{EI}{L^3}}$$

Replacing I by $$\displaystyle{\phi _B}$$
$$
\displaystyle{S_B = \frac{C_1}{12} \frac{E}{L^3}\phi ^e_B A^2}
$$
We use this to eliminate the free variable, this leads to the material index (which is to be maximised for minimum mass),
$$
\displaystyle{M_1 = \frac{\left( \phi ^e_B E \right) ^{\frac{1}{2}}}{\rho}}
$$

##### Failure of beams and Shafts

Failure occurs if the load exceeds the moment 
$$
\displaystyle{M = Z. \sigma_f}
$$

### Co-selection of Material & Shape

The equation 

