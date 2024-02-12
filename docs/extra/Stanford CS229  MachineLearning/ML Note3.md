# ML Note3 SVM
!!!NOTE "New Notation"
    - 在介绍SVM前，我们约定以后的 $y\in \{ -1,1\}$ , 以及分类器用w与b表示(更好表示斜率与节距)，并抛弃了 $x_0=1$
    
    $$h_{w,b}(x)=g(w^Tx+b)$$
    
    - 其中
    
    $$g(z)=\begin{cases}  1 \quad if \ z \geq 0\\\
    -1 \quad otherwise \end{cases}$$

## 1.Functional and geometric margins

### Functional margins
$$
	\hat{\gamma}^{(i)}=y^{(i)}(w^Tx+b)
$$

根据我们的分析，如果y=1,那么我们希望 $w^T+b$ 远大于0越好 ；如果y=-1，我们希望 $w^T+b$ 远小于0越好。那么不论如何 $\gamma$ 都会很大，但如果我们把 $\gamma$ 值的大小作为评定该系统的性能，又显得不太妥当，这是因为我们可以把w与b等比例放大来对系统进行做一个“欺骗”行为。所以我们一般将w与b单位化，有关于这部分内容将在后续呈现。

同时，**function margin** 被定义为

$$
\hat{\gamma}=\min_{i=1,...,m}\hat{\gamma}^{(i)}
$$

### Geometric margins
![](Attachments/ML_Note3%20Support%20Vector%20Machines_image_1.png)

如图，我们得到A点到直线的距离为

$$
\gamma^{(i)}=(\frac{w}{||w||})^Tx+\frac{b}{||w||}
$$

由于y的正负性，可以得到普遍的geometric margins为

$$
\gamma^{(i)}=y^{(i)}(\frac{w}{||w||})^Tx+\frac{b}{||w||}
$$

同时，**geometric margin**被定义为

$$
\gamma=\min_{i=1,...,m}\gamma^{(i)}
$$