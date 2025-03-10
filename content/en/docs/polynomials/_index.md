+++
title = 'Polynomials'
weight = 3
bookFlatSection = true
+++

*Interpolation polynomials* are commonly used for function interpolation.

*Interpolation polynomials* are polynomials of the form $a_0 + a_1x + a_2x^2 + \cdots$, which pass through a given set of nodes and depend only on the coordinates of these points.

Let $(n+1)$ points be given with indices from $0$ to $n$, inclusive: $(x_k, y_k),{}_{k \in \left\{0, ..., n\right\}}$.

When interpolating with polynomials, a polynomial of degree $n$ is typically used, because there is a *unique* polynomial of that degree that passes through $(n+1)$ points.

There are two approaches to interpolation:
1. Calculating the coefficients of the interpolation polynomial and then evaluating it at the required points:
	- [Lagrange's formula](lagrange.md)
	- [Improved Lagrange's formula](imp_lagrange.md)
	- [Newton's formula](newton.md)
2. Evaluating the interpolation polynomial directly --- without calculating the coefficients:
	- [Lagrange's formula](lagrange.md)
	- [Improved Lagrange's formula](imp_lagrange.md)
	- [Newton's formula](newton.md)
	- [Barycentric formula](../barycentric-formula/_index.md)