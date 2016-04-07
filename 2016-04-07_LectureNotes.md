---
title:  'Nonlinear Optimization Lecture 21'
date: Thursday, April 7, 2016
author: Garrick Aden-Buie
...


# Review

- $VI(F, \Omega)$
    - $y \in \Omega, F(y)^T(x - y) \geq 0\;\forall x \in \Omega$
- $NCP(F)$
    - $F(y)^T y = 0$
    - $F(y) \geq 0$
    - $y \geq 0$
- $FPP_{\min}(F, \Omega)$
    - $y \in P_{\Omega} \lbrack y - F(y) \rbrack$
    - $y \in \Omega$


# Theorem

If $\Omega  = \mathbb{R}^n_+$[^1] then $VI(F, \Omega) \Leftrightarrow NCP(F)$.

*Proof ($\Rightarrow$).* If $y$ is a solution of $VI(F, \Omega)$, then $y$ is a solution of $NCP(F)$.

$$F(y)^T (x - y) \geq 0 \;\forall x \in \mathbb{R}^n_+$$

i.  $x = 0 \in \mathbb{R}^n_+$: $F(y)^T (-y) \geq 0$

ii.  $x = 2y \in \mathbb{R}^n_+$: $F(y)^T y \geq 0$

iii.  (i) & (ii) $\Rightarrow F(y)^T y = 0$. Now we need to show that $F(y) \geq 0$.

    Suppose not: $F(y) \not\geq 0 \Rightarrow \exists j \in 1, \dots, n$ such that $F_j(y) < 0$, which is to say that $F(y)$ is not non-negative.

    $$\begin{aligned}
    F(y)^T (x - y) &= \sum_{i=1}^n F_i(y) (x_i - y_i) \geq 0 \\
    \text{Pick } x &= \begin{bmatrix} y_1 \\ \vdots \\ x_j = \infty \\ \vdots \\ y_n \end{bmatrix}
    \end{aligned}$$

    Now, then $x_i - y_i = 0$ for all elements that are not $x_j$, but then $x_j$ forces $F_j(y) (x_j - y_j) < 0$, so contradiction.

*Proof ($\Leftarrow$).* If $y$ is a solution to $NCP(F)$, then $y$ is also a solution to $VI(F, \Omega)$. $F(y) \geq 0, y \geq 0, F(y)^T y = 0$.
Then we choose an $x \in \Omega$ which will by definition be non-negative and observe the following

$$\begin{aligned}
F(y)^T x &\geq 0 &&\forall x \in \Omega\\
\Rightarrow F(y)^T x - F(y)^T y &\geq 0 &&\forall x \in \Omega\\
\Rightarrow F(y)^T (x - y) &\geq 0 &&\forall x \in \Omega
\end{aligned}$$


# Theorem

$\Omega \subset \mathbb{R}^n$ convex, nonempty, closed.
Then $FPP_{\min} (F, \Omega) \Leftrightarrow VI(F, \Omega)$.

*Proof.* $P_{\Omega} \lbrack y - F(y) \rbrack$ requires a solution to

$$\begin{aligned}
\min_x	&&&\Vert (y - F(y)) - x \Vert	& 	& \\
\text{s.t}	&&&x \in \Omega		&	& \\
\end{aligned}$$

Without loss of generality we can rewrite as

$$\begin{aligned}
\min_x	&&&\frac 1 2 \Vert (y - F(y)) - x \Vert^2	& 	& \\
\text{s.t}	&&&x \in \Omega		&	& \\
\end{aligned}$$

Which is also the same as

$$\begin{aligned}
\min_x	&&&\frac 1 2 (y - F(y) - x)^T (y - F(y) - x) = Z(x;y) & 	& \\
\text{s.t}	&&&x \in \Omega		&	& \\
\end{aligned}$$

Now, we can rewrite this as the KKT conditions, which are sufficient conditions given the convexity of $\Omega$, although in this case we'll use the VI-type optmiality:

$$\Leftrightarrow \nabla_x Z(x^*; y)^T (x - x^*) \geq 0 \;\forall x \in \Omega$$

