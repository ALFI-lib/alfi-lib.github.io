+++
title = 'Parabolic-ends'
weight = 4
+++

"Parabolic-ends" (параболические концы) кубический сплайн - это сплайн, крайние сегменты которого представляют из себя кривые второй степени или параболы.

Является частным случаем ["Fixed-third" сплайна](fixed-third.md), когда третьи производные на концах устанавливаются равными нулю.

Условия: $S_1'''(x_1) = 0, \ S_{n-1}'''(x_n) = 0$.

Из них получаются следующие выражения для коэффициентов:
1. $6d_1 = 0$
2. $6d_{n-1} = 0$

Таким образом:

$$
\boxed {
	d_1 = 0
}
\tag{IV.1}
$$
$$
\boxed {
	d_{n-1} = 0
}
\tag{IV.2}
$$

Из (5), (VI.1):

$$
\boxed{
	c_1 - c_2 = 0
}
\tag{IV.3}
$$

Из (5), (VI.2):

$$
\boxed{
	-c_{n-1} + c_n = 0
}
\tag{IV.4}
$$

Таким образом, мы получаем два недостающих уравнения для матрицы:
1. $c_1 - c_2 = 0$
2. $-c_{n-1} + c_n = 0$

Заносим их в матрицу:

$$
\begin{bmatrix}
	1 & -1 & 0 & 0 & \dots & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & 0 \\
	0 & h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & 0 & -1 & 1
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ c_3 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	0 \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ 0
\end{bmatrix}
$$
, где $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$.

Теперь матрицу можно решить с помощью [метода прогонки](https://ru.wikipedia.org/wiki/Метод_прогонки).

После нахождения коэффициентов $c_k$ остальные коэффициенты $b_k$ и $d_k$ можно вычислить по формулам (6) и (5) соответственно.

### Особый случай: $n = 2$.

В случае, когда точек две (а значит, сегмент один), уравнения становятся идентичными:

$$
\begin{cases}
	c_1 - c_2 = 0 \\
	-c_1 + c_2 = 0
\end{cases}
\Rightarrow
\begin{cases}
	c_1 - c_2 = 0 \\
	c_1 - c_2 = 0
\end{cases}
$$

Таким образом, мы получаем всего одно уравнение, вместо двух.

Чтобы выкрутиться из этой ситуации, приравняем модули $c_1$ и $c_2$ (который фиктивный).

Тогда $c_1$ и $c_2$ будут равны нулю.