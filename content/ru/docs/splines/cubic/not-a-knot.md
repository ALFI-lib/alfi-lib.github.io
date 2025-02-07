+++
title = 'Not-a-knot'
weight = 2
+++

"Not-a-knot" кубический сплайн - это сплайн, у которого третья производная непрерывна во второй и предпоследней точках. То есть третья производная равна на первом и второй сегментах, а также на предпоследнем и последнем.

Условия: $S_1'''(x_2) = S_2'''(x_2), \ S_{n-2}'''(x_{n-1}) = S_{n-1}'''(x_{n-1})$.

Из них получаются следующие выражения для коэффициентов:
1. $6d_1 = 6d_2 \Longrightarrow d_1 = d_2$
2. $6d_{n-2} = 6d_{n-1} \Longrightarrow d_{n-2} = d_{n-1}$

Из (5) получаем:
1. $\frac{c_2 - c_1}{3h_1} = \frac{c_3 - c_2}{3h_2} \Longrightarrow h_2c_2 - h_2c_1 = h_1c_3 - h_1c_2$
2. $\frac{c_{n-1} - c_{n-2}}{3h_{n-2}} = \frac{c_n - c_{n-1}}{3h_{n-1}} \Longrightarrow h_{n-1}c_{n-1} - h_{n-1}c_{n-2} = h_{n-2}c_n - h_{n-2}c_{n-1}$

, из которых получаем два уравнения:
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

Из (7) для $k = 1$ получаем:\
$c_1(h_1) + c_2(2h_1 + 2h_2) + c_3(h_2) = 3\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)$

Вычитаем это уравнение, умноженное на $\frac{h_1}{h_2}$, из (II.1), чтобы занулить коэффициент перед $c_3$:\
$c_1\left(h_2 - \frac{h_1^2}{h_2}\right) + c_2\left(-h_2 - h_1 - 2\frac{h_1^2}{h_2} - 2h_1\right) = -3\frac{h_1}{h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)$

Выносим общий множитель из коэффициентов:\
$c_1\left(-\frac{h_1+h_2}{h_2}\right)(h_1-h_2) + c_2\left(-\frac{h_1+h_2}{h_2}\right)(2h_1+h_2) = \left(-\frac{h_1+h_2}{h_2}\right)\left(3\frac{h_1}{h_1+h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)\right)$

И сокращаем на $\left(-\frac{h_1+h_2}{h_2}\right)$:
$$
\boxed{
	(h_1-h_2)c_1 + (2h_1+h_2)c_2 = 3\frac{h_1}{h_1+h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)
}
\tag{II.3}
$$

Аналогично получаем формулу для последней строки матрицы:

<details>
<summary>Подробнее</summary>

Из (7) для $k = n-2$ получаем:\
$c_{n-2}(h_{n-2}) + c_{n-1}(2h_{n-2} + 2h_{n-1}) + c_n(h_{n-1}) = 3\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$

Вычитаем это уравнение, умноженное на $\frac{h_{n-1}}{h_{n-2}}$, из (II.2), чтобы занулить коэффициент перед $c_{n-2}$:\
$c_{n-1}\left(-h_{n-1} - h_{n-2} - 2\frac{h_{n-1}^2}{h_{n-2}} - 2h_{n-1}\right) + c_n\left(h_{n-2} - \frac{h_{n-1}^2}{h_{n-2}}\right) = -3\frac{h_{n-1}}{h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$

Выносим общий множитель из коэффициентов:\
$c_{n-1}\left(-\frac{h_{n-1}+h_{n-2}}{h_{n-2}}\right)(2h_{n-1}+h_{n-2}) + c_n\left(-\frac{h_{n-1}+h_{n-2}}{h_{n-2}}\right)(h_{n-1}-h_{n-2}) = \left(-\frac{h_{n-1}+h_{n-2}}{h_{n-2}}\right)\left(3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)\right)$

И сокращаем на $\left(-\frac{h_{n-1}+h_{n-2}}{h_{n-2}}\right)$:\
$c_{n-1}(2h_{n-1}+h_{n-2}) + c_n(h_{n-1}-h_{n-2}) = 3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$
</details>

$$
\boxed{
	c_{n-1}(h_{n-2}+2h_{n-1}) + c_n(-h_{n-2}+h_{n-1}) = 3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)
}
\tag{II.4}
$$

Заносим уравнения (II.3) и (II.4) в матрицу:

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
, где $R_0 = 3\frac{h_1}{h_1+h_2}\left(\frac{\delta_2}{h_2} - \frac{\delta_1}{h_1}\right)$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, $R_{n-1} = 3\frac{h_{n-1}}{h_{n-1}+h_{n-2}}\left(\frac{\delta_{n-1}}{h_{n-1}} - \frac{\delta_{n-2}}{h_{n-2}}\right)$.

Теперь матрицу можно решить с помощью [метода прогонки](https://ru.wikipedia.org/wiki/Метод_прогонки).

После нахождения коэффициентов $c_k$ остальные коэффициенты $b_k$ и $d_k$ можно вычислить по формулам (6) и (5) соответственно.