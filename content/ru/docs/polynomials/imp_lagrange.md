+++
title = 'Улучшенная Формула Лагранжа'
weight = 2
+++

Улучшенная формула многочлена Лагранжа является модификацией [формулы многочлена Лагранжа](lagrange.md), а также позволяет вывести [барицентрическую формулу](../barycentric-formula/_index.md).

Вспомним [формулу интерполяционного многочлена Лагранжа](lagrange.md):

$$P(x) = \sum_{i=0}^n{y_i l_i(x)}$$

$l_i(x) = \prod_{j \ne i}{\frac{x-x_j}{x_i-x_j}}$ --- базисный многочлен.

Введём

$$l(x) = (x-x_0)(x-x_1)\cdots(x-x_n)$$

и определим *барицентрические веса* как

$$w_i = \frac{1}{\prod_{j \ne i}{(x_i-x_j)}}$$

Заметим, что $w_i = 1/l'(x_i)$.

Тогда базисный многочлен можно представить в таком виде:

$$l_i(x) = l(x)\frac{w_i}{x-x_i}$$

После подстановки в изначальную формулу, можно вынести $l(x)$ так:

$$\boxed{P(x) = l(x) \sum_{i=0}^n{\frac{w_i}{x-x_i} y_i}}$$

Это и есть ***улучшенная формула многочлена Лагранжа***.

## Ссылки

1. Jean-Paul Berrut and Lloyd N. Trefethen, [*Barycentric Lagrange Interpolation*](https://people.maths.ox.ac.uk/trefethen/barycentric.pdf), SIAM Review, Vol. 46, No. 3, pp. 501–517, 2004.