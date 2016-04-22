---
title:  'Nonlinear Optimization Lecture 20'
date: Tuesday, April 5, 2016
author: Garrick Aden-Buie
...

# Game Theory Intro

There are two purposes to game theory: descriptive and predictive.
In engineering, the primary use is *predictive*.

# Noncooperative $N$-Player Game

# Theorem. Nash Equilibrium Problem

For each player $i$:

$$\begin{aligned}
\text{max}	&&&u_i (x^i, x^{-i})	& 	& \\
\text{s.t}	&&&x^i \in X_i \subset \mathbb{R}^{m_i}		&	& \\
&&&X = \prod_{i=1}^N X_i = X_1 \times X_2 \times \cdots \times X_N
\end{aligned}$$

where $u_i \colon X \to \mathbb{R}$ is continuously differentiable with respect to $x^i$ or pseudo-concave with respect to $x^i$.

$x^* \in X$ is[^1] a solution to $NE(X,u)$ if and only if $x^* \in X$ satisfies $$\sum_{i=1}^N \left\lbrack \nabla_{x^i} u_i (x^*) \right\rbrack^T (x^i - x^{i*}) \leq 0 \;\forall x \in X$$

[^1]: $x^* = (x^{1*}, x^{2*}, \dots, x^{N*})$

This kind of problem is called *variational inequality*, because the form of the inequality changes with $x^i - x^{i*}$, as in the number of inequalities that $x^*$ must satisfy is infinite, as the above must be satisfied $\forall x$.

*Recall.* For $\min f(x)$ s.t. $x \in X$, $x^* \in X$ is optimal if and only if $\nabla f(x^*)^T (x - x^*) \geq 0\;\forall x \in X$.

*Remark.* In the following formulation, the optimum is for the global "system" maximum. Note the difference with the Nash equilibrium.

$$\begin{aligned}
\text{max}	&&&\sum_{i=1}^N u_i (x) 	& \\
\text{s.t}	&&&x \in X		&	& \\
\Leftrightarrow &&& \sum_{i=1}^N (\nabla_x u_i)^T (x - x^*) \leq 0 &&\forall x \in X \\
\end{aligned}$$

*Proof ($\Rightarrow$)*. For each $i$: given $x^{i*}$, $x^{i*}$ maximizes $u_i$.

$$\left\lbrack \nabla_{x^i} u_i (x^{i*}, x^{-i*}) \right\rbrack^T (x^i - x^{i*}) \leq 0 \;\forall x^i \in X_i$$

This then simply leads to the Variational Inequality, so proven.

*Proof ($\Leftarrow$)*. Assume that $x^*$ satisfies the VI, and show that it is a nash equilibrium point.

Fix $j \in {1, 2, \dots, N}$ and let $y = \begin{bmatrix} x^{1*}, x^{2*}, \dots, y^j, \dots, x^{N*} \end{bmatrix}$ for some $y^j \in X^j$.
Essentially: take the optimal for all players not $j$ and let one player's strategy vary.
Note also that $y \in X$.

From here, when taking $x^i - x^{i*}$, all terms cancel except $y^j$.

$$\left\lbrack \nabla_{x^j} u_j (x^*) \right\rbrack^T (y^j - x^{j*}) \leq 0$$

Because our choice of $y^j$ was arbitrary, we can do the same thing for all $y^j \in X_j$.
Then $x^{j*}$ maximizes $u_j$ given $x^{j*}$ (because pseudo-convex).

### Scalar-based version of Nash Equilibrium Variational Inequality

$$\sum_{i=1}^N \sum_{j=1}^{m_i} \frac{\partial u_i(x^*)}{\partial x^i_j} (x^i_j x_j^{i*}) \leq 0 \;\forall x \in X$$

# Variational Inequality

*Definition.*

$$\begin{aligned}
VI(F, \Omega) \\
\Omega \subset \mathbb{R}^n \;\text{non-empty}\\
F \colon \Omega \to \mathbb{R}^n \\
VI(F, \Omega) \;\text{is to find a vector } y \\
\text{such that } y \in \Omega \\
\lbrack F(y) \rbrack^T (x - y) \geq 0 \;\forall x \in \Omega \\
\langle F(y), x-y \rangle \geq 0 \;\forall x \in \Omega
\end{aligned}$$

# Nonlinear Complimentary Problem

$F \colon \mathbb{R}^n \to \mathbb{R}^n$. $NCP(F)$ is to find a vector $y$ such that

$$\begin{aligned}
F(y)^T y &= 0 \\
F(y) &\geq 0 \\
y &\geq 0
\end{aligned}$$

Note that this is similar to the KKT conditions, but more general.
Sometimes these three conditions are written in the following form:

$$ 0 \leq F(y) \perp y \geq 0$$

# Fixed-Point Problem

- $\Omega in \mathbb{R}^n$ non-empty
- $F \colon \Omega \to \Omega$
- $FPP(F, \Omega)$ is to find a vector $y$ such that $y \in \Omega, y = F(y)$.
- This is related to the notion of equilibrium.

# Minimum Norm Projection

$$\begin{aligned}
y &= P_\Omega [v] && v \in \mathbb{R}^n, \Omega \subset \mathbb{R}^n &&(v \text{ vector}, \Omega \text{ set}) \\
&= \arg\min_{x \in \Omega} \Vert v - x \Vert \\
\Rightarrow y &\in \Omega
\end{aligned}$$

# Fixed-Point Problem based on Min Norm Projection

An extension of the general form.

- $\Omega \subset \mathbb{R}^n$ non-empty
- $F \colon \Omega \to \Omega$
- $FPP_{\min} (F, \Omega)$ is to find a vector $y$ such that $y \in \Omega$ and $y = P_{\Omega} [y - F(y)]$.

Here $P_{\Omega}$ is the projection onto feasible space and $F(y)$ is like the gradient of vector function.
But FPP implies you stay at some point $\Rightarrow$ optimal solution.

$$y = P_{\Omega} [y - F(y)] \Rightarrow y = \arg\min_{x \in \Omega} \Vert y - F(y) - x \Vert$$

# Connection between VI, NCP, FPP~min~

So far we have been discussing VI, NCP, FPP~min~ and we are going to now show that these three are all related.

Consider the following optimization problem:

$$\left.\begin{aligned}
\text{min}	&&&f(x)	& 	& \\
\text{s.t}	&&&x \in X		&	& \\
&&&f \text{ pseudoconvex} \\
&&&X \text{ convex}
\end{aligned} \right\rbrace \Rightarrow \nabla f(x^*)^T (x - x^*) \geq 0 \;\forall x \in X$$

Whenever you have an optimization problem in this situation, you can convert to VI problem.

What is we have VI problem $VI(F, \Omega) \colon F(y)^T (x - y) \geq 0 \;\forall x \in \Omega$?
We can go from the optimization problem to the VI using gradient.
Can we go VI $\to$ optimization?
The following theorem shows this.

# Theorem

Suppose $\Omega \subset \mathbb{R}^n$ and $F \colon \Omega \to \mathbb{R}^n$.

Then $VI(F, \Omega)$ is equivalent to $\min \oint_0^x F(z) dz$ s.t. $x \in \Omega$.

**Note.** $x,z,dz$ are all vectors with dimension $n$, so the integral is a line integral $\oint$.

The theorem holds if $\oint_0^x F(z) dz$ is *single-valued*, where single-valued means that $\oint_0^x F(z) dz = c \;\forall$ paths from $\mathbf{0} \to \mathbf{x}$.
