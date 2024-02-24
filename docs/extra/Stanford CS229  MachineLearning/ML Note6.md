
在前面的情况中，我们都认为我们有足够的训练集数量来让我们识别数据中的多重高斯结构。但当样本的维度n远大于训练集的数量m时，前面的算法就很难起到好的作用。具体来说，样本只反应了低维度信息，并且得到的协方差矩阵也是不可逆的。
## 1.Restriction of $\Sigma$
如果我们没有足够的数据来拟合一个完整的协方差矩阵，我们可以 对我们将要考虑的矩阵空间施加一些限制。
### 拟合对角矩阵
考虑拟合一个对角矩阵，可以证明原矩阵的极大似然估计可以用以下的对角矩阵来拟合

$$
\Sigma_{jj}=\frac{1}{m}\sum_{i=1}^m(x_j^{(i)}-\mu_j)
$$

其中 $\mu=\frac{1}{m}\sum_{i=1}^mx^{(i)}.$

### 进一步约束
高斯密度的轮廓是椭圆，在有时候需要让对角元素相等，即 $\Sigma=\sigma^2I$ ,参数的极大似然估计用

$$
\sigma^2=\frac{1}{mn}\sum_{j=1}^n\sum_{i=1}^m(x_j^{(i)}-\mu_j)^2
$$

这样得到的密度图为圆形。

在上述提到的两个约束条件下，只需要 $m\geq 2$ 我们就可以获得非奇异的协方差矩阵 $\Sigma$.

然而，利用这样的对角化意味着我们把 $x_i$ ,$x_j$ 建模为不相关的。样本数据里实际上应该会包含一些相关的信息，如果这样对角化就让我们无法获得这个信息了。

我们需要提取有用特征----利用因子分析模型（Factor analysis）
## 2.Marginals and conditionals of Gaussians 
在因子分析前，我们先讲述联合多元高斯分布的条件分布和边际分布。我们建立以下假设：

![](Attachments/ML_Note6%20Factor%20analysis_image_1.png)

我们得到边际分布和条件分布

$$
\begin{equation}
x_1\sim N(\mu_1,\Sigma_{11}) \\
\end {equation}
$$

$$
\begin{equation}
x_1|x_2\sim N(\mu_{1|2},\Sigma_{1|2}) \\
\end {equation}
$$

其中

$$
\begin{align}
\mu_{1|2}&=\mu_1+\Sigma_{12}\Sigma_{22}^{-1}(x_2-\mu_2) \\
\Sigma_{1|2}& =\Sigma_{11}-\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}
\end {align}
$$

## 3.The Factor analysis model
接下来介绍因子分析模型，我们首先假设联合分布 $(x,z)$ 如下：

$$
\begin{align}
z&\sim N(0,I)\\
x|z&\sim N(\mu+\Lambda z,\Psi)
\end {align}
$$

其中，$z\in R^k$ 为一个隐性随机变量，$\mu \in R^n$ ，$\Lambda \in R^{n\times k}$，对角矩阵 $\Psi \in R^{n\times n}$,k的值一般比n小。所以在这样的假设下，每个数据点 $x^{(i)}$ 可以理解为是通过采取k维高斯变量 $z^{(i)}$产生并通过仿射、添加噪声得到。

同样可以这样表示

$$
\begin{align}
z&\sim N(0,I)\\
\epsilon &\sim N(0,\Psi)\\
x&=\mu+\Lambda z+\epsilon
\end {align}
$$

经过计算可以得到

$$
\begin{bmatrix}
z\\x
\end{bmatrix}\sim
N(
\begin{bmatrix}
0\\\mu
\end{bmatrix},
\begin{bmatrix}
I &\Lambda^T\\
\Lambda &\Lambda \Lambda ^T+\Psi
\end{bmatrix})
$$

于是得到

$$
x \sim N(\mu,\Lambda \Lambda ^T+\Psi)
$$

---

根据训练集，我们可以得到对数似然函数

$$
l(\mu,\Lambda,\Psi)=\log \prod_{i=1}^m
\frac{1}{(2\pi)^{n/2}|\Lambda \Lambda ^T+\Psi|^{1/2}}exp(-\frac{1}{2}(x^{(i)}-\mu)^T(\Lambda \Lambda ^T+\Psi)^{-1}(x^{(i)}-\mu))
$$

通过求导的方式求解是困难的，由此我们继续使用EM算法。
## 4.EM for factor analysis
EM算法的介绍见[The EM algorithm](https://zjulwind.github.io/extra/Stanford%20CS229%20%20MachineLearning/ML%20Note5/#3the-em-algorithm)


??? NOTE "因子分析 EM算法推导"
    ![](Attachments/ML_Note6%20Factor%20analysis_image_2.jpg)


