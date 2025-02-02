+++
title = 'Fixed-second'
weight = 6
+++

A "Fixed-second" cubic spline is a spline where the second derivatives at the endpoints are fixed.

A special case of the "Fixed-second" spline is the [natural spline](natural.md), where the second derivatives at the endpoints are set to zero.

Conditions: $S_1''(x_1) = f''(x_1), \ S_{n-1}''(x_n) = f''(x_n)$.

From these conditions, the following expressions for the coefficients are obtained:
1. $2c_1 + 6d_1 \cdot 0 = f''(x_1) \Longrightarrow c_1 = \frac{f''(x_1)}{2}$
2. $2c_{n-1} + 6d_{n-1}h_{n-1} = 0 \Longrightarrow c_n = \frac{f''(x_n)}{2}$ (recall our fictitious variable $c_n$: the left part is equal to $2c_n$)

Thus, we obtain the two missing equations for the matrix:
1. $c_1 = \frac{f''(x_1)}{2}$
2. $c_n = \frac{f''(x_n)}{2}$

We now incorporate these into the matrix:

$$
\begin{bmatrix}
	1 & 0 & 0 & 0 & \dots & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & 0 \\
	0 & h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ c_3 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	f''(x_1)/2 \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ f''(x_n)/2
\end{bmatrix}
$$
where $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$.

Now, the matrix can be solved using the [tridiagonal matrix algorithm](https://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm).

After finding the coefficients $c_k$, the other coefficients $b_k$ and $d_k$ can be computed using formulas (6) and (5) respectively.