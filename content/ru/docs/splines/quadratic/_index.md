+++
title = 'Квадратичные Сплайны'
weight = 3
+++

# Интерполяция квадратичными сплайнами

Одним из методов интерполяции сплайнами является интерполяция квадратичными сплайнами.

Пусть $S(x)$ --- квадратичный сплайн, построенный на $n$ точках $\left\{\left(x_i, y_i\right)\right\}_{i=1}^n$.\
$S(x)$ состоит из $n-1$ сегмента $S_k(x)$, каждый из которых представляет из себя многочлен второй степени.

$k$-тый сегмент квадратичного сплайна имеет вид:\
$S_k(x) = a_k + b_k(x-x_k) + c_k(x-x_k)^2 {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$.

Квадратичный сплайн принимает значения $y_i$ для каждой точки $x_i$; также он имеет непрерывную первую производную.

### Общие условия квадратичных сплайнов:
1. $S_k(x_k) = y_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
2. $S_k(x_{k+1}) = y_{k+1} {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
3. $S_k'(x_{k+1}) = S_{k+1}'(x_{k+1}) {}_{, \ \forall k \in \left\{1,...,n-2\right\}}$

Положим шаги между узлами и значениями в узлах:
- $h_k = x_{k+1} - x_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$
- $\delta_k = y_{k+1} - y_k {}_{, \ \forall k \in \left\{1,...,n-1\right\}}$.

Распишем общие условия с использованием коэффициентов:
1. $S_k(x_k) = y_k \Longleftrightarrow a_k = y_k$
2. $S_k(x_{k+1}) = y_{k+1} \Longleftrightarrow b_kh_k + c_kh_k^2 = \delta_k$
3. $S_k'(x_{k+1}) = S_{k+1}'(x_{k+1}) \Longleftrightarrow b_k + 2c_kh_k = b_{k+1}$

Из полученных формул можно вывести несколько полезных формул для выражения коэффициентов:

Из первого пункта:

$$
\boxed{
	a_k = y_k
}
{}_{, \ \forall k \in \left\{1,...,n-1\right\}}
\tag{1}
$$

Из второго пункта:

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

Из третьего пункта:

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

Из (2), (4):\
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

Из (3), (6):\
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

#### Формулы для итеративного построения

Выведем формулы для расчёта следующего сегмента при условии известных коэффицеинтов для преыдущего:

Даны: $a_k, b_k, c_k$. Вывести $a_{k+1}, b_{k+1}, c_{k+1}$. $_{k \in \left\{1,...,n-2\right\}}$.

1. $a_{k+1}$: Из (1): $a_{k+1} = y_{k+1}$.
2. $b_{k+1}$: Несклько способов:
	- Из (5): $b_{k+1} = b_k + 2c_kh_k$.
	- Из (7): $b_{k+1} = c_kh_k + \frac{\delta_k}{h_k}$.
	- Из (8): $b_{k+1} = 2\frac{\delta_k}{h_k} - b_k$.
3. $c_{k+1}$: Из (3): $c_k = \frac{\delta_k - b_kh_k}{h_k^2} = \frac{\frac{\delta_k}{h_k} - b_k}{h_k} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}$.

Выведем формулы для расчёта предыдущего сегмента при условии известных коэффицеинтов следующего:

Даны: $a_{k+1}, b_{k+1}, c_{k+1}$. Вывести $a_k, b_k, c_k$. $_{k \in \left\{1,...,n-2\right\}}$.

1. $a_k$: Из (1): $a_k = y_k$.
2. $b_k$: Из (8): $b_k = 2\frac{\delta_k}{h_k} - b_{k+1}$.
3. $c_k$: Несколько способов:
	- Из (3): $c_k = \frac{\delta_k - b_kh_k}{h_k^2} = \frac{\frac{\delta_k}{h_k} - b_k}{h_k} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}$.
	- Из (6): $c_k = \frac{b_{k+1} - b_k}{2h_k}$.
	- Из (7): $c_k = \frac{b_{k+1}h_k - \delta_k}{h_k^2} = \frac{b_{k+1} - \frac{\delta_k}{h_k}}{h_k} = \frac{b_{k+1}}{h_k} - \frac{\delta_k}{h_k^2}$.

Таким образом, если мы вычислим коэффициенты одного сегмента, мы сможем построить все остальные сегменты.

