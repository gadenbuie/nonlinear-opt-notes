---
title:  'Nonlinear Optimization Lecture 22'
date: Tuesday, April 12, 2016
author: Garrick Aden-Buie
...

# Examples of a Mathematical Game

- Two players
- Each player produces two types of products
- Price is a function of total production (oligopoly)
    - $q_{ij}$: production quantity of product $i$ by player $j$
    - $p_i$: market price of product $i$
    - Example:
        - $p_1 = \pi_1 (q_{11} + q_{12}) = a_1 - b_1(q_{11} + q_{12}) = 100 - 2(q_{11} + q_{12})$
        - $p_2 = \pi_2 (q_{21} + q_{22}) = a_2 - b_2(q_{21} + q_{22}) = 200 - 5(q_{21} + q_{22})$

## Player 1

Then Player 1's problem is

$$\begin{aligned}
\max        &&& u_1 (\text{own variables};\; \text{other's variables}) \\
            &&&= u_1 (q_{11}, q_{21}; q_{12}, q_{22}) \\
            &&&= p_1 q_{11} + p_2 q_{21} - c_{11}q_{11} - c_{21} q_{21} \\
            &&&= (100 - 2(q_{11} + q_{12})) q_{11} + (200 - 5(q_{21} + q_{22})) q_{21} -q_{11} - 2 q_{21} \\
\text{s.t}	&&&3 q_{11} + 5q_{21}		&	& \\
            &&&q_{11}, q_{21} \geq 0
\end{aligned}$$

Note that in the above, the optimization problem is not subject to any variables that are not the *player's* variables.
If it is the case that the problem is dependent on outside player's variables, then we cannot use the variational inequality theorem and the problem is becomes somewhat more difficult.

Also note that the terms $-q_{11} - 2 q_{21}$ represent the cost of producing products 1 and 2 for player 1, and the cost is twice as much to player 1 for product 1 than for product 2.

## Player 2

$$\begin{aligned}
\max        &&&= u_2  (q_{12}, q_{22}; q_{11}, q_{21}) \\
            &&&= (100 - 2(q_{11} + q_{12})) q_{12} + (200 - 5(q_{21} + q_{22})) q_{22} - 2 q_{12} -  q_{22} \\
\text{s.t}	&&&4 q_{12} + 3 q_{22} \leq 40 &	& \\
            &&&q_{12}, q_{22} \geq 0
\end{aligned}$$


## Cournot Competition

*Recall.* $\max f(x)\; \text{s.t. } x \in X \Leftrightarrow \nabla f(x^*)^T (x - x^*) \leq 0 \;\forall x \in X$

### Player 1

$$\nabla_{q_{11}, q_{12}} =
  \begin{bmatrix} 100 - 2(q_{11} + q_{12}) - 2q_{11} - 1 \\
                  200 - 5(q_{21} + q_{22}) - 5q_{21} - 2 \\
  \end{bmatrix} = \begin{bmatrix} \frac{\partial u_1}{\partial q_{11}} \\ \frac{\partial u_1}{\partial q_{21}}  \end{bmatrix}$$

Given $q_{12}^*, q_{22}^*$,

$$\frac{\partial u_1 (q_{11}^*, q_{21}^*; q_{12}^*, q_{22}^*)}{\partial q_{11}} (q_{11} - q_{11}^*) + \frac{\partial u_1 (q_{11}^*, q_{21}^*; q_{12}^*, q_{22}^*)}{\partial q_{21}} (q_{21} - q_{21}^*) \leq 0$$

or similarly

$$\begin{bmatrix} 100 - 2(q_{11}^* + q_{12}^*) - 2q_{11}^* - 1 \\
                  200 - 5(q_{21}^* + q_{22}^*) - 5q_{21}^* - 2
  \end{bmatrix} \begin{bmatrix} q_{11} - q_{11}^* \\ q_{21} - q_{21}^* \end{bmatrix} \leq 0$$

for all $q_{11}, q_{21} \in X_1$

## Player 2

Following a similar process we arrive at

$$\begin{bmatrix} 100 - 2(q_{11}^* + q_{12}^*) - 2q_{12}^* - 2 \\
                  200 - 5(q_{21}^* + q_{22}^*) - 5q_{22}^* - 1
  \end{bmatrix} \begin{bmatrix} q_{12} - q_{12}^* \\ q_{22} - q_{22}^* \end{bmatrix} \leq 0$$

for all $q_{12}, q_{22} \in X_2$

## Combined

We then combine these into a single problem:

$$\begin{bmatrix} 100 - 2(q_{11}^* + q_{12}^*) - 2q_{11}^* - 1 \\
                  200 - 5(q_{21}^* + q_{22}^*) - 5q_{21}^* - 2 \\
                  100 - 2(q_{11}^* + q_{12}^*) - 2q_{12}^* - 2 \\
                  200 - 5(q_{21}^* + q_{22}^*) - 5q_{22}^* - 1
  \end{bmatrix}
  \begin{bmatrix} q_{11} - q_{11}^* \\
                  q_{21} - q_{21}^* \\
                  q_{12} - q_{12}^* \\
                  q_{22} - q_{22}^*
  \end{bmatrix} \leq 0$$

for all $q_{11}, q_{21}, q_{12}, q_{22} \in X_1 \times X_2 = X$.

Written in another way:

$$\begin{aligned}
F(q^*)^T (q - q^*) &\leq 0 & q &\in X \\
q &= \begin{bmatrix} q_{11} \\ q_{21} \\ q_{12} \\ q_{22} \end{bmatrix} & F(q) &= \begin{bmatrix} \frac{\partial u_1}{\partial q_{11}} \\ \frac{\partial u_1}{\partial q_{21}} \\ \frac{\partial u_2}{\partial q_{12}} \\ \frac{\partial u_2}{\partial q_{22}} \end{bmatrix} \\
&& X &= \{ q_{ij} \;\text{satisfy constraints in individual problems}\}
\end{aligned}$$

This is all just a simple example based on 2 players, so now we move into the abstract world.

# When can the VI problem be represented as an optimization problem?

Recall the variational inequality problems

$$VI(F, \Omega) = \min_{x \in \Omega} \oint_0^x F(z) dz$$

Example: $\Omega \in \mathbb{R}^2$.

$$\begin{aligned}
F(x) &= \begin{bmatrix} x_1 + 2x_2 \\ x_1 + x_2 \end{bmatrix} \\
\oint_{(0,0)}^{(1,1)} F(z) dz
\end{aligned}$$

Let's consider two paths:

1. $(0,0) \to (0,1) \to (1,1)$
2. $(0,0) \to (1,0) \to (1,1)$

$$\begin{aligned}
\int_0^1 F_2(0, z_2) dz_2 + \in_0^1 F_1 (z_1, 1)dz_1 &= \int_0^1 z_2 dz_2 + \int_0^1 (z_1 + 2) dz_1 \\
&= \frac 1 2 + (\frac 1 2 + 2) \\
&= 3 \\
\int_0^1 F_1(z_1, 0) dz_1 + \int_0^1 F_2 (1, z_2)dz_2 &= \int_0^1 z_1 dz_1 + \int_0^1 (1 + z_2) dz_2 \\
&= \frac 1 2 + (1 + \frac 1 2) \\
&= 2
\end{aligned}$$

Note that because we do not arrive at the same answer for both we cannot simply take the line integral to solve the VI problem, which means that we cannot solve the VI problem as an optimization problem.

For a line integral to be path-independent, we should have $$\frac{\partial F_i}{\partial x_j} = \frac{\partial F_j}{\partial x_i} \;\;\forall i, j$$

*Definition.* The Jacobian matrix, $J(F) = JF = J_F$ is defined as

$$J(F) =
\begin{bmatrix}  
\frac{\partial F_1}{\partial x_1} & \frac{\partial F_1}{\partial x_2} & \cdots & \frac{\partial F_1}{\partial x_n} \\
\vdots & \ddots & \ddots & \vdots \\
\frac{\partial F_n}{\partial x_1} & \cdots & \cdots & \frac{\partial F_n}{\partial x_n}
\end{bmatrix}$$

If the Jacobian is symmetric, then the line integral is path-independent and we can rewrite the VI problem as an optimization problem.

Of course, we will not be so lucky.
Even in the previous game theory example, we will not be able to solve the VI problem as an optimization problem and we'll need to use some other algorithms.

# Diagonalization Algorithm

$$F(x^*)^T (x - x^*) \geq 0 \;\;\forall x \in X$$

In iteration $k$, we create $x^k$

$$F_i^k (x_i) = F_i (x_i, x_j = x_j^k \;\forall j \neq i)$$

Suppose $x^k = \begin{bmatrix} \frac 1 2 & \frac 1 3 \end{bmatrix}^T$, then

$$\begin{aligned}
F_1^k (x_1) &= x_1 + 2 \frac 1 3 \\
F_2^k (x_2) &= \frac 1 2 + x_2 \\
F^k &= \begin{bmatrix} x_1 \frac 2 3 \\ x_2 + \frac 1 2 \end{bmatrix} \Rightarrow J(F^k) = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}
\end{aligned}$$

Process: Iteration $k$, find $x^k$, solve $VI(F^k, \Omega)$

Solving $VI(F^k, \Omega)$ to continue the above example:

$$F^k = \begin{bmatrix} x_1 \frac 2 3 \\ x_2 + \frac 1 2 \end{bmatrix}
\to \int_{(0,0)}^{(x_1, x_2)} \begin{bmatrix} z_1 \frac 2 3 \\ z_2 + \frac 1 2 \end{bmatrix} \begin{bmatrix} dz_1 \\ dz_2 \end{bmatrix} \to \min \dots (\text{s.t. } x \in \Omega)$$
