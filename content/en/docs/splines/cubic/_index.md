+++
title = 'Cubic Splines'
weight = 4
+++

# Cubic Spline Interpolation

One of the methods of spline interpolation is cubic spline interpolation.

Let $S(x)$ be a cubic spline constructed on $n$ points $\left\{\left(x_i, y_i\right)\right\}_{i=1}^n$.\
$S(x)$ consists of $n-1$ segments $S_k(x)$, each of which is a third-degree polynomial.

The $k$-th segment of the cubic spline has the form:\
$S_k(x) = a_k + b_k(x-x_k) + c_k(x-x_k)^2 + d_k(x-x_k)^3 {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$.

The cubic spline takes values $y_i$ at each point $x_i$; moreover, it has continuous first and second derivatives.

### General Conditions for Cubic Splines:
1. $S_k(x_k) = y_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
2. $S_k(x_{k+1}) = y_{k+1} {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
3. $S_k'(x_{k+1}) = S_{k+1}'(x_{k+1}) {}_{, \ \forall k \in \left\{1,...,n-2\right\}}$
4. $S_k''(x_{k+1}) = S_{k+1}''(x_{k+1}) {}_{, \ \forall k \in \left\{1,...,n-2\right\}}$

Define the step sizes and differences between values at the nodes:
- $h_k = x_{k+1} - x_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
- $\delta_k = y_{k+1} - y_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$.

Rewriting the general conditions using coefficients:
1. $S_k(x_k) = y_k \Longleftrightarrow a_k = y_k$
2. $S_k(x_{k+1}) = y_{k+1} \Longleftrightarrow b_kh_k + c_kh_k^2 + d_kh_k^3 = \delta_k$
3. $S_k'(x_{k+1}) = S_{k+1}'(x_{k+1}) \Longleftrightarrow b_k + 2c_kh_k + 3d_kh_k^2 = b_{k+1}$
4. $S_k''(x_{k+1}) = S_{k+1}''(x_{k+1}) \Longleftrightarrow 2c_k + 6d_kh_k = 2c_{k+1}$ (can be divided by 2)

Introduce a dummy variable $c_n = 3d_{n-1}h_{n-1} + c_{n-1}$, which can be rewritten as $c_{n-1} + 3d_{n-1}h_{n-1} = c_n$, thus extending equality under point `4.` to $k = n - 1$.

As a result, we obtain:

$$
\boxed{
	a_k = y_k
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{1}
$$
$$
\boxed{
	b_kh_k + c_kh_k^2 + d_kh_k^3 = \delta_k
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{2}
$$
$$
\boxed{
	b_k + 2c_kh_k + 3d_kh_k^2 = b_{k+1}
}
{}_{, \ \forall k \in \left\{1,...,n-2\right\}}
\tag{3}
$$
$$
\boxed{
	c_k + 3d_kh_k = c_{k+1}
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{4}
$$

Now, let's derive the equalities that will help us express some coefficients in terms of others:

from (4):
$$
\boxed{
	d_k = \frac{c_{k+1} - c_k}{3h_k}
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{5}
$$

From (2), (5):\
$\frac{c_{k+1} - c_k}{3h_k}h_k^3 + c_kh_k^2 + b_kh_k = \delta_k$\
, from which we get:
$$
\boxed{
	b_k = \frac{\delta_k}{h_k} - h_k\frac{2c_k + c_{k+1}}{3}
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{6}
$$

From (3), (5):\
$3\frac{c_{k+1} - c_k}{3h_k}h_k^2 + 2c_kh_k + b_k = b_{k+1}$\
$h_k(c_k + c_{k+1}) + b_k = b_{k+1}$

Then, using (6), we can derive the following equality:

<details>
<summary>Intermediate expressions</summary>

$h_k(c_k + c_{k+1}) + \frac{\delta_k}{h_k} - h_k\frac{2c_k + c_{k+1}}3 = \frac{\delta_{k+1}}{h_{k+1}} - h_{k+1}\frac{2c_{k+1} + c_{k+2}}3$

$h_k(c_k + c_{k+1}) - h_k\frac{2c_k + c_{k+1}}3 = \frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k} - h_{k+1}\frac{2c_{k+1} + c_{k+2}}3$

$3h_kc_k + 3h_kc_{k+1} - 2h_kc_k - h_kc_{k+1} + 2h_{k+1}c_{k+1} + h_{k+1}c_{k+2} = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$

$h_kc_k + 2h_kc_{k+1} + 2h_{k+1}c_{k+1} + h_{k+1}c_{k+2} = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$
</details>

$$
\boxed{
	c_k(h_k) + c_{k+1}(2h_k + 2h_{k+1}) + c_{k+2}(h_{k+1})
	= 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)
}
{}_{, \ \forall k \in \left\{1,...,n-2\right\}}
\tag{7}
$$

Thus, we have obtained $(n)$ variables $c_k$ (among them one dummy variable --- $c_n$) and $(n-2)$ equations for their determination (one of which was obtained using the dummy variable).

At this point, we can create an incomplete tridiagonal matrix representing the system of linear equations for finding the values of the variables $c_k$:

$$
\begin{bmatrix}
	\boxed{?} & \boxed{?} & 0 & 0 & \dots & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & 0 \\
	0 & h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & \boxed{?} & \boxed{?}
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ c_3 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	\boxed{?} \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ \boxed{?}
\end{bmatrix}
\tag{8}
$$
where $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$.

As seen, to form a complete tridiagonal matrix, we need two more equations.\
Thus, for the unambiguous determination of the coefficients, two additional conditions are required.

### Additional Conditions

#### I. Natural Spline

A natural cubic spline is a spline for which the second derivative is zero at the endpoints.\
It is a special case of the "Fixed-second" spline.

Conditions: $S_1''(x_1) = 0, \ S_{n-1}''(x_n) = 0$.

Equations:
- $c_1 = 0$
- $c_n = 0$

Matrix:

$$
\begin{bmatrix}
	1 & 0 & 0 & \dots & 0 & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & \dots & 0 & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	0 \\ R_1 \\ \vdots \\ R_{n-2} \\ 0
\end{bmatrix}
$$

[More about the natural spline.](natural.md)

#### II. Not-a-knot Spline

A "Not-a-knot" cubic spline is a spline where the third derivative is continuous at the second and penultimate points. This means that the third derivative is equal at the first and second segments, as well as at the penultimate and last segments.

Conditions: $S_1'''(x_2) = S_2'''(x_2), \ S_{n-2}'''(x_{n-1}) = S_{n-1}'''(x_{n-1})$.

Equations:
- $(h_1-h_2)c_1 + (2h_1+h_2)c_2 = 3\frac{h_1}{h_1+h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)$
- $(h_{n-2}+2h_{n-1})c_{n-1} + (-h_{n-2}+h_{n-1})c_n = 3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$

Matrix:

$$
\begin{bmatrix}
	h_1 - h_2 & 2h_1 + h_2 & 0 & \dots & 0 & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & \dots & 0 & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & h_{n-2} + 2h_{n-1} & -h_{n-2} + h_{n-1}
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	R_0 \\ R_1 \\ \vdots \\ R_{n-2} \\ R_{n-1}
\end{bmatrix}
$$
where $R_0 = 3\frac{h_1}{h_1+h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, $R_{n-1} = 3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$.

[More about the "Not-a-knot" spline.](not-a-knot.md)

#### III. Periodic Spline

A periodic cubic spline is a spline whose first and second derivatives are equal at the endpoints.

Conditions: $S_1'(x_1) = S_{n-1}'(x_n), \ S_1''(x_1) = S_{n-1}''(x_n)$.

Matrix (in this case, not tridiagonal):

$$
\begin{bmatrix}
	2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & 0 & h_1 \\
	h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	h_1 & 0 & 0 & \dots & 0 & h_{n-1} & 2h_{n-1} + 2h_1
\end{bmatrix}
\begin{bmatrix}
	c_2 \\ c_3 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ R_{n-1}
\end{bmatrix}
$$
where $c_n = c_1$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, and $R_{n-1} = 3\left(\frac{\delta_1}{h_1} - \frac{\delta_{n-1}}{h_{n-1}}\right)$.

[More about the periodic spline.](periodic.md)

#### IV. Parabolic-ends

"Parabolic-ends" cubic spline is a spline where the boundary segments are quadratic curves or parabolas.\
It is a special case of the "Fixed-third" spline, where the third derivatives at the ends are set to zero.

Conditions: $S_1'''(x_1) = 0, \ S_{n-1}'''(x_n) = 0$.

Equations:
- $c_1 - c_2 = 0$
- $-c_{n-1} + c_n = 0$

Matrix:

$$
\begin{bmatrix}
	1 & -1 & 0 & \dots & 0 & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & \dots & 0 & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & -1 & 1
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	0 \\ R_1 \\ \vdots \\ R_{n-2} \\ 0
\end{bmatrix}
$$

Special case: $n = 2$:
- $c_1 = 0$
- $c_2 = 0$

[More about the "Parabolic-ends" spline.](parabolic-ends.md)

#### V. Clamped Spline

A clamped cubic spline is a spline with fixed first derivatives at the endpoints.

Conditions: $S_1'(x_1) = f'(x_1), \ S_{n-1}'(x_n) = f'(x_n)$.

Equations:
- $2h_1c_1 + h_1c_2 = 3\left(\frac{\delta_1}{h_1} - f'(x_1)\right)$
- $h_{n-1}c_{n-1} + 2h_{n-1}c_n = 3\left(f'(x_n) - \frac{\delta_{n-1}}{h_{n-1}}\right)$

Matrix:

$$
\begin{bmatrix}
	2h_1 & h_1 & 0 & \dots & 0 & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & \dots & 0 & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & h_{n-1} & 2h_{n-1}
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	R_0 \\ R_1 \\ \vdots \\ R_{n-2} \\ R_{n-1}
\end{bmatrix}
$$
where $R_0 = 3\left(\frac{\delta_1}{h_1} - f'(x_1)\right)$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, and $R_{n-1} = 3\left(f'(x_n) - \frac{\delta_{n-1}}{h_{n-1}}\right)$.

[More about the clamped spline.](clamped.md)

#### VI. Fixed-second Spline

A "Fixed-second" cubic spline is a spline with fixed second derivatives at the endpoints.\
A special case is the natural spline, where the second derivatives at the endpoints are set to zero.

Conditions: $S_1''(x_1) = f''(x_1), \ S_{n-1}''(x_n) = f''(x_n)$.

Equations:
1. $c_1 = \frac{f''(x_1)}{2}$
2. $c_n = \frac{f''(x_n)}{2}$

Matrix:

$$
\begin{bmatrix}
	1 & 0 & 0 & \dots & 0 & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & \dots & 0 & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	f''(x_1)/2 \\ R_1 \\ \vdots \\ R_{n-2} \\ f''(x_n)/2
\end{bmatrix}
$$

[More about the "Fixed-second" spline.](fixed-second.md)

#### VII. Fixed-third Spline

A "Fixed-third" cubic spline is a spline with fixed third derivatives at the endpoints.\
A special case is the "Parabolic-ends" spline, where the third derivatives at the endpoints are set to zero.

Conditions: $S_1'''(x_1) = f'''(x_1), \ S_{n-1}'''(x_n) = f'''(x_n)$.

Equations:
- $c_1 - c_2 = -\frac{h_1f'''(x_1)}{2}$
- $-c_{n-1} + c_n = \frac{h_{n-1}f'''(x_n)}{2}$

Matrix:

$$
\begin{bmatrix}
	1 & -1 & 0 & \dots & 0 & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & \dots & 0 & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & -1 & 1
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	-h_1f'''(x_1)/2 \\ R_1 \\ \vdots \\ R_{n-2} \\ h_{n-1}f'''(x_n)/2
\end{bmatrix}
$$

Special case: $n = 2$:
- $c_1 = -\frac{h_1\left(f'''(x_1) + f'''(x_2)\right)}{8}$
- $c_2 = -c_1$

[More about the "Fixed-third" spline.](fixed-third.md)

### Arbitrary Conditions

We can set two arbitrary conditions for two given points.

In this case, we can construct a "sub-spline", whose initial and final points are these two points.\
Note: there may be subtleties for Fixed-third conditions, for which segments are specified, and for Not-a-knot conditions, for which the second and penultimate points are specified.

At these points the necessary equations can be set, corresponding to the conditions for the first or last point (see the variants described above).

Next we can iteratively construct the preceding and subsequent segments, extending the sub-spline to the ends of the spline.

Below are the formulas for the iterative calculation of the coefficients of the $k$-th segment, given the known coefficients of the $(k+1)$-th or $(k-1)$-th segment.

#### Formulas for Iterative Construction

Given: $a_{k+1}, b_{k+1}, c_{k+1}, d_{k+1}$. Derive $a_k, b_k, c_k, d_k$. $_{k \in \left\{1,...,n-2\right\}}$.

1. $d_k = \frac{c_{k+1} - \frac{b_{k+1}}{h_k} + \frac{\delta_k}{h_k^2}}{h_k}$.
2. $c_k = c_{k+1} - 3d_kh_k$.
3. $b_k = \frac{\delta_k}{h_k} - d_kh_k^2 - c_kh_k$.
4. $a_k = y_k$.

Given: $a_{k-1}, b_{k-1}, c_{k-1}$. Derive $a_k, b_k, c_k$. $_{k \in \left\{2,...,n-1\right\}}$.

1. $a_k = y_k$.
2. $b_k = 3d_{k-1}h_{k-1}^2 + 2c_{k-1}h_{k-1} + b_{k-1}$.
3. $c_k = 3d_{k-1}h_{k-1} + c_{k-1}$.
4. $d_k = \frac{\frac{\delta_k}{h_k^2} - c_k - \frac{b_k}{h_k}}{h_k}$.

#### Notes

**1. "Clamped" and "Fixed-second" Conditions at a Single Point**

The general scheme does not cover the case where both "Clamped" and "Fixed-second" conditions are specified at a single point.

Let's derive the coefficients separately for this case.

Let at point $x_k$ the first derivative $f'$ and the second derivative $f''$ be specified.

Coefficients for the previous ($k-1$-th) segment:
- $a_{k-1} = y_{k-1}$
- $b_{k-1} = \frac{3\delta_{k-1}}{h_{k-1}} + \frac{f''h_{k-1}}{2} - 2f'$
- $c_{k-1} = \frac{3f'}{h_{k-1}} - \frac{3\delta_{k-1}}{h_{k-1}^2} - f''$
- $d_{k-1} = \frac{f''}{2h_{k-1}} - \frac{f'}{h_{k-1}^2} + \frac{\delta_{k-1}}{h_{k-1}^3}$

Coefficients for the current ($k$-th) segment:
- $a_k = y_k$
- $b_k = f'$
- $c_k = \frac{f''}{2}$
- $d_k = \frac{\delta_k}{h_k^3} - \frac{f'}{h_k^2} - \frac{f''}{2h_k}$

**2. "Fixed-second" and "Not-a-knot" Conditions at a Single Point**

Coefficients for the $k-1$-th and $k$-th segments:
- $a_{k-1} = y_{k-1}$
- $a_k = y_k$
- $c_k = \frac{f''(x_k)}{2}$
- $c_{k-1} = \frac{f'' - 6dh_{k-1}}{2}$
- $b_{k-1} = \frac{\delta_{k-1}}{h_{k-1}} - \frac{f''h_{k-1}}{2} + 2dh_{k-1}^2$
- $b_k = \frac{\delta_{k-1}}{h_{k-1}} + \frac{f''h_{k-1}}{2} - dh_{k-1}^2$
- $d_{k-1} = d_k = d = \frac{\frac{\delta_k}{h_k} - \frac{\delta_{k-1}}{h_{k-1}} - \frac{f''(x_k)}{2}h_{k-1} - \frac{f''(x_k)}{2}h_k}{h_k^2 - h_{k-1}^2}$

As we can see, to compute the coefficients, we need to perform division by the expression $h_k^2 - h_{k-1}^2$, which equals zero if the steps $h_{k-1}$ and $h_k$ are equal.

Therefore, in particular, when interpolating using uniformly spaced points, it is **impossible** to set these two conditions at a single point.