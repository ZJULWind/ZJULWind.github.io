# ML Note1
线性的规划中，假设函数（hypothesis）被设定为

$$
h(x)=\sum_{i=1}^n \theta _i x_i=\theta ^T x
$$

损失函数(cost function)

$$
J(\theta)=\frac{1}{2}\sum_{i=1}^{m}(h(x^{(i)})-y^{(i)})
$$
## 1.LMS algorithm
取一个 $\theta$ 使得 J 最小。
### Batch gradient descent
![](Attachments/ML%20Note1_image_1.png)

$\alpha：learning\ rate$
### Stochastic gradient descent
![](Attachments/ML%20Note1_image_2.png)

!!!NOTE "二者比较"
    - Batch是可以得到收敛解的，而stochastic大概率会在最优解处振荡。但是后者可以较好处理大数据情况

## 2.The normal equations

!!! NOTE "矩阵的求导"
    - ![](Attachments/ML%20Note1_image_3.png)

!!! NOTE "矩阵迹的基本性质"
    - $$\begin{cases}
    trABC = trCAB = trBCA\\
    trABCD = trDABC = trCDAB = trBCDA\\
    trA = trA^T\\
    tr(A + B) = trA + trB\\
    tr\ aA = a\ trA
    \end{cases}
    $$

!!! NOTE "矩阵的迹与微分的关系"
    -![](Attachments/ML%20Note1_image_4.png)

#### The normal equations

$$
X^T Xθ = X^Ty
$$

$$
θ = (X^T X)^{-1}X^Ty.
$$

## 3.Probabilistic interpretation
从概率角度解释：为什么最小二乘损失函数J是一个比较好的选择？  

假设

$$y^{(i)}=\theta^Tx^{(i)}+\epsilon^{(i)}$$

并假设 $\epsilon^{(i)}$ 的分布为

$$p(\epsilon^{(i)})=\frac{1}{\sqrt{2\pi}\sigma}exp(-\frac{(y^{(i)}-\theta^Tx^{(i)})^2}{2\sigma^2})$$

极大似然估计函数为

$$L(\theta)=\prod_{i=1}^{m}\frac{1}{\sqrt{2\pi}\sigma}exp(-\frac{(y^{(i)}-\theta^Tx^{(i)})^2}{2\sigma^2})$$

取对数后，发现实际就是求最小值

$$J(\theta)=\frac{1}{2}\sum_{i=1}^{m}(h(x^{(i)})-y^{(i)})$$

## 4.Locally weighted regression
Fit $\theta$ to minimize 

$$\sum_{i=1}^{m}w^{(i)}(y^{(i)}-\theta^Tx^{(i)})^2$$

where $w^{(i)}$ is defined by 

$$w^{(i)}=exp\{-\frac{(x^{(i)}-x)^2}{2\tau^2}\}$$

τ is called the **bandwidth parameter**
## 5.Logistic regression
·针对的是binary classification problem。
### 新的假设函数
对于分类型问题，线性最小二乘并没那么有效。  

我们引入一个Logistic funtcion 

$$g(z)=\frac{1}{1+e^{-z}}$$

!!! NOTE "g(z)的一个性质"
    - $$g'(z)=g(z)g(1-z)$$

选择新的假设函数

$$h_\theta(x)=g(\theta^Tx)=\frac{1}{1+e^{-\theta^Tx}}$$

### 解决思路
假设

$$
P(y=1|x;\theta)=h_\theta(x)
$$

$$
P(y=0|x;\theta)=1-h_\theta(x)
$$

那么

$$P(y|x;\theta)=h^y_\theta(x)(1-h_\theta(x))^{1-y}$$

最大似然函数 

![](Attachments/ML%20Note1_image_5.png)  

这里，我们是要求似然函数的最大值，所以采取梯度上升

$$
\theta:=\theta+\alpha\nabla_\thetaℓ(θ)
$$

$$
\theta_j:=\theta_j+\alpha(y^{(i)}-h(x^{(i)}))x_j^{(i)}
$$
## 6.Another algorithm for maximizing $ℓ(θ)$
### Newtown's method
牛顿方法是一种找零点的方法。  

对某些函数 $f : R → R$ ,选取一个 $\theta_0$ ，逐步下降最后趋近于0  

$$
\theta:=\theta-\frac{f(\theta)}{f'(\theta)}
$$
### 应用
注意到：在$ℓ(θ)$的最大点处，$ℓ'(θ)=0$ 。利用这一点我们得到更新方案

$$
\theta:=\theta-\frac{ℓ'(θ)}{ℓ'’(θ)}
$$
### 推广
如果 $\theta$ 是一个多维的向量，那么更新方案改为

$$θ := θ - H^{-1}∇_θℓ(θ).$$

其中H是Hessian矩阵，

$$H_{ij}=\frac{\partial^2ℓ(θ).}{\partial \theta_i \partial \theta_j}$$




