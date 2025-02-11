+++
title = 'Quadratic Splines'
weight = 3
+++

# Quadratic Spline Interpolation

One of the methods of spline interpolation is quadratic spline interpolation.

Let $S(x)$ be a quadratic spline constructed on $n$ points $\left\{\left(x_i, y_i\right)\right\}_{i=1}^n$.\
$S(x)$ consists of $n-1$ segments $S_k(x)$, each of which is a second-degree polynomial.

The $k$-th segment of the quadratic spline is given by:\
$S_k(x) = a_k + b_k(x-x_k) + c_k(x-x_k)^2 {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$.

The quadratic spline takes the values $y_i$ at each point $x_i$; it also has a continuous first derivative.

### General Conditions for Quadratic Splines:
1. $S_k(x_k) = y_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
2. $S_k(x_{k+1}) = y_{k+1} {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
3. $S_k'(x_{k+1}) = S_{k+1}'(x_{k+1}) {}_{, \ \forall k \in \left\{1,...,n-2\right\}}$

Let us denote the steps between the nodes and the values at the nodes:
- $h_k = x_{k+1} - x_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
- $\delta_k = y_{k+1} - y_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$.

We now express the general conditions in terms of the coefficients:
1. $S_k(x_k) = y_k \Longleftrightarrow a_k = y_k$
2. $S_k(x_{k+1}) = y_{k+1} \Longleftrightarrow b_kh_k + c_kh_k^2 = \delta_k$
3. $S_k'(x_{k+1}) = S_{k+1}'(x_{k+1}) \Longleftrightarrow b_k + 2c_kh_k = b_{k+1}$

From the formulas obtained, several useful formulas for expressing coefficients can be derived:

From the first list item:

$$
\boxed{
	a_k = y_k
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{1}
$$

From the second list item:

$$
\boxed{
	b_k = \frac{\delta_k - c_kh_k^2}{h_k} = \frac{\delta_k}{h_k} - c_kh_k
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{2}
$$
$$
\boxed{
	c_k = \frac{\delta_k - b_kh_k}{h_k^2} = \frac{\frac{\delta_k}{h_k} - b_k}{h_k} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{3}
$$

From the third list item:

$$
\boxed{
	b_k = b_{k+1} - 2c_kh_k
}
{}_{, \ \forall k \in \left\{1,...,n-2\right\}}
\tag{4}
$$
$$
\boxed{
	b_{k+1} = b_k + 2c_kh_k
}
{}_{, \ \forall k \in \left\{1,...,n-2\right\}}
\tag{5}
$$
$$
\boxed{
	c_k = \frac{b_{k+1} - b_k}{2h_k}
}
{}_{, \ \forall k \in \left\{1,...,n-2\right\}}
\tag{6}
$$

From (2), (4):\
$\frac{\delta_k - c_kh_k^2}{h_k} = b_{k+1} - 2c_kh_k$\
$\delta_k - c_kh_k^2 = b_{k+1}h_k - 2c_kh_k^2$\
$c_kh_k^2 = b_{k+1}h_k - \delta_k$

$$
\boxed{
	c_k = \frac{b_{k+1}h_k - \delta_k}{h_k^2} = \frac{b_{k+1} - \frac{\delta_k}{h_k}}{h_k} = \frac{b_{k+1}}{h_k} - \frac{\delta_k}{h_k^2}
}
{}_{, \ \forall k \in \left\{1,...,n-2\right\}}
\tag{7}
$$

From (3), (6):\
$\frac{\delta_k}{h_k^2} - \frac{b_k}{h_k} = \frac{b_{k+1} - b_k}{2h_k}$\
$2\frac{\delta_k}{h_k} - 2b_k = b_{k+1} - b_k$\
$b_k + b_{k+1} = 2\frac{\delta_k}{h_k}$

$$
\boxed{
	b_k + b_{k+1} = 2\frac{\delta_k}{h_k}
}
{}_{, \ \forall k \in \left\{1,...,n-2\right\}}
\tag{8}
$$

#### Formulas for Iterative Construction

Let us derive the formulas for computing the next segment given the known coefficients for the previous one:

Given: $a_k, b_k, c_k$. Derive $a_{k+1}, b_{k+1}, c_{k+1}$. $_{k \in \left\{1,...,n-2\right\}}$.

1. $a_{k+1}$: From (1): $a_{k+1} = y_{k+1}$.
2. $b_{k+1}$: Several ways:
	- From (5): $b_{k+1} = b_k + 2c_kh_k$.
	- From (7): $b_{k+1} = c_kh_k + \frac{\delta_k}{h_k}$.
	- From (8): $b_{k+1} = 2\frac{\delta_k}{h_k} - b_k$.
3. $c_{k+1}$: From (3): $c_k = \frac{\delta_k - b_kh_k}{h_k^2} = \frac{\frac{\delta_k}{h_k} - b_k}{h_k} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}$.

Let us now derive the formulas for computing the previous segment given the known coefficients of the next segment:

Given: $a_{k+1}, b_{k+1}, c_{k+1}$. Derive $a_k, b_k, c_k$. $_{k \in \left\{1,...,n-2\right\}}$.

1. $a_k$: From (1): $a_k = y_k$.
2. $b_k$: From (8): $b_k = 2\frac{\delta_k}{h_k} - b_{k+1}$.
3. $c_k$: Several ways:
	- From (3): $c_k = \frac{\delta_k - b_kh_k}{h_k^2} = \frac{\frac{\delta_k}{h_k} - b_k}{h_k} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}$.
	- From (6): $c_k = \frac{b_{k+1} - b_k}{2h_k}$.
	- From (7): $c_k = \frac{b_{k+1}h_k - \delta_k}{h_k^2} = \frac{b_{k+1} - \frac{\delta_k}{h_k}}{h_k} = \frac{b_{k+1}}{h_k} - \frac{\delta_k}{h_k^2}$.

Thus, if we compute the coefficients for one segment, we can construct all the other segments.

Since the spline has $3(n-1)$ coefficients, and we have $2(n-1) + (n-2) = 3(n-1)-1$ equations, we need one more equation to uniquely determine the spline coefficients.

With this last equation, we will be able to compute the coefficients for one spline segment, after which we can iteratively compute the coefficients for all subsequent and previous segments.

To obtain the last equation, an additional condition is required.

### Additional Conditions

#### I. Not-a-knot-start

A special case of ["Not-a-knot (with index)"](./#xvi-not-a-knot-with-index) for the second point ($k = 2$).

#### II. Not-a-knot-end

A special case of ["Not-a-knot (with index)"](./#xvi-not-a-knot-with-index) for the penultimate point ($k = n - 1$).

#### III. Semi-not-a-knot

The arithmetic mean between ["Not-a-knot-start"](./#i-not-a-knot-start) and ["Not-a-knot-end"](./#ii-not-a-knot-end).

#### IV. Natural-start

A special case of ["Fixed-second-start"](./#xi-fixed-second-start) with a zero second derivative.\
Also, due to the specifics of a second-degree polynomial, it is a special case of ["Clamped-start"](./#viii-clamped-start) with the derivative equal to $\frac{\delta_1}{h_1}$.

#### V. Natural-end

A special case of ["Fixed-second-end"](./#xii-fixed-second-end) with a zero second derivative.\
Also, due to the specifics of a third-degree polynomial, it is a special case of ["Clamped-end"](./#ix-clamped-end) with the derivative equal to $\frac{\delta_{n-1}}{h_{n-1}}$.

#### VI. Semi-natural

The arithmetic mean between ["Natural-start"](./#iv-natural-start) and ["Natural-end"](./#v-natural-end).

#### VII. Semi-semi

The arithmetic mean between ["Semi-not-a-knot"](./#iii-semi-not-a-knot) and ["Semi-natural"](./#vi-semi-natural).

#### VIII. Clamped-start

A special case of ["Clamped (with index)"](./#xiv-clamped-with-index) for the first point ($k = 1$).

#### IX. Clamped-end

A special case of ["Clamped (with index)"](./#xiv-clamped-with-index) for the last point ($k = n$).

#### X. Semi-clamped

The arithmetic mean between ["Clamped-start"](./#viii-clamped-start) and ["Clamped-end"](./#ix-clamped-end).

#### XI. Fixed-second-start

A special case of ["Fixed-second (with index)"](./#xv-fixed-second-with-index) for the first segment ($k = 1$).

#### XII. Fixed-second-end

A special case of ["Fixed-second (with index)"](./#xv-fixed-second-with-index) for the last segment ($k = n - 1$).

#### XIII. Semi-fixed-second

The arithmetic mean between ["Fixed-second-start"](./#xi-fixed-second-start) and ["Fixed-second-end"](./#xii-fixed-second-end).

#### XIV. Clamped (with index)

Given: $k$ --- the index of the point ($1 \leqslant k \leqslant n$), $f'(x_k)$ --- the value of the derivative at that point.

Based on this information, we can compute the coefficients for the segments $k-1$ and $k$ (if they exist).\
If $k$ equals $1$ or $n$, then we can compute the coefficients for only the $k$-th or $(k-1)$-th segment, respectively.

For the $(k-1)$-th segment the condition gives the equation:

$$b_{k-1} + 2c_{k-1}h_{k-1} = f'(x_k)$$

Let us derive the coefficients for the $(k-1)$-th segment:
- From (1): $a_{k-1} = y_{k-1}$.
- From (3): $b_{k-1} + 2\left(\frac{\delta_{k-1}}{h_{k-1}^2} - \frac{b_{k-1}}{h_{k-1}}\right)h_{k-1} = f'(x_k)$\
	$b_{k-1} + 2\frac{\delta_{k-1}}{h_{k-1}} - 2b_{k-1} = f'(x_k)$\
	$b_{k-1} = 2\frac{\delta_{k-1}}{h_{k-1}} - f'(x_k)$.
- From (3): $c_{k-1} = \frac{\delta_{k-1} - b_{k-1}h_{k-1}}{h_{k-1}^2} = \frac{\frac{\delta_{k-1}}{h_{k-1}} - b_{k-1}}{h_{k-1}} = \frac{\delta_{k-1}}{h_{k-1}^2} - \frac{b_{k-1}}{h_{k-1}}$.

For the $k$-th segment the condition gives the equation:

$$b_k = f'(x_k)$$

Let us derive the coefficients for the $k$-th segment:
- From (1): $a_k = y_k$.
- $b_k = f'(x_k)$.
- From (3): $c_k = \frac{\delta_k - b_kh_k}{h_k^2} = \frac{\frac{\delta_k}{h_k} - b_k}{h_k} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}$.

Now we can iteratively construct all the other segments (see [here](./#formulas-for-iterative-construction)).

#### XV. Fixed-second (with index)

Given: $k$ --- the index of the SEGMENT (not of the point) ($1 \leqslant k \leqslant n-1$), $f''$ --- the value of the second derivative on this segment.

Based on this information, we can compute the coefficients for the $k$-th segment.

The condition gives the equation:

$$2c_k = f''$$

Let us derive the coefficients for the $k$-th segment:
- From (1): $a_k = y_k$.
- $c_k = \frac{f''}{2}$.
- From (2): $b_k = \frac{\delta_k - c_kh_k^2}{h_k} = \frac{\delta_k}{h_k} - c_kh_k$.

Now we can iteratively construct all the other segments (see [here](./#formulas-for-iterative-construction)).

#### XVI. Not-a-knot (with index)

Given: $k$ --- the index of the point ($2 \leqslant k \leqslant n-1$ --- excluding the end points), at which the second derivative is continuous, meaning that the value of the second derivative on the left and right segments at this point coincide.

Based on this information, we can compute the coefficients for the $(k-1)$-th and $k$-th segments.

The condition gives the equation:

$$c_{k-1} = c_k$$

From (3):\
$\frac{\delta_{k-1}}{h_{k-1}^2} - \frac{b_{k-1}}{h_{k-1}} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}$\
$\frac{b_k}{h_k} - \frac{b_{k-1}}{h_{k-1}} = \frac{\delta_k}{h_k^2} - \frac{\delta_{k-1}}{h_{k-1}^2}$

From the previous equality and (8) we obtain two expressions:\
$b_{k-1} = \left(\frac{h_{k-1}h_k}{h_{k-1}+h_k}\right)\left(2\frac{\delta_{k-1}}{h_{k-1}h_k} + \frac{\delta_{k-1}}{h_{k-1}^2} - \frac{\delta_k}{h_k^2}\right)$\
$b_k = \left(\frac{h_{k-1}h_k}{h_{k-1}+h_k}\right)\left(\frac{\delta_{k-1}}{h_{k-1}^2} + \frac{\delta_k}{h_k^2}\right)$

Substituting them into (6) we obtain:

$$c_{k-1} = \frac{\frac{\delta_k}{h_k} - \frac{\delta_{k-1}}{h_{k-1}}}{h_{k-1} + h_k}$$

Let us derive all the coefficients:
- From (1): $a_{k-1} = y_{k-1}$, $a_k = y_k$.
- $c_{k-1} = c_k = \frac{\frac{\delta_k}{h_k} - \frac{\delta_{k-1}}{h_{k-1}}}{h_{k-1} + h_k}$.
- From (2):
	- $b_{k-1} = \frac{\delta_{k-1} - c_{k-1}h_{k-1}^2}{h_{k-1}} = \frac{\delta_{k-1}}{h_{k-1}} - c_{k-1}h_{k-1}$,
	- $b_k = \frac{\delta_k - c_kh_k^2}{h_k} = \frac{\delta_k}{h_k} - c_kh_k$,
	- Also, to find one coefficient "b" after the other has been computed, you can use formula (8).

Now we can iteratively construct all the other segments (see [here](./#formulas-for-iterative-construction)).