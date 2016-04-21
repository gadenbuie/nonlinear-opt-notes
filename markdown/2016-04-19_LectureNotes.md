---
title:  'Nonlinear Optimization Lecture 24'
date: Tuesday, April 19, 2016
author: Garrick Aden-Buie
...

# Network User Equilibrium

Definitions for Graph $G(N, A)$:

- $N$: set of nodes
- $A$: set of arcs
- $W$: set of O-D pairs
- $T_{ij}$: fixed travel demand for O-D pairs
- $u_{ij}$: minimum travel time for O-D pairs
- $P_{ij}$: set of paths from node $i$ to node $j$
- $c_{p}$: unit cost of travel along path $p$
- $h_{p}$: flow rate on path $p$
- flow vector $h = (h_{p} \colon p \in P)$
- $P = \cup_{(i,j) \in W} P_{ij}$
- $c_{p}(h)$ cost as a function of flow rate

*Definition*. A vector $h$ is a user equilibrium if it obeys the following conditions

$$h_{p} > 0 \Rightarrow c_{p}(h) = u_{ij}$$

for all $p \in P_{ij}$, for all $(i,j) \in W$, where $u_{ij} = \min_{p \in P_{ij}} c_{p}(h)$

and

$$\sum_{p \in P_{ij}} h_p = T_{ij}$$

for all $(i,j) \in W$ and $h \geq 0$.

In the second condition $T_{ij}$ is the travel demand between $i$ and $j$ and the conditions states that total flow across all paths from $i$ to $j$ needs to satisfy this demand.
The first condition states that if flow rate on a path is greater than zero, then the cost on that path, taking into account the flow rate, minimizes the travel cost from $i$ to $j$.
Intuitively, if the overall flow rates on the paths from $i$ to $j$ does not give a minimum cost, then it cannot be a *user equilibrium*.

## User Equilibrium

$$\text{UE } \left\lbrace\begin{aligned}
(c_p - u_{ij}) h_p &= 0 &&\forall (i,j) \in W, p \in P_{ij} \\
c_p - u_{ij} &\geq 0 &&\forall (i,j) \in W, p \in P_{ij} \\
\sum_{p \in P_{ij}} h_p - T_{ij} &= 0 &&(i,j) \in W \\
h_p &\geq 0 &&\forall p \in P
\end{aligned}\right.$$

The conditions 1, 2, and 4 are equivalent to a NCP^[*Nonlinear Complimentary Problem*. See Lecture 20 from April 5, 2016. $$\text{NCP} = \begin{aligned} F(y)^T y &= 0 \\ F(y) &\geq 0 \\ y &\geq 0\end{aligned}$$].
We need some more notation to be able to add condition 3 into the NCP formulation.

![Illustration of flow rate and cost function, with transportation example using BPR[^bpr].](images/lec24/24-1.png)

[^bpr]: See <https://en.wikipedia.org/w/index.php?title=Route_assignment&section=4#Frank-Wolfe_algorithm>

### Path-arc conversion

$$\begin{aligned}
\delta_{ap} &= \begin{cases} 1 &\text{if arc } a \text{ belongs to path } p \\ 0 &\text{otherwise} \end{cases} \\
\Delta &= (\delta_{ap} \colon a \in A, p \in P) =\;\text{arc-path incidence matrix} \\
f_a &= \sum_{p \in P}\delta_{ap} h_p =\;\text{flow rate across arc } a\\
c_p(h) &= \sum_{a \in A} \delta_{ap} c_a (f_a)
\end{aligned}$$

If we know $h_p$ for all paths in $P$, then we can compute $f_a$.
On the other hand, if the network is complicated, it can be very difficult to calculate path flow rates, because knowing the number of objects traveling on an arc does not necessarily tell you the origin/destination of those objects.
In other words $h \to f$ is unique, but $f \to h$ is not unique.

## User Equilibrium as Nonlinear Complimentary Problem (NCP)

Assume that $c_a (f_a) > 0 \;\forall f_a \geq 0, a \in A$.
Any pair $(h, u)$ is a user equilibrium (UE) if:

$$\text{NCP } \left\lbrace\begin{aligned}
(c_p - u_{ij}) h_p &= 0 &&\forall (i,j) \in W, p \in P_{ij} \\
c_p - u_{ij} &\geq 0 &&\forall (i,j) \in W, p \in P_{ij} \\
(\sum_{p \in P_{ij}} h_p - T_{ij}) u_{ij} &\geq 0 &&\forall(i,j) \in W \\
u_{ij} &\geq 0 &&\forall(i,j) \in W \\
\sum_{p \in P_{ij}} h_p - T_{ij} &\geq 0 &&\forall(i,j) \in W \\
h_p &\geq 0 &&\forall p \in P \\
\end{aligned}\right.$$

*Proof.*
We need to prove two things: UE $\Rightarrow$ NCP (obvious); and NCP $\Rightarrow$ UE (proven by contradiction): Assume that there exists some flow vector $h$ that satisfies the NCP but not UE.

## User Equilibrium as Variational Inequality (VI)  

$$\Omega = \{h \colon h \geq 0, \sum_{p \in P_{ij}} = T_{ij} \;\forall (i,j) \in W$$

VI is to find $h^* \in \Omega$:

$$\sum_{p \in P} c_p (h^*) (h_p - h_p^*) \geq 0 \;\forall h \in \Omega$$

$$\begin{aligned}
F(h) &= \begin{bmatrix} \vdots \\ c_p(h) \\ \vdots \end{bmatrix} \\
h &= \begin{bmatrix} \vdots \\ h_p \\ \vdots \end{bmatrix} \\
F(h^*)^T (h - h^*) &\geq 0 \;\forall h \in \Omega
\end{aligned}$$

*Proof.* (UE $\Rightarrow$ VI)

$h^*$ is a UE flow.
Then $c_p(h^*) \geq u_{ij} \;\forall p \in P_{ij}, (i,j) \in W$.

This is equivalent to $$\Rightarrow c_p(h^*)(h_p - h_p^*) \geq u_{ij}(h_p - h_p^*) \;\forall p \in P_{ij}, (i,j) \in W$$


If $h_p - h_p^* \geq 0$ then this is clear.
But if $h_p - h_p^* < 0$, then because $h_p$ is any $h_p$, $h_p^* > h_p \geq 0$ so $h_p^* > 0$, which implies that $c_p - u_{ij}$.

Now taken over all paths

$$\sum_{p \in P_{ij}} c_p(h^*)(h_p - h_p^*) \geq \sum_{p \in P_{ij}} u_{ij}(h_p - h_p^*) \;\forall (i,j) \in W$$

And if we consider just the right-hand side, this is equivalent to

$$\sum_{p \in P_{ij}} u_{ij}(h_p - h_p^*) = u_{ij}(\sum_{p \in P_{ij}} h_p - \sum_{p \in P_{ij}} h_p^*)$$

Note that $\sum_{p \in P_{ij}} h_p = T_{ij}$ and that $\sum_{p \in P_{ij}} h_p^*) = T_{ij}$ as well, so the right hand side is equal to 0.
