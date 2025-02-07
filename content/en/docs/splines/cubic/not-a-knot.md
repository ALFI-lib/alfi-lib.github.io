+++
title = 'Not-a-knot'
weight = 2
+++

The "Not-a-knot" cubic spline is a spline where the third derivative is continuous at the second and second-to-last points. In other words, the third derivative is equal on the first and second segments, as well as on the second-to-last and last segments.

Conditions: $S_1'''(x_2) = S_2'''(x_2), \ S_{n-2}'''(x_{n-1}) = S_{n-1}'''(x_{n-1})$.

From these conditions, the following expressions for the coefficients are obtained:
1. $6d_1 = 6d_2 \Longrightarrow d_1 = d_2$
2. $6d_{n-2} = 6d_{n-1} \Longrightarrow d_{n-2} = d_{n-1}$

From equation (5), we obtain:
1. $\frac{c_2 - c_1}{3h_1} = \frac{c_3 - c_2}{3h_2} \Longrightarrow h_2c_2 - h_2c_1 = h_1c_3 - h_1c_2$
2. $\frac{c_{n-1} - c_{n-2}}{3h_{n-2}} = \frac{c_n - c_{n-1}}{3h_{n-1}} \Longrightarrow h_{n-1}c_{n-1} - h_{n-1}c_{n-2} = h_{n-2}c_n - h_{n-2}c_{n-1}$

, from which we obtain the two equations:
$$
\boxed{
	h_2c_1 + (-h_2 - h_1)c_2 + h_1c_3 = 0
}
\tag{II.1}
$$
$$
\boxed{
	h_{n-1}c_{n-2} + (-h_{n-1} - h_{n-2})c_{n-1} + h_{n-2}c_n = 0
}
\tag{II.2}
$$

From (7) for $k = 1$ we obtain:\
$c_1(h_1) + c_2(2h_1 + 2h_2) + c_3(h_2) = 3\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)$

We subtract this equation, multiplied by $\frac{h_1}{h_2}$, from (II.1) to eliminate the coefficient in front of $c_3$:\
$c_1\left(h_2 - \frac{h_1^2}{h_2}\right) + c_2\left(-h_2 - h_1 - 2\frac{h_1^2}{h_2} - 2h_1\right) = -3\frac{h_1}{h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)$

Factoring out the common multiplier from the coefficients:\
$c_1\left(-\frac{h_1+h_2}{h_2}\right)(h_1-h_2) + c_2\left(-\frac{h_1+h_2}{h_2}\right)(2h_1+h_2) = \left(-\frac{h_1+h_2}{h_2}\right)\left(3\frac{h_1}{h_1+h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)\right)$

And canceling out by $\left(-\frac{h_1+h_2}{h_2}\right)$:
$$
\boxed{
	(h_1-h_2)c_1 + (2h_1+h_2)c_2 = 3\frac{h_1}{h_1+h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)
}
\tag{II.3}
$$

Similarly, we obtain the formula for the last row of the matrix:

<details>
<summary>Details</summary>

From (7) for $k = n-2$ we obtain:\
$c_{n-2}(h_{n-2}) + c_{n-1}(2h_{n-2} + 2h_{n-1}) + c_n(h_{n-1}) = 3\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$

We subtract this equation, multiplied by $\frac{h_{n-1}}{h_{n-2}}$, from (II.2) to eliminate the coefficient in front of $c_{n-2}$:\
$c_{n-1}\left(-h_{n-1} - h_{n-2} - 2\frac{h_{n-1}^2}{h_{n-2}} - 2h_{n-1}\right) + c_n\left(h_{n-2} - \frac{h_{n-1}^2}{h_{n-2}}\right) = -3\frac{h_{n-1}}{h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$

Factoring out the common multiplier from the coefficients:\
$c_{n-1}\left(-\frac{h_{n-1}+h_{n-2}}{h_{n-2}}\right)(2h_{n-1}+h_{n-2}) + c_n\left(-\frac{h_{n-1}+h_{n-2}}{h_{n-2}}\right)(h_{n-1}-h_{n-2}) = \left(-\frac{h_{n-1}+h_{n-2}}{h_{n-2}}\right)\left(3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)\right)$

And canceling out by $\left(-\frac{h_{n-1}+h_{n-2}}{h_{n-2}}\right)$:\
$c_{n-1}(2h_{n-1}+h_{n-2}) + c_n(h_{n-1}-h_{n-2}) = 3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$
</details>

$$
\boxed{
	c_{n-1}(h_{n-2}+2h_{n-1}) + c_n(-h_{n-2}+h_{n-1}) = 3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)
}
\tag{II.4}
$$

Now, we place equations (II.3) and (II.4) into the matrix:

$$
\begin{bmatrix}
	h_1 - h_2 & 2h_1 + h_2 & 0 & 0 & \dots & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & 0 \\
	0 & h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & h_{n-2} + 2h_{n-2} & -h_{n-2} + h_{n-1}
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ c_3 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	R_0 \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ R_{n-1}
\end{bmatrix}
$$
where $R_0 = 3\frac{h_1}{h_1+h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, $R_{n-1} = 3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$.

Now the matrix can be solved using the [tridiagonal matrix algorithm](https://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm).

After finding the coefficients $c_k$, the other coefficients $b_k$ and $d_k$ can be calculated using formulas (6) and (5) respectively.