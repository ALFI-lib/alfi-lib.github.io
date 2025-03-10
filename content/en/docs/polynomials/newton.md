+++
title = 'Newton Formula'
weight = 3
+++

Newton's formula is another classical formula for constructing an interpolation polynomial. It allows us to obtain a unique polynomial of degree $n$ that passes through a given set of $(n+1)$ nodes $(x_k, y_k),{}_{k \in \left\{0, ..., n\right\}}$:

$$P(x) = f[x_0] + f[x_0,x_1](x-x_0) + f[x_0,x_1,x_2](x-x_0)(x-x_1) + \cdots + f[x_0, x_1, ..., x_n](x-x_0)(x-x_1)\cdots(x-x_{n-1})$$

or

$$P(x) = \sum_{i=0}^n{\left(f[x_0, ..., x_i] \cdot \prod_{j=0}^{i-1}{(x-x_j)}\right)}$$

where:
- $x_i$ are the coordinates of the nodes,
- $y_i$ are the function values at these points,
- $f[...]$ represents divided differences.

The divided differences $f[...]$ are computed using the formula

$$f[x_j, x_{j+1}, ..., x_{k-1}, x_k] = \frac{f[x_{j+1}, ..., x_{k-1}, x_k] - f[x_j, x_{j+1}, ..., x_{k-1}]}{x_k-x_j}$$

with the initial condition $f[x_j] = y_j$.

## References

1. Jean-Paul Berrut and Lloyd N. Trefethen, [*Barycentric Lagrange Interpolation*](https://people.maths.ox.ac.uk/trefethen/barycentric.pdf), SIAM Review, Vol. 46, No. 3, pp. 501–517, 2004.