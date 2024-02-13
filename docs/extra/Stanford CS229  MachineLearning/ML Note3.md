# ML Note3 SVM
!!!NOTE "New Notation"
    - 在介绍SVM前，我们约定以后的 $y\in \{ -1,1\}$ , 以及分类器用w与b表示(更好表示斜率与节距)，并抛弃了 $x_0=1$
    
    $$h_{w,b}(x)=g(w^Tx+b)$$
    
    - 其中
    
    $$g(z)=\begin{cases}  1 \quad if \ z \geq 0\\\
    -1 \quad otherwise \end{cases}$$

## 1.Functional and geometric margins

### Functional margin 功能余量
$$
	\hat{\gamma}^{(i)}=y^{(i)}(w^Tx+b)
$$

根据我们的分析，如果y=1,那么我们希望 $w^T+b$ 远大于0越好 ；如果y=-1，我们希望 $w^T+b$ 远小于0越好。那么不论如何 $\gamma$ 都会很大，但如果我们把 $\gamma$ 值的大小作为评定该系统的性能，又显得不太妥当，这是因为我们可以把w与b等比例放大来对系统进行做一个“欺骗”行为。所以我们一般将w与b单位化，有关于这部分内容将在后续呈现。

同时，**function margin** 被定义为

$$
\hat{\gamma}=\min_{i=1,...,m}\hat{\gamma}^{(i)}
$$

### Geometric margins 几何余量
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

## 2.The optimal margin classifier
假设我们的训练集是可以线性分离的，也就是说我们可以用一个超平面来分离正与负。我们的目标是找到最大的几何余量。

接下来将介绍几种建立方式，不断对建立方式优化最后得出最终：

=== "第一种"
    建立以下的优化问题：
    
    $$
    \begin{align}
        \max_{\gamma,w,b}  & \quad \gamma\\
        s.t. & \quad y^{(i)}(w^Tx^{(i)}+b)\geq\gamma,i=1,..,m \\
        &\quad||w||=1
        \end{align}
    $$

    但是 $||w||=1$不是一个较好处理的问题（因为是非凸的）。

=== "第二种"
    根据几何余量与功能余量的关系，建立以下的优化问题：

    $$\begin{align}
    \max_{\gamma,w,b}  & \quad \frac{\hat{\gamma}}{||w||}\\
    s.t. & \quad y^{(i)}(w^Tx^{(i)}+b)\geq \hat{\gamma},i=1,..,m \\
    \end{align}$$

    但是，所求的 $\frac{\hat{\gamma}}{||w||}$同样也是非凸的

=== "**第三种（最终）**"
    根据我们上述的结论，功能余量可以根据w，b的取值等比例放缩。那么在第二种的基础上，令 $\hat{\gamma}=1$，建立以下优化问题：

    $$\begin{align}
    \max_{\gamma,w,b}  & \quad \frac{1}{||w||}\\
    s.t. & \quad y^{(i)}(w^Tx^{(i)}+b)\geq1,i=1,..,m \\
    \end{align}$$

    进一步优化：

    $$\begin{align}
    \max_{\gamma,w,b}  & \quad \frac{1}{2}||w||^2\\
    s.t. & \quad y^{(i)}(w^Tx^{(i)}+b)\geq1,i=1,..,m \\
    \end{align}$$

    这是一个具有凸二次目标和线性约束的优化问题。它的解给出了最优边际分类器。这个优化问题可以用商业的二次规划(QP)代码来解决

虽然说这个问题可以说解决了，但是我们经过讨论拉格朗日对偶性，可以通过kernels来让该决策器在更高维的问题中有更好的性能。

## 3.Lagrange duality
接下来将讲述如何寻找一个问题的对偶问题。
??? quote "回忆"

    考虑问题：

    $$\begin{align}
    \min_{w}  & \quad   f(w)            \\
    s.t. & \quad h_i(w)=0,i=1,..,l \\
    \end{align}$$

    使用**拉格朗日乘数法**来解决该问题：

    !!! NOTE  "拉格朗日乘数法"
        定义拉格朗日多项式为：

        $$L(w,\beta)=f(w)+\sum_{i=1}^l\beta_ih_i(w)$$

        当所有偏导数均为0时，就是问题的解

        $$\frac{\partial L}{\partial w_i}=0;\frac{\partial L}{\partial \beta_i}=0$$

类似地，做一个推广,考虑问题：

$$\begin{align}
\min_{w}  & \quad   f(w)            \\
s.t. & \quad g_i(w)\leq 0,i=1,...k\\
& \quad h_i(w)=0,i=1,..,l \\
\end{align}$$

我们定义广义的拉格朗日多项式

$$
L(w,\alpha,\beta)=f(w)+\sum_{i=1}^k\alpha_ig_i(w)+\sum_{i=1}^l\beta_ih_i(w)
$$

同时，我们给出两类问题：**原始问题与对偶问题**
=== "原始(primal)问题"
    $$
    \theta_P(w)=\max_{\alpha,\beta:\alpha_i\geq0}L(w\,,\alpha,\beta)
    $$

    可以发现

    $$
    \theta_P(w)=
    \begin{cases}
    f(w) \quad if \ w \ satisfies \ primal \ constraints\\
    \infty \quad otherwise
    \end{cases}
    $$

    那么，我们如果要求 $f(w)$ 的最小值，就是求
    $$
    \min_w \theta_P(w)=\min_w \max_{\alpha,\beta:\alpha_i\geq0}L(w\,,\alpha,\beta)
    $$

    规定 $p^*=\min_w \theta_P(w)$为原始问题的解。


