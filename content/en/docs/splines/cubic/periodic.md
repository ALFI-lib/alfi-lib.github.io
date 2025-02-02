+++
title = 'Periodic'
weight = 3
+++

A periodic cubic spline is a spline where the first and second derivatives are equal at the endpoints.

Conditions: $S_1'(x_1) = S_{n-1}'(x_n), \ S_1''(x_1) = S_{n-1}''(x_n)$.

From these conditions, the following expressions for the coefficients are obtained:
1. $b_{n-1} + 2c_{n-1}h_{n-1} + 3d_{n-1}h_{n-1}^2 = b_1$
2. $c_{n-1} + 3d_{n-1}h_{n-1} = c_1$

By performing some manipulations, we obtain the matrix:

$$
\begin{bmatrix}
	2h_1 + 2h_2 & h_2 & 0 & 0 & \dots & 0 & h_1 \\
	h_2 & 2h_2 + 2h_3 & h_3 & 0 & \dots & 0 & 0 \\
	0 & h_3 & 2h_3 + 2h_4 & h_4 & \dots & 0 & 0 \\
	\vdots & \vdots & \ddots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & \dots & h_{n-3} & 2h_{n-3} + 2h_{n-2} & h_{n-2} & 0 \\
	0 & 0 & \dots & 0 & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	h_1 & 0 & \dots & 0 & 0 & h_{n-1} & 2h_{n-1} + 2h_1
\end{bmatrix}
\begin{bmatrix}
	c_2 \\ c_3 \\ c_4 \\ \vdots \\ c_{n-2} \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	R_1 \\ R_2 \\ R_3 \\ \vdots \\ R_{n-3} \\ R_{n-2} \\ R_{n-1}
\end{bmatrix}
$$
where $c_n = c_1$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, and $R_{n-1} = 3\left(\frac{\delta_1}{h_1} - \frac{\delta_{n-1}}{h_{n-1}}\right)$.

This is not a tridiagonal matrix, so it cannot be solved using the [tridiagonal matrix algorithm](https://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm).\
However, it can be solved using a modified method.

After finding the coefficients $c_k$, the other coefficients $b_k$ and $d_k$ can be calculated using formulas (6) and (5) respectively.