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

​		Value of elements: $f_W(x)[i, j] = \sum\limits_{k=0}^{2}\sum\limits_{l=0}^1 x[l, 2*j + k]W[i, l, k]$.

​	(ii)

​		Dimension of $\frac{\partial f_W(x)}{\partial W}$ $\in \R^{1 \times 2 \times 3 \times 2 \times 1},$

​		$\frac{\partial f_W(x)}{\partial W}[a, b, e, d, c] = \frac{\partial f_W[a, b]}{\partial W[e, d, c]} = \sum\limits_{k=0}^2\sum\limits_{l=0}^1 x[l, 2*b + k]\delta_{i=c, l=d, k=e} = x[d, 2*b + e]\delta_{a=c}.$

​	(iii)

​		Dimension of $\frac{\partial f_W(x)}{\partial x} \in \R^{1 \times 2 \times 5 \times 2},$

​		$\frac{\partial f_W(x)}{\partial x}[a, b, d, c] = \frac{\partial f_W[a, b]}{\partial x[d, c]} = \sum\limits_{k=0}^2\sum\limits_{l=0}^1 W[a, l, k] \delta_{l=c, 2*j + k = d} = \sum\limits_{k=0}^2 W[a, c, k]\delta_{k = d - b}.$

​	(iv)

​		Dimension of $\frac{\partial l}{\partial W} \in \R^{3 \times 2 \times 1}$
$$
\frac{\partial l}{\partial W}[c, b, a] = (\frac{\partial l}{\partial f_W} \frac{\partial f_W}{\partial W})[c, b, a] 
\\
= \sum\limits_{j}\sum\limits_{i}\frac{\partial l}{\partial f_W}[j, i] \frac{\partial f_W(x)}{\partial W}[i, j, c, b, a]
\\
= \sum\limits_{j}\sum\limits_{i}\frac{\partial l}{\partial f_W}[j, i] x[b, 2*j + c]\delta_{i=a}
\\
= \sum\limits_{j} \frac{\partial l}{\partial f_W}[j, a] x[b, 2*j + c].
$$
​		In (i) there is a reduction over $m$ in the $2*n + m$ second dimension of $x$. On the other hand, in the 		above expression there is a reduction over $n$ instead.	

---

## 1.2 Recurrent Neural Networks

**(a)**      ![hw2-rnn.png](/Users/sanjeet/NYU-DLSP21/homework2/hw2-rnn.png.png)

**(b)** $z_t \in \R^m.$

**(c)**

​	Dimension of $\frac{\partial l}{\partial W_x} \in \R^{n \times m}.$
$$
\frac{\partial l}{\partial W_x} = \sum\limits_t \frac{\partial l}{\partial z_t} \frac{\partial z_t}{\partial W_x},
\\
= \sum\limits_t \frac{\partial l}{\partial z_t} \bigg( c_t \odot \frac{\partial z_{t - 1}}{\partial W_x} + (1 - c_t) \odot \frac{\partial W_x x_{t-1}}{\partial W_x} \bigg).
$$
​	Both the backward and forward pass have a very similar structure with the main difference being the forward pass is a branching out operation as the same shared weights $W_x$ produce multiple outputs whereas the backward pass is a sum as the gradients all accumulate in $\frac{\partial l}{\partial W_x}$.

**(d)** This network can be subject to the exploding gradient problem gradient w.r.t. the output at timestep $t$ has a multiplicative dependency on all gradients w.r.t. outputs in the future timesteps. This can cause the gradient to blow up.

The network is less susceptible to the vanishing gradient problem due to the $c_t \odot z_{t - 1}$ term that provides the gradient to pass backwards without a multiplicative interaction.













































