+++
title = 'Improved Lagrange Formula'
weight = 2
+++

The improved Lagrange polynomial formula is a modification of the [Lagrange polynomial formula](lagrange.md), and it also allows us to derive the [barycentric formula](../barycentric-formula/_index.md).

Let’s recall the [Lagrange interpolation polynomial formula](lagrange.md):

$$P(x) = \sum_{i=0}^n{y_i l_i(x)}$$

where $l_i(x) = \prod_{j \ne i}{\frac{x-x_j}{x_i-x_j}}$ is the Lagrange basis polynomial.

We introduce

$$l(x) = (x-x_0)(x-x_1)\cdots(x-x_n)$$

and define the *barycentric weights* as

$$w_i = \frac{1}{\prod_{j \ne i}{(x_i-x_j)}}$$

Note that $w_i = 1/l'(x_i)$.

Thus, the Lagrange basis polynomial can be expressed as:

$$l_i(x) = l(x)\frac{w_i}{x-x_i}$$

Substituting this into the original formula, we can factor out $l(x)$:

$$\boxed{P(x) = l(x) \sum_{i=0}^n{\frac{w_i}{x-x_i} y_i}}$$

This is the ***improved Lagrange polynomial formula***.

## References

1. Jean-Paul Berrut and Lloyd N. Trefethen, [*Barycentric Lagrange Interpolation*](https://people.maths.ox.ac.uk/trefethen/barycentric.pdf), SIAM Review, Vol. 46, No. 3, pp. 501–517, 2004.