But note that $x, x^*$, and $y$ are all the same at the end, because we are solving the Fixed-Point Problem.

Note that in the simple case if we have $\Omega$ convex, then $\min f(x)$ s.t. $x \in \Omega \Leftrightarrow \nabla f(x^*)^T (x - x^*) \geq 0 \;\forall x \in \Omega$.
So in this case, note that

$$\begin{aligned}
\nabla_x Z(x^*; y) &= - (y - F(y) - x^*) &&\\
( \text{Note that } \nabla_x Z(x^*; y) &= \left. \nabla_x Z(x; y) \right\vert_{x = x^*} ) &&\\
\Leftrightarrow - (y - F(y) - x^*)^T (x - x^*) &\geq 0 &&\forall x \in \Omega
\end{aligned}$$

At this point we have shown that $FPP_{\min} (F \Omega) \Rightarrow VI(F, \Omega)$, and we have that $y = x^*$.

The next step is to show that $VI(F, \Omega) \Rightarrow FPP_{\min} (F, \Omega)$.
Start from the condition $F(y)^T (x - y) \geq 0 \;\forall x \in \Omega$ (1).
We also have $- (y - F(y) - x^*)^T (x - x^*) \geq 0$ (2) which gives $x^*$ as a result of the projection.

So from the side of (1), $y$ is a VI solution and $x^*$ is a projection result from a given $y$.
So we pick $x = x^*$.
This gives $F(y)^T (x^* - y) \geq 0$.

Then from (2), pick $x = y \Rightarrow -(y - x^*)^T (y - x^*) + F(y)^T (y - x^*) \geq 0 \Rightarrow 0 \geq F(y)^T (y - x^*) \geq (y - x^*)^T (y - x^*) \geq 0$.
Notice that $(y - x^*)^T (y - x^*)$ is sandwiched between 0 and 0, so $y$ needs to be $x^*$.

Overall, the proof starts with knowing that at the end $x, y$, and $x^*$ are all the same, but starting from the assumption that they may be different.



# Existence (of Fixed-Point)

## Brower's Fixed-Point Theorem

If $\Omega$ is a convex, nonempty and compact set and $F(x)$ is continuous on $\Omega$, then the fixed-point problem

$$\begin{aligned}
x &= F(x) \\
x &\in \Omega
\end{aligned}$$

has a solution.

## Theorem

- $\Omega$ convex, nonempty, compact
- $F(x)$ continuous on $\Omega$
- Then $VI(F, \Omega)$ has a solution

*Proof.* $VI(F, \Omega) \Leftrightarrow FPP_{\min} (F, \Omega)$.
Then $y = P_{\Omega} (y - F(y))$, or equivalently $y = G(y)$.
If we can show that $G(y)$ is continuous, then we are done.
From advanced linear algebra (and commonly taught in advance linear algebra courses), the projection operator is continuous, so $G(y)$ is continuous.

## Theorem: Nash Game

$\max u_i (x^i; x^{-i})$

If

- $u_i$ is pseudo-concave with respect to $x^i$ for all $x^{-i}$.
- $\Omega = \prod_{i = 1}^N \Omega_i$ is convex, compact, nonempty

Then there exists a Nash equilibrium.

# Uniqueness

- Optimization: strictly pseudoconvex
- Nash equilibrium: strictly monotone

## Definition

- $F \colon \mathbb{R}^n \to \mathbb{R}^n$
- $F$ is (strictly) monotone on $\Omega$ if
    $$\begin{aligned}
    \left\lbrack F(y^1) - F(y^2)) \right\rbrack^T (y^1 - y^2) &\geq (>) 0 \\
    \forall y^1, y^2 \in \Omega \;&\; (y^1 \neq y^2)
    \end{aligned}$$


## Theorem

**If** $y \in \Omega \subset \mathbb{R}^n$ is a solution of $VI(F, \Omega)$ and $F(\cdot)$ is strictly monotone

**Then** $y$ is the unique solution.
