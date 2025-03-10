+++
title = 'Lagrange Formula'
weight = 1
+++

Lagrange's formula is a classical formula for constructing an interpolation polynomial. It allows us to obtain a unique polynomial of degree $n$ that passes through a given set of $(n+1)$ nodes $(x_k, y_k),{}_{k \in \left\{0, ..., n\right\}}$:

$$P(x) = \sum_{i=0}^n{y_i l_i(x)}$$

where:
- $x_i$ are the coordinates of the nodes,
- $y_i$ are the function values at these points,
- $l_i(x) = \prod_{j \ne i}{\frac{x-x_j}{x_i-x_j}}$ is the Lagrange basis polynomial for each point, which equals 1 when $x = x_i$ and 0 when $x = x_j$ for $j \neq i$.