+++
title = 'Natural'
weight = 1
+++

A natural cubic spline is a spline where the second derivative is zero at the endpoints.

It is a special case of the ["Fixed-second" spline](fixed-second.md).

Conditions: $S_1''(x_1) = 0, \ S_{n-1}''(x_n) = 0$.

From these conditions, the following expressions for the coefficients are obtained:
1. $2c_1 + 6d_1 \cdot 0 = 0 \Longrightarrow c_1 = 0$
2. $2c_{n-1} + 6d_{n-1}h_{n-1} = 0 \Longrightarrow c_n = 0$ (let's recall our dummy variable $c_n$: the left part is equal to $2c_n$)

Thus, we obtain two missing equations for the matrix:
1. $c_1 = 0$
2. $c_n = 0$

We place them into the matrix:

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
	0 \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ 0
\end{bmatrix}
$$
where $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$.

Now the matrix can be solved using the [tridiagonal matrix algorithm](https://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm).

After finding the coefficients $c_k$, the other coefficients $b_k$ and $d_k$ can be calculated using formulas (6) and (5) respectively.