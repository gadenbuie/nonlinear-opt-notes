---
title:  'Nonlinear Optimization Lecture 14'
date: Thursday, March 3, 2016
author: Garrick Aden-Buie
...

# Homework 3 Review

## Problem 3

> Consider $\min f(x)$ s.t. $g_i(x) \leq 0$ for i = 1, \dots, m$. Let $\bar x$ be a feasilbe point and $I = \{i \colon g_i(\bar x) = 0\}$. Suppose $f$ is differentiable at $\bar x$ and $g_i$ for $i \in i$ differentiable and concave at $\bar x$ and $g_i$ for $i \not\in I$ is continuous at $\bar x$. Then consider

$$\begin{aligned}
\text{min}	&&&\nabla f(\bar x)^T d	& 	& \\
\text{s.t}	&&&\nabla g_i(\bar x)^T d \leq 0 &	&\forall i \in I \\
            &&&-1 \leq d \leq 1 &&\forall j = 1, \dots, n
\end{aligned}$$

> Let $\bar d$ be an optimal solution with objective function value $\bar z$.

### 3.b

> Show that if $\bar z <0$, then there exists $\delta >0$ such that $\bar x + \lambda \bar d$ is feasible, $f(\bar x + \lambda \bar d) < f(\bar x)$ for each $\lambda \in (0, \delta)$.

We know that $\nabla f(\bar x)^T \bar d < 0$ and $\nabla g_i(\bar x)^T \bar d_i \leq 0$ for all $i \in I$.
We also know that $g_i$ is concave $\forall i \in I$, which implies that $$g_i(y) \leq g_i(\bar y) + \nabla g_i(\bar y)^T (y - \bar y),\;\forall y, \bar y$$

Let $y = \bar x + \lambda \bar d$ and $\bar y = \bar x$.
Then $$g_i(\bar x + \lambda \bar d) \leq g_i(\bar x) + \nabla g_i(\bar x)^T \lambda \bar d,\;\forall \lambda \geq 0,\;\forall i \in I$$

Then (1) $g_i(\bar x + \lambda \bar d) \leq 0,\;\forall \lambda \geq 0,\;\forall i \in I$.
And (2) $g_i (\bar x + \lambda \bar d) \leq 0,\;\forall i \not\in I$. Then there exists $\delta_1 > 0$ such that $g_i(\bar x + \lambda \bar d) \leq 0$ for all $\lambda \in [0, \delta_1)$.
(1) + (2) implies that $\bar x + \lambda \bar d$ feasible for all $\lambda \in [0, \delta_1)$ and knowing that $\nabla f(\bar x)^T \bar d < 0$ gives us that $\exists \delta_2 > 0 \colon f(\bar x + \lambda \bar d) < f(\bar x),\;\forall \lambda \in (0, \delta_2)$.

Then if we let $\delta = \min \{\delta_1, \delta_2\}$ we have the proof.

### 3.c

> Show that if $\bar z = 0$ then $\bar x$ is a KKT point.

Rewrite the above problem as

$$\begin{aligned}
\text{min}	&&&c^T d	& 	& \\
\text{s.t}	&&&Ad \leq b		&	& \\
\end{aligned}$$

Where

$$\begin{aligned}
c &= \nabla f(\bar x) \\
b &= \begin{bmatrix} \mathbf{0}_I \\ \mathbf{1}_m \\ \mathbf{1}_m \end{bmatrix} \\
A &= \begin{bmatrix} \left.\begin{matrix} \nabla g_i(\bar x)^T \\ \vdots \end{matrix} \right\rbrace i \in I \\ I_m \\ -I_m \end{bmatrix} \\
d &= \begin{bmatrix} d_1 \\ d_2 \\ \vdots \\ d_m \end{bmatrix}
\end{aligned}$$

And the dual problem is

$$\begin{matrix}
\begin{aligned}
\max_w	&&&b^T w	& 	& \\
\text{s.t}	&&&A^T w = c		&	& \\
            &&&w \leq 0 &&\\
\end{aligned}
&
\Rightarrow
&
\begin{aligned}
\max_w	    &&&\sum_{j=1}^m \mu_j + \sum_{j=1}^m \eta_j	& 	& \\
\text{s.t}	&&&\begin{bmatrix} \nabla g_i(\bar x) & \dots & \vert & I & \vert & -I  \end{bmatrix}	\begin{bmatrix} \lambda \\ \mu \\ \eta \end{bmatrix} = \nabla f(\bar x)	&	& \\
            &&&\lambda, \mu, \eta \leq 0 &&\\
\end{aligned}
\end{matrix}$$

If $\bar z = 0$, then $\mu = 0$ and $\eta = 0$.

Then the constraint becomes

$$\begin{aligned}
&\sum_{i \in I} \nabla g_i(\bar x)\lambda_i = \nabla f(\bar x), &\lambda_i \leq 0 \\
\Rightarrow &\nabla f(\bar x) - \sum_{i \in I} \nabla g_i(\bar x)\lambda_i = 0
\end{aligned}$$

Let $\rho_i = -\lambda_i \geq 0$.
Then $$\nabla f(\bar x) + \sum_{i \in I} \nabla g_i(\bar x)\rho_i = 0$$


# Review

## Unconstrained Optimization

- Line Search
    - Single dimension problem: $\min f(x),\; a \leq x \leq b$, we know $x^* \in [a, b]$ and $f(x)$ is strictly quasiconvex.
- Dichotomous Search
- Golden Section Search
- (No derivatives used in the above...)

# Line Search with Derivative

We are still minimizing $f(x),\; x \in \mathbb{R}$, but we are going to use $f^\prime(x)$ and $f$ is pseudoconvex, hence differentiable.

- Bisection Method
    - Will cover next lecture
    - Evaluate $f^\prime(\frac{a+b}{2})$ and depending on the direction decide which section of $[a,b]$ to explore.
