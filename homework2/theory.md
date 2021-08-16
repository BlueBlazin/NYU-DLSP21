## 1.1 Convolutional Neural Netoworks

**(a)** $4 \times 5$

**(b)** 
$$
H' = 1 + \bigg\lfloor \frac{(H + 2P - D(K - 1) - 1)}{S} \bigg\rfloor,
$$

$$
W' = 1 + \bigg\lfloor \frac{(W + 2P - D(K - 1) - 1)}{S} \bigg\rfloor.
$$

**(c)** 

​	(i) 

​		Output dimension: $f_W \in \R^{1 \times 2}$.

​		Value of elements: $f_W(x)[c, j] = \sum\limits_{k = 0}^{3} \sum\limits_{i = 0}^{1} x[i, j * 2 + k]W[0, i, k]$.

​	(ii)

​		Dimension of $\frac{\partial f_W(x)}{\partial W}$: $1 \times 2 \times 2 \times 3,$

​		$\frac{\partial f_W(x)}{\partial W}[c, i, j, k] = x[j, i*2 + k].$

​	(iii)

​		Dimension of $\frac{\partial f_W(x)}{\partial x} = 1 \times 2 \times 2 \times 5,$

​		$\frac{\partial f_W(x)}{\partial x} = $



























