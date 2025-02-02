+++
title = 'Fixed-third'
weight = 7
+++

A "Fixed-third" cubic spline is a spline where the third derivatives at the endpoints are fixed. A special case is the "Parabolic-ends" spline, where the third derivatives at the endpoints are set to zero.

Conditions: $S_1'''(x_1) = f'''(x_1), \ S_{n-1}'''(x_n) = f'''(x_n)$.

From these conditions, the following expressions for the coefficients are obtained:
1. $6d_1 = f'''(x_1)$
2. $6d_{n-1} = f'''(x_n)$

Thus:

$$
\boxed {
	d_1 = \frac{f'''(x_1)}{6}
}
\tag{IV.1}
$$
$$
\boxed {
	d_{n-1} = \frac{f'''(x_n)}{6}
}
\tag{IV.2}
$$

From (5) and (VI.1):

$$
\boxed{
	c_1 - c_2 = -\frac{h_1f'''(x_1)}{2}
}
\tag{IV.3}
$$

From (VI.2) and $d_{n-1} = \frac{c_n - c_{n-1}}{3h_{n-1}}$, we get:

$$
\boxed{
	-c_{n-1} + c_n = \frac{h_{n-1}f'''(x_n)}{2}
}
\tag{IV.4}
$$

Thus, we obtain two missing equations for the matrix:
1. $c_1 - c_2 = -\frac{h_1f'''(x_1)}{2}$
2. $-c_{n-1} + c_n = \frac{h_{n-1}f'''(x_n)}{2}$

We insert them into the matrix:

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
	-h_1f'''(x_1)/2 \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ h_{n-1}f'''(x_n)/2
\end{bmatrix}
$$
where $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$.

Now the matrix can be solved using the [tridiagonal matrix algorithm](https://ru.wikipedia.org/wiki/Метод_прогонки).

After finding the coefficients $c_k$, the other coefficients $b_k$ and $d_k$ can be computed using formulas (6) and (5) respectively.

### Special case: $n = 2$.

In the case where there are only two points (and therefore just one segment), the equations become linearly dependent:

$$
\begin{cases}
	c_1 - c_2 = -\frac{h_1f'''(x_1)}{2} \\
	-c_1 + c_2 = \frac{h_1f'''(x_n)}{2}
\end{cases}
\Rightarrow
\begin{cases}
	c_1 - c_2 = -\frac{h_1f'''(x_1)}{2} \\
	c_1 - c_2 = -\frac{h_1f'''(x_n)}{2}
\end{cases}
$$

Thus, if the third derivatives at the endpoints are not equal, we get two contradictory equations. However, if they are equal, we are left with only one equation instead of two.

To resolve this situation, we take the arithmetic mean of the third derivatives at each node and set the modules of $c_1$ and $c_2$ (the fictitious one) equal. 

Then we get the following expressions:
- $c_1 = -\frac{h_1\left(f'''(x_1) + f'''(x_2)\right)}{8}$
- $c_2 = -c_1$