+++
title = 'Barycentric Formula'
weight = 5
bookFlatSection = true
+++

The barycentric formula is another interpolation method related to interpolation polynomials.\
It does not allow for the computation of the coefficients of the interpolation polynomial, but it enables us to find its values at target points.

However, its capabilities are not limited to the values of the interpolation polynomial — in a certain way (described below), this formula can successfully interpolate functions even when using equally spaced (uniformly distributed) nodes, which is problematic for interpolation polynomials due to the [Runge's phenomenon](https://en.wikipedia.org/wiki/Runge%27s_phenomenon).

## Derivation of the formula

Let’s recall the [improved Lagrange polynomial formula](../polynomials/imp_lagrange.md):

$$P(x) = l(x) \sum_{i=0}^n{\frac{w_i}{x-x_i} y_i}$$

Note that for the function $f \equiv 1$, all values of $y_i$ will be equal to 1, so the interpolation formula for this function will look like:

$$1 = l(x) \sum_{i=0}^n{\frac{w_i}{x-x_i}}$$

Since division by one does not change the value, we can divide the improved Lagrange polynomial formula for the function of interest by the formula for the function $f \equiv 1$. In doing so, the $l(x)$ factors will cancel out:

$$\boxed{p(x) = \frac{\displaystyle \sum_{i=0}^n{\frac{w_i}{x-x_i} y_i}}{\displaystyle \sum_{i=0}^n{\frac{w_i}{x-x_i}}}}$$

This is the ***barycentric formula***.

Note that the weight coefficients $w_i$ in the numerator and denominator can be factored and any common factors can be canceled.\
This helps simplify calculations for known formulas of $w_i$ that depend on the distribution of nodes.

## Known formulas for barycentric weights $w_i$

We will present several node distributions on the interval $[-1, 1]$ and their corresponding formulas for the coefficients $w_i$.

If interpolation is performed not on the interval $[-1, 1]$, but on some other interval $[a, b]$, the barycentric weights are multiplied by $2^n(b-a)^{-n}$; however, this common factor is canceled out just like other common factors, so we will not take it into account.

### 1. Equally spaced nodes

$h = 2/n$

$x_i = -1 + ih$

$w_i = \frac{(-1)^i \binom{n}{k}}{h^n n!}$

After canceling common factors, we get:

$w_i = (-1)^i \binom{n}{k}$

### 2. Chebyshev nodes (of the first kind)

$x_i = -\cos{\frac{(2i+1)\pi}{2n+2}} = \cos{\frac{(2n-2i+1)\pi}{2n+2}}, \quad i = 0,...,n$

$w_i = (-1)^i \sin{\frac{(2i+1)\pi}{2n+2}}$

### 3. "Stretched" Chebyshev nodes of the first kind

For nodes "stretched" to the segment boundaries, the same weights are obtained:

$\displaystyle x_{i_{stretched}} = \frac{x_i}{\cos{\frac{\pi}{2n+2}}} = -
\frac{\cos{\frac{(2i+1)\pi}{2n+2}}}{\cos{\frac{\pi}{2n+2}}} = \frac{\cos{\frac{(2n-2i+1)\pi}{2n+2}}}{\cos{\frac{\pi}{2n+2}}}, \quad i = 0,...,n$

$w_{i_{stretched}} = w_i = (-1)^i \sin{\frac{(2i+1)\pi}{2n+2}}$

### 4. "Augmented" Chebyshev nodes of the first kind

To obtain "augmented" $(n+1)$ Chebyshev nodes of the first kind, we need to add the points $\{-1\}$ and $\{1\}$ to the $(n-1)$ Chebyshev nodes of the first kind:

$
x_i =
\begin{cases}
	-1, & i = 0 \\
	\cos{\frac{(2n-2i-1)\pi}{2n-2}}, & i = 1, ..., n - 1 \\
	1, & i = n
\end{cases}
$

$
w_i =
\begin{cases}
	1/2, & i = 0 \\
	\displaystyle \frac{(-1)^i}{(n - 1) \sin{\frac{(2i - 1)\pi}{2n-2}}}, & i = 1, ..., n - 1 \\
	(-1)^{n+1}/2, & i = n
\end{cases}
$

### 5. Chebyshev nodes of the second kind

$x_i = -\cos{\frac{in}{n}} = \cos{\frac{(n-i)\pi}{n}}, \quad i = 0,...,n$

$w_i = (-1)^i \delta_i, \quad \delta_i =
\begin{cases}
	\frac{1}{2}, & i = 0 \text{ or } i = n \\
	1, & \text{otherwise}
\end{cases}$

### 6. Chebyshev nodes of the third kind

In other sources, these may be called Chebyshev nodes of the *fourth* kind.

$x_i = -\cos{\frac{2i\pi}{2n+1}} = \cos{\frac{(2n-2i+1)\pi}{2n+1}}, \quad i = 0,...,n$

$w_i = (-1)^i \delta_i \cos{\frac{i\pi}{2n+1}}, \quad \delta_i =
\begin{cases}
	\frac{1}{2}, & i = 0 \\
	1, & \text{otherwise}
\end{cases}$

### 7. Chebyshev nodes of the fourth kind

In other sources, these may be called Chebyshev nodes of the *third* kind.

$x_i = -\cos{\frac{(2i+1)\pi}{2n+1}} = \cos{\frac{(2n-2i)\pi}{2n+1}}, \quad i = 0,...,n$

$w_i = (-1)^i \delta_i \sin{\frac{i\pi}{2n+1}}, \quad \delta_i =
\begin{cases}
	\frac{1}{2}, & i = n \\
	1, & \text{otherwise}
\end{cases}$

## References

1. Jean-Paul Berrut and Lloyd N. Trefethen, [*Barycentric Lagrange Interpolation*](https://people.maths.ox.ac.uk/trefethen/barycentric.pdf), SIAM Review, Vol. 46, No. 3, pp. 501–517, 2004.
2. J.-P. Berrut, *Baryzentrische Formeln zur trigonometrischen Interpolation* I, Z. Angew. Math. Phys. (ZAMP), 35 (1984), pp. 91–105.