=== "对偶(dual)问题"

    $$
    \theta_D(w)=\min_{w}L(w\,,\alpha,\beta)
    $$

    $$
    \max_{\alpha,\beta:\alpha_i\geq0}\theta_D(w)=\max_{\alpha,\beta:\alpha_i\geq0}\min_{w}L(w\,,\alpha,\beta)
    $$

    $$d^*=\max_{\alpha,\beta:\alpha_i\geq0}\theta_D(w)$$

---

很容易有 $d^*$ 与 $p^*$ 的关系

$$
d^*=\max_{\alpha,\beta:\alpha_i\geq0}\min_{w}L(w\,,\alpha,\beta)\leq \min_w \max_{\alpha,\beta:\alpha_i\geq0}L(w\,,\alpha,\beta)=p^*
$$

但是在一些条件限制下，我们可以有$d^*=p^*$，这样就可以用对偶问题来代替原始问题。以下是条件所在：

1. $f$ 和 $g_i$ 是凸的。
2. $h_i$ 是映射的。
3. $g_i$的限制是严格的（即 $g_i(w)<0$ ）
4. 原始问题的解 $w^*$ 与对偶问题的解 $\alpha^*,\beta^*$ 满足KKT条件![](Attachments/ML_Note3%20Support%20Vector%20Machines_image_2.png)

上面的等式（5）中又被称为KKT对偶互补条件。
## 4.Optimal margin classifiers
我们回归问题：

$$\begin{align}
\max_{\gamma,w,b}  & \quad \frac{1}{2}||w||^2\\
s.t. & \quad y^{(i)}(w^Tx^{(i)}+b)\geq1,i=1,..,m \\
\end{align}$$

我们可以写出限制

$$
g_i(w)=-y^{(i)}(w^Tx^{(i)}+b)+1\leq0.
$$

根据KKT对偶互补条件，如果要 $\alpha_i>0$ ，那么对应的功能余量 $y^{(i)}(w^Tx^{(i)}+b)$ 必须要为1,这样的向量就是支持向量。

为了建立合适的对偶问题，我们有一个准则就是尽量构造形如 $<x^{(i)},x^{(j)}>$ 的内积形式，这样就可以在后面的kernel形式中起到作用。
对于下面的问题找对偶问题：

$$
L(w; b; α) = \frac{1}{2}||w||_2 - \sum_{ i =1}^m α_i [y^{(i)}(w^Tx^{(i)}+b)-1]
$$

根据KKT条件，可以得到

$$
w=\sum_{i=1}^m \alpha_iy^{(i)}x^{(i)}
$$

$$
\sum_{i=1}^m \alpha_iy^{(i)}=0
$$

可以获得对偶问题如下：

![](Attachments/ML_Note3%20Support%20Vector%20Machines_image_3.png)

在这个问题中，我们只需要关注 $\alpha^*$ 的取值，随后可以得到 $w^*$ 的取值，回代也可以得到

$$
b^*=-\frac{1}{2}(\max_{i:y^{(i)}=-1}w^{*^T}x^{(i)}+\min_{i:y^{(i)}=11}w^{*^T}x^{(i)})
$$

在此之后,对于新加入的值x，只需要计算

$$
\begin{align}
w^Tx+b &=(\sum_{i=1}^m \alpha_iy^{(i)}x^{(i)})^Tx+b\\
&=\sum_{i=1}^m \alpha_iy^{(i)}<x^{(i)},x>+b
\end{align}
$$

如果这个值足够大，那么预测y=1.
## 5.Kernels
为了应对非线性边界，我们的做法是把它映射到高维，在高维重找到线性分割平面，在投射到低维。

x向量包含了输入的属性(attributes)，映射到高维后，对于映射后的向量，我们认为它包含了特性(features)。在此后，所有的x都会被换成 $\phi(x)$。

因为原来的算法都可以被写成内积的形式<x,z>，那么对于更换之后我们也经常会出现 $<\phi(x),\phi(z)>$，于是我们定义对每一个映射函数 $\phi$，它的核函数为

$$
K(x,z)=\phi(x)^T\phi(z)
$$

于是我们只需将原来的算法中的 $x^Tz$ 换成 $K(x,z)$ 。

可以给核函数一个比较直观的理解，就是两个向量的相似程度。

我们还可以注意到，使用核函数可以降低运算时间。

### Kernels的一般形式
一般形式

$$
K(x,z)=(c+x^Tz)^d
$$

参数c的出现使得映射函数拥有从低维到高维的维度变化。

如果我们需要映射后的维度尽可能大（甚至接近于无穷），需要使用到高斯核函数

$$
K(x,z)=exp(-\frac{||x-z||^2}{2\sigma^2})
$$

通过使用高斯核函数，可以作化简后用泰勒展开展开至无穷项数，实现了无穷维度。
### 如何判断某个核函数是否可用

引入**核矩阵**Kernel matrix：
$$
K_{ij} = K(x^{(i)}; x^{(j)}).
$$

!!! quote "Theorem (Mercer)"
    - 如果K将 $R^n\times R^n->R^n$ ,那么它可以称为一个核函数当且仅当：任选m个样本组成的核矩阵都是对称的且是正定的。

## 6.Regularization and the non-separable case

为了应对异常值出现的情况，我们对进行一些惩罚工作。

问题转化为

$$\begin{align}
\max_{\gamma,w,b}  & \quad \frac{1}{2}||w||^2+C\sum_{i=1}^m\xi_i\\
s.t. & \quad y^{(i)}(w^Tx^{(i)}+b)\geq1-\xi_i,i=1,..,m \\
& \quad \xi_i\geq0,i=1,..,m
\end{align}$$

它的对偶问题：

![](Attachments/ML_Note3%20Support%20Vector%20Machines_image_4.png)

KKT条件改为：

![](Attachments/ML_Note3%20Support%20Vector%20Machines_image_5.png)

关于如何使用算法解决，使用**SMO算法**
