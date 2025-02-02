+++
title = 'Parabolic-ends'
weight = 4
+++

A "Parabolic-ends" cubic spline is a spline whose end segments are second-degree curves or parabolas.\
This spline is a special case of the "Fixed-third" spline, where the third derivatives at the endpoints are set to zero.

Conditions: $S_1'''(x_1) = 0, \ S_{n-1}'''(x_n) = 0$.

From these conditions, the following expressions for the coefficients are obtained:
1. $6d_1 = 0$
2. $6d_{n-1} = 0$

Thus:

$$
\boxed {
	d_1 = 0
}
\tag{IV.1}
$$
$$
\boxed {
	d_{n-1} = 0
}
\tag{IV.2}
$$

From (5), (VI.1):

$$
\boxed{
	c_1 - c_2 = 0
}
\tag{IV.3}
$$

From (5), (VI.2):

$$
\boxed{
	-c_{n-1} + c_n = 0
}
\tag{IV.4}
$$

Thus, we obtain two missing equations for the matrix:
1. $c_1 - c_2 = 0$
2. $-c_{n-1} + c_n = 0$

These are entered into the matrix:

$$
\begin{bmatrix}
	1 & -1 & 0 & 0 & \dots & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & 0 \\
	0 & h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & -1 & 1
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ c_3 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	0 \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ 0
\end{bmatrix}
$$
where $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$.

The matrix can now be solved using the [tridiagonal matrix algorithm](https://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm).

After finding the coefficients $c_k$, the other coefficients $b_k$ and $d_k$ can be computed using formulas (6) and (5) respectively.

### Special case: $n = 2$.

In the case where there are two points (and therefore only one segment), the equations become identical:

$$
\begin{cases}
	c_1 - c_2 = 0 \\
	-c_1 + c_2 = 0
\end{cases}
\Rightarrow
\begin{cases}
	c_1 - c_2 = 0 \\
	c_1 - c_2 = 0
\end{cases}
$$

Thus, we get only one equation instead of two.

To resolve this situation, we equate the magnitudes of $c_1$ and $c_2$ (which is fictitious).

Then $c_1$ and $c_2$ will be equal to zero.