Поскольку сплайн имеет $3(n-1)$ коэффициентов, а имеем мы $2(n-1) + (n-2) = 3(n-1)-1$ уравнений, нам необходимо ещё одно уравнение для однозначного определения коэффициентов сплайна.

С помощью последнего уравнения мы сможем вычислить коэффициенты одного сегмента сплайна, после чего мы сможем итеративно вычислить коэффицеинты всех последующих и предыдущих сегментов.

Для получения последнего уравнения нам понадобится дополнительное условие.

### Дополнительные условия

#### I. Not-a-knot-start

Частный случай ["Not-a-knot (with index)"](./#xvi-not-a-knot-with-index) для второй точки ($k = 2$).

#### II. Not-a-knot-end

Частный случай ["Not-a-knot (with index)"](./#xvi-not-a-knot-with-index) для предпоследней точки ($k = n - 1$).

#### III. Semi-not-a-knot

Среднее арифметическое между ["Not-a-knot-start"](./#i-not-a-knot-start) и ["Not-a-knot-end"](./#ii-not-a-knot-end).

#### IV. Natural-start

Частный случай ["Fixed-second-start"](./#xi-fixed-second-start) с нулевой второй производной.\
Также в силу специфики многочлена второй степени является частным случаем ["Clamped-start"](./#viii-clamped-start) с производной, равной $\frac{\delta_1}{h_1}$.

#### V. Natural-end

Частный случай ["Fixed-second-end"](./#xii-fixed-second-end) с нулевой второй производной.\
Также в силу специфики многочлена третьей степени является частным случаем ["Clamped-end"](./#ix-clamped-end) с производной, равной $\frac{\delta_{n-1}}{h_{n-1}}$.

#### VI. Semi-natural

Среднее арифметическое между ["Natural-start"](./#iv-natural-start) и ["Natural-end"](./#v-natural-end).

#### VII. Semi-semi

Среднее арифметическое между ["Semi-not-a-knot"](./#iii-semi-not-a-knot) и ["Semi-natural"](./#vi-semi-natural).

#### VIII. Clamped-start

Частный случай ["Clamped (with index)"](./#xiv-clamped-with-index) для первой точки ($k = 1$).

#### IX. Clamped-end

Частный случай ["Clamped (with index)"](./#xiv-clamped-with-index) для последней точки ($k = n$).

#### X. Semi-clamped

Среднее арифметическое между ["Clamped-start"](./#viii-clamped-start) и ["Clamped-end"](./#ix-clamped-end).

#### XI. Fixed-second-start

Частный случай ["Fixed-second (with index)"](./#xv-fixed-second-with-index) для первого сегмента ($k = 1$).

#### XII. Fixed-second-end

Частный случай ["Fixed-second (with index)"](./#xv-fixed-second-with-index) для последнего сегмента ($k = n - 1$).

#### XIII. Semi-fixed-second

Среднее арифметическое между ["Fixed-second-start"](./#xi-fixed-second-start) и ["Fixed-second-end"](./#xii-fixed-second-end).

#### XIV. Clamped (with index)

Даны: $k$ --- номер точки ($1 \leqslant k \leqslant n$), $f'(x_k)$ --- значение производной в этой точке.

На основе этой информации мы можем вычислить коэффициенты для сегментов $k-1$ и $k$ (если они существуют).\
Если $k$ равно $1$ или $n$, то мы можем вычислить коэффициенты только $k$-го или $k-1$-го сегмента соответственно.

Для $k-1$-го сегмента условие даёт уравнение:

$$b_{k-1} + 2c_{k-1}h_{k-1} = f'(x_k)$$

Выведем коэффициенты для $k-1$-го сегмента:
- Из (1): $a_{k-1} = y_{k-1}$.
- Из (3): $b_{k-1} + 2\left(\frac{\delta_{k-1}}{h_{k-1}^2} - \frac{b_{k-1}}{h_{k-1}}\right)h_{k-1} = f'(x_k)$\
	$b_{k-1} + 2\frac{\delta_{k-1}}{h_{k-1}} - 2b_{k-1} = f'(x_k)$\
	$b_{k-1} = 2\frac{\delta_{k-1}}{h_{k-1}} - f'(x_k)$.
- Из (3): $c_{k-1} = \frac{\delta_{k-1} - b_{k-1}h_{k-1}}{h_{k-1}^2} = \frac{\frac{\delta_{k-1}}{h_{k-1}} - b_{k-1}}{h_{k-1}} = \frac{\delta_{k-1}}{h_{k-1}^2} - \frac{b_{k-1}}{h_{k-1}}$.

Для $k$-го сегмента условие даёт уравнение:

$$b_k = f'(x_k)$$

Выведем коэффициенты для $k$-го сегмента:
- Из (1): $a_k = y_k$.
- $b_k = f'(x_k)$.
- Из (3): $c_k = \frac{\delta_k - b_kh_k}{h_k^2} = \frac{\frac{\delta_k}{h_k} - b_k}{h_k} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}$.

Теперь мы можем итеративно построить все остальные сегменты (см. [здесь](./#формулы-для-итеративного-построения)).

#### XV. Fixed-second (with index)

Даны: $k$ --- номер СЕГМЕНТА (не точки) ($1 \leqslant k \leqslant n-1$), $f''$ --- значение второй производной на этом сегменте.

На основе этой информации мы можем вычислить коэффициенты для $k$-го сегмента.

Условие даёт уравнение:

$$2c_k = f''$$

Выведем коэффициенты для $k$-го сегмента:
- Из (1): $a_k = y_k$.
- $c_k = \frac{f''}{2}$.
- Из (2): $b_k = \frac{\delta_k - c_kh_k^2}{h_k} = \frac{\delta_k}{h_k} - c_kh_k$.

Теперь мы можем итеративно построить все остальные сегменты (см. [здесь](./#формулы-для-итеративного-построения)).

#### XVI. Not-a-knot (with index)

Даны: $k$ --- номер точки ($2 \leqslant k \leqslant n-1$ --- за исключением крайних точек), в которой вторая производная непрерывна, то есть значение второй производной на левом и правом сегменте в этой точке совпадают.

На основе этой информации мы можем вычислить коэффициенты для $k-1$ и $k$-го сегментов.

Условие даёт уравнение:

$$c_{k-1} = c_k$$

Из (3):\
$\frac{\delta_{k-1}}{h_{k-1}^2} - \frac{b_{k-1}}{h_{k-1}} = \frac{\delta_k}{h_k^2} - \frac{b_k}{h_k}$\
$\frac{b_k}{h_k} - \frac{b_{k-1}}{h_{k-1}} = \frac{\delta_k}{h_k^2} - \frac{\delta_{k-1}}{h_{k-1}^2}$

Из предыдущего равенства и (8) получаются два выражения:\
$b_{k-1} = \left(\frac{h_{k-1}h_k}{h_{k-1}+h_k}\right)\left(2\frac{\delta_{k-1}}{h_{k-1}h_k} + \frac{\delta_{k-1}}{h_{k-1}^2} - \frac{\delta_k}{h_k^2}\right)$\
$b_k = \left(\frac{h_{k-1}h_k}{h_{k-1}+h_k}\right)\left(\frac{\delta_{k-1}}{h_{k-1}^2} + \frac{\delta_k}{h_k^2}\right)$

Подставляем их в (6) и получаем:

$$c_{k-1} = \frac{\frac{\delta_k}{h_k} - \frac{\delta_{k-1}}{h_{k-1}}}{h_{k-1} + h_k}$$

Выведем все коэффициенты:
- Из (1): $a_{k-1} = y_{k-1}$, $a_k = y_k$.
- $c_{k-1} = c_k = \frac{\frac{\delta_k}{h_k} - \frac{\delta_{k-1}}{h_{k-1}}}{h_{k-1} + h_k}$.
- Из (2):
	- $b_{k-1} = \frac{\delta_{k-1} - c_{k-1}h_{k-1}^2}{h_{k-1}} = \frac{\delta_{k-1}}{h_{k-1}} - c_{k-1}h_{k-1}$,
	- $b_k = \frac{\delta_k - c_kh_k^2}{h_k} = \frac{\delta_k}{h_k} - c_kh_k$,
	- Также для нахождения одного коэффициента "b" после нахождения другого можно использовать формулу (8).

Теперь мы можем итеративно построить все остальные сегменты (см. [здесь](./#формулы-для-итеративного-построения)).