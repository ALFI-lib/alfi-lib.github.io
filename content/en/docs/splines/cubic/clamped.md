+++
title = 'Clamped'
weight = 5
+++

A "Clamped" cubic spline is a spline where the first derivatives at the endpoints are fixed.

Conditions: $S_1'(x_1) = f'(x_1), \ S_{n-1}'(x_n) = f'(x_n)$.

From these conditions, the following expressions for the coefficients are obtained:
$$
\boxed {
	b_1 = f'(x_1)
}
\tag{V.1}
$$
$$
\boxed {
	b_{n-1} + 2c_{n-1}h_{n-1} + 3d_{n-1}h_{n-1}^2 = f'(x_n)
}
\tag{V.2}
$$

From (6) and (V.1):

<details>
<summary>Intermediate expressions</summary>

$\frac{\delta_1}{h_1} - h_1\frac{2c_1 + c_2}3 = f'(x_1)$\
$\frac{3\delta_1}{h_1^2} - 2c_1 - c_2 = \frac{3f'(x_1)}{h_1}$\
$2c_1 + c_2 = \frac{3\delta_1}{h_1^2} - \frac{3f'(x_1)}{h_1}$
</details>

$$
\boxed{
	2h_1c_1 + h_1c_2 = 3\left(\frac{\delta_1}{h_1} - f'(x_1)\right)
}
\tag{V.3}
$$

From (5), (6), and (V.2):

<details>
<summary>Intermediate expressions</summary>

$\left(\frac{\delta_{n-1}}{h_{n-1}} - h_{n-1}\frac{2c_{n-1} + c_n}{3}\right) + 2c_{n-1}h_{n-1} + 3\left(\frac{c_n - c_{n-1}}{3h_{n-1}}\right)h_{n-1}^2 = f'(x_n)$\
$\frac{\delta_{n-1}}{h_{n-1}} - h_{n-1}\frac{2c_{n-1} + c_n}{3} + 2c_{n-1}h_{n-1} + (c_n - c_{n-1})h_{n-1} = f'(x_n)$\
$-h_{n-1}(2c_{n-1} + c_n) + 6c_{n-1}h_{n-1} + 3(c_n - c_{n-1})h_{n-1} = 3\left(f'(x_n) - \frac{\delta_{n-1}}{h_{n-1}}\right)$\
$-2h_{n-1}c_{n-1} - h_{n-1}c_n + 6h_{n-1}c_{n-1} + 3h_{n-1}c_n - 3h_{n-1}c_{n-1} = 3\left(f'(x_n) - \frac{\delta_{n-1}}{h_{n-1}}\right)$
</details>

$$
\boxed{
	h_{n-1}c_{n-1} + 2h_{n-1}c_n = 3\left(f'(x_n) - \frac{\delta_{n-1}}{h_{n-1}}\right)
}
\tag{V.4}
$$

Now, the equations (V.3) and (V.4) are entered into the matrix:

$$
\begin{bmatrix}
	2h_1 & h_1 & 0 & 0 & \dots & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & 0 \\
	0 & h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & h_{n-1} & 2h_{n-1}
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ c_3 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	R_0 \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ R_{n-1}
\end{bmatrix}
$$
where $R_0 = 3\left(\frac{\delta_1}{h_1} - f'(x_1)\right)$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, $R_n = 3\left(f'(x_n) - \frac{\delta_{n-1}}{h_{n-1}}\right)$.

The matrix can now be solved using the [tridiagonal matrix algorithm](https://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm).

After finding the coefficients $c_k$, the other coefficients $b_k$ and $d_k$ can be computed using formulas (6) and (5) respectively.