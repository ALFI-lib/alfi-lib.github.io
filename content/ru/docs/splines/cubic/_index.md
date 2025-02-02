+++
title = 'Кубические Сплайны'
weight = 4
+++

# Интерполяция кубическими сплайнами

Одним из методов интерполяции сплайнами является интерполяция кубическими сплайнами.

Пусть $S(x)$ --- кубический сплайн, построенный на $n$ точках $\left\{\left(x_i, y_i\right)\right\}_{i=1}^n$.\
$S(x)$ состоит из $n-1$ сегмента $S_k(x)$, каждый из которых представляет из себя многочлен третьей степени.

$k$-тый сегмент кубического сплайна имеет вид:\
$S_k(x) = a_k + b_k(x-x_k) + c_k(x-x_k)^2 + d_k(x-x_k)^3 {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$.

Кубический сплайн принимает значения $y_i$ для каждой точки $x_i$; также он имеет непрерывные первую и вторую производные.

### Общие условия кубических сплайнов:
1. $S_k(x_k) = y_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
2. $S_k(x_{k+1}) = y_{k+1} {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
3. $S_k'(x_{k+1}) = S_{k+1}'(x_{k+1}) {}_{, \ \forall k \in \left\{1,...,n-2\right\}}$
4. $S_k''(x_{k+1}) = S_{k+1}''(x_{k+1}) {}_{, \ \forall k \in \left\{1,...,n-2\right\}}$

Положим шаги между узлами и значениями в узлах:
- $h_k = x_{k+1} - x_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
- $\delta_k = y_{k+1} - y_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$.

Распишем общие условия с использованием коэффициентов:
1. $S_k(x_k) = y_k \Longleftrightarrow a_k = y_k$
2. $S_k(x_{k+1}) = y_{k+1} \Longleftrightarrow b_kh_k + c_kh_k^2 + d_kh_k^3 = \delta_k$
3. $S_k'(x_{k+1}) = S_{k+1}'(x_{k+1}) \Longleftrightarrow b_k + 2c_kh_k + 3d_kh_k^2 = b_{k+1}$
4. $S_k''(x_{k+1}) = S_{k+1}''(x_{k+1}) \Longleftrightarrow 2c_k + 6d_kh_k = 2c_{k+1}$ (можно сократить на 2)

Введём фиктивную переменную $c_n = 3d_{n-1}h_{n-1} + c_{n-1}$, что можно переписать как $c_{n-1} + 3d_{n-1}h_{n-1} = c_n$, таким образом, расширяя равенство под пунктом `4.` на $k = n - 1$.

В итоге получаем:

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

Теперь выведем равенства, которые помогут нам выразить одни коэффициенты через другие:

Из (4):
$$
\boxed{
	d_k = \frac{c_{k+1} - c_k}{3h_k}
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{5}
$$

Из (2), (5):\
$\frac{c_{k+1} - c_k}{3h_k}h_k^3 + c_kh_k^2 + b_kh_k = \delta_k$\
, откуда получаем:
$$
\boxed{
	b_k = \frac{\delta_k}{h_k} - h_k\frac{2c_k + c_{k+1}}{3}
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{6}
$$

Из (3), (5):\
$3\frac{c_{k+1} - c_k}{3h_k}h_k^2 + 2c_kh_k + b_k = b_{k+1}$\
$h_k(c_k + c_{k+1}) + b_k = b_{k+1}$

Тогда с использованием (6) можно получить следующее равенство:

<details>
<summary>Промежуточные выражения</summary>

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

Таким образом, мы получили $(n)$ переменных $c_k$ (среди них одна фиктивная --- $c_n$) и $(n-2)$ уравнений для их нахождения (среди них одно получено благодаря фиктивной переменной).

На данный момент мы можем создать неполную тридиагональную матрицу, представляющую из себя СЛАУ (систему линейных алгебраических уравнений) для нахождения значений переменных $c_k$:

$$
\begin{bmatrix}
	\boxed{?} & \boxed{?} & \boxed{?} & 0 & \dots & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & 0 \\
	0 & h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & \boxed{?} & \boxed{?} & \boxed{?}
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ c_3 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	\boxed{?} \\ R_1 \\ R_2 \\ \vdots \\ R_{n-2} \\ \boxed{?}
\end{bmatrix}
\tag{8}
$$
, где $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$.

Как видно, для формирования полной трёхдиагональной матрицы, нам необходимо ещё два уравнения.\
То есть для однозначного определения коэффициентов нам необходимо два дополнительных условия.

### Дополнительные условия

#### I. Натуральный сплайн

Натуральный кубический сплайн — это сплайн, у которого вторая производная равна нулю в крайних точках. Является частным случаем "Fixed-second" сплайна.

Условия: $S_1''(x_1) = 0, \ S_{n-1}''(x_n) = 0$.

Уравнения:
- $c_1 = 0$
- $c_n = 0$

Матрица:

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

[Подробнее про натуральный сплайн.](natural.md)

#### II. Not-a-knot сплайн

"Not-a-knot" кубический сплайн - это сплайн, у которого третья производная непрерывна во второй и предпоследней точках. То есть третья производная равна на первом и второй сегментах, а также на предпоследнем и последнем.

Условия: $S_1'''(x_2) = S_2'''(x_2), \ S_{n-2}'''(x_{n-1}) = S_{n-1}'''(x_{n-1})$.

Уравнения:
- $h_2c_1 + (-h_2 - h_1)c_2 + h_1c_3 = 0$
- $h_{n-1}c_{n-2} + (-h_{n-1} - h_{n-2})c_{n-1} + h_{n-2}c_n = 0$

Матрица:

$$
\begin{bmatrix}
	h_2 & -h_2 - h_1 & h_1 & \dots & 0 & 0 & 0 \\
	h_1 & 2h_1 + 2h_2 & h_2 & \dots & 0 & 0 & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
	0 & 0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	0 & 0 & 0 & \dots & h_{n-1} & -h_{n-1} - h_{n-2} & h_{n-2}
\end{bmatrix}
\begin{bmatrix}
	c_1 \\ c_2 \\ \vdots \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	0 \\ R_1 \\ \vdots \\ R_{n-2} \\ 0
\end{bmatrix}
$$

[Подробнее про "Not-a-knot" сплайн.](not-a-knot.md)

#### III. Периодический сплайн

Периодический кубический сплайн - это сплайн, первая и вторая производные которого равна на концах.

Условия: $S_1'(x_1) = S_{n-1}'(x_n), \ S_1''(x_1) = S_{n-1}''(x_n)$.

Матрица (в данном случае не тридиагональная):

$$
\begin{bmatrix}
	2h_1 + 2h_2 & h_2 & 0 & \dots & 0 & h_1 \\
	h_2 & 2h_2 + 2h_3 & h_3 & \dots & 0 & 0 \\
	0 & h_3 & 2h_3 + 2h_4 & \dots & 0 & 0 \\
	\vdots & \vdots & \ddots & \ddots & \vdots & \vdots \\
	0 & 0 & \dots & 2h_{n-3} + 2h_{n-2} & h_{n-2} & 0 \\
	0 & 0 & \dots & h_{n-2} & 2h_{n-2} + 2h_{n-1} & h_{n-1} \\
	h_1 & 0 & \dots & 0 & h_{n-1} & 2h_{n-1} + 2h_1
\end{bmatrix}
\begin{bmatrix}
	c_2 \\ c_3 \\ c_4 \\ \vdots \\ c_{n-2} \\ c_{n-1} \\ c_n
\end{bmatrix}
= \begin{bmatrix}
	R_1 \\ R_2 \\ R_3 \\ \vdots \\ R_{n-3} \\ R_{n-2} \\ R_{n-1}
\end{bmatrix}
$$
, где $c_n = c_1$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, $R_{n-1} = 3\left(\frac{\delta_1}{h_1} - \frac{\delta_{n-1}}{h_{n-1}}\right)$.

[Подробнее про периодический сплайн.](periodic.md)

#### IV. Parabolic-ends

"Parabolic-ends" (параболические концы) кубический сплайн - это сплайн, крайние сегменты которого представляют из себя кривые второй степени или параболы.\
Этот сплайн является частным случаем "Fixed-third" сплайна, когда третьи производные на концах устанавливаются равными нулю.

Условия: $S_1'''(x_1) = 0, \ S_{n-1}'''(x_n) = 0$.

Уравнения:
- $c_1 - c_2 = 0$
- $-c_{n-1} + c_n = 0$

Матрица:

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

Особый случай: $n = 2$:
- $c_1 = 0$
- $c_2 = 0$

[Подробнее про "Parabolic-ends" сплайн.](parabolic-ends.md)

#### V. Зажатый сплайн

Зажатый кубический сплайн - это сплайн с фиксированными первыми производными на концах.

Условия: $S_1'(x_1) = f'(x_1), \ S_{n-1}'(x_n) = f'(x_n)$.

Уравнения:
- $2h_1c_1 + h_1c_2 = 3\left(\frac{\delta_1}{h_1} - f'(x_1)\right)$
- $h_{n-1}c_{n-1} + 2h_{n-1}c_n = 3\left(f'(x_n) - \frac{\delta_{n-1}}{h_{n-1}}\right)$

Матрица:

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
, где $R_0 = 3\left(\frac{\delta_1}{h_1} - f'(x_1)\right)$, $R_k = 3\left(\frac{\delta_{k+1}}{h_{k+1}} - \frac{\delta_k}{h_k}\right)$, $R_n = 3\left(f'(x_n) - \frac{\delta_{n-1}}{h_{n-1}}\right)$.

[Подробнее про зажатый сплайн.](clamped.md)

#### VI. Fixed-second сплайн

"Fixed-second" кубический сплайн - это сплайно с фиксированными вторыми производными на концах.\
Частным случаем является натуральный сплайн, у которого вторые производные на концах устанавливаются равными нулю.

Условия: $S_1''(x_1) = f''(x_1), \ S_{n-1}''(x_n) = f''(x_n)$.

Уравнения:
1. $c_1 = \frac{f''(x_1)}{2}$
2. $c_n = \frac{f''(x_n)}{2}$

Матрица:

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

[Подробнее про "Fixed-second" сплайн.](fixed-second.md)

#### VII. Fixed-third сплайн

"Fixed-third" кубический сплайн - это сплайно с фиксированными третьими производными на концах.\
Частным случаем является "Parabolic-ends" сплйан, у которого третьи производные на концах устанавливаются равными нулю.

Условия: $S_1'''(x_1) = f'''(x_1), \ S_{n-1}'''(x_n) = f'''(x_n)$.

Уравнения:
- $c_1 - c_2 = -\frac{h_1f'''(x_1)}{2}$
- $-c_{n-1} + c_n = \frac{h_{n-1}f'''(x_n)}{2}$

Матрица:

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

Особый случай: $n = 2$:
- $c_1 = -\frac{h_1\left(f'''(x_1) + f'''(x_2)\right)}{8}$
- $c_2 = -c_1$

[Подробнее про "Fixed-third" сплайн.](fixed-third.md)