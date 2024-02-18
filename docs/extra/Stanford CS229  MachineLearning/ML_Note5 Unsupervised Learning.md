# 无监督学习
## 1.The k-means clustering algorithm
在聚类问题中，没有给定的y值。

k-means算法流程图如下：

![](Attachments/ML_Note5%20Unsupervised%20Learning_image_1.png)

事实上，就是不断地将样本点分配给最近的聚类中心 $c^{(i)}$ ，然后调整聚类中心的位置直到收敛。

![](Attachments/ML_Note5%20Unsupervised%20Learning_image_2.png)
### 收敛性
K-mean算法一定是收敛的。

定义**畸变函数**(distorion function)

$$
J(c, \mu) =\sum^m_{i=1} ||x^{(i)} - \mu_{c^{(i)}}||^2
$$

可以证明，k-means是J上的精确坐标下降，具体来说，k-means的内循环在保持µ固定的情况下反复使J相对于c最小化，然后在保持c固定的情况下使J相对于µ最小化。因此J必须单调减小，且J的值必须收敛。(通常，这意味着c和µ也会收敛)
## 2.Mixtures of Gaussians
### Mixtures of Gaussians
指定一个联合分布进行建模

$$
p(x^{(i)},z^{(i)})=p(x^{(i)}|z^{(i)})p(z^{(i)})
$$

在这里，$z\sim Multinomial(\phi)$（z可以取k个值，$\phi_j$ 表示z=j的概率，$\phi_j$之和为1）; $x^{(i)}|z^{(i)}=j \sim N(\mu_j,\Sigma_j)$。还需要说明的是，$z^{(i)}$是潜在随机变量（即他们的值是未知的），于是我们需要估计的参数就是 $\phi 与 \Sigma$。
### EM算法求解
推导发现，使用MLE并不能得到好的解析解，于是我们使用EM算法来逐步逼近似然函数的最大值。

## 3.The EM algorithm
前面我们跟已经展示了如何在混合高斯模型中使用EM算法，接下来将进行较为系统的阐述，来讲述如何用EM算法解决带有隐变量的问题。
### Jensen's inequality

!!!quote "琴生不等式"
    - 如果 $f$ 是一个凸函数，X是一个随机变量，那么
    $$ E[f(X)]\geq f(EX)$$
    - 且，如果 $f$ 是严格凸的，那么等号取等的条件当且仅当 $X=E[X]$
### The EM algorithm
对于存在隐变量的联合分布 $p(x,z)$ 似然函数为

$$
l(θ) =\sum^m_{i=1}
log \ p(x^{(i)}; θ)
=
\sum^m_{i=1}
log\sum_{z}
p(x^{(i)},z; θ):
$$

用最大似然估计无法获得解析解，EM算法的核心在于找到似然函数的下界，然后不断优化这一个下界。

对于每一个i，让 $Q_i$ 代表 z 的分布，利用琴生不等式(凸函数选取为log \ x) 

$$
\begin{align}
\sum_{i}log\sum_{z^{(i)}}p(x^{(i)},z^{(i)}; θ) &=   \sum_{i}log\sum_{z^{(i)}}Q_i(z^{(i)})\frac{p(x^{(i)},z^{(i)}; θ)}{Q_i(z^{(i)})} \\
& \geq \sum_{i}\sum_{z^{(i)}}Q_i(z^{(i)})log\frac{p(x^{(i)},z^{(i)}; θ)}{Q_i(z^{(i)})} 
\end{align}
$$

现在，我们需要讨论如何让这个下界越紧越好，关注琴生不等式的取等条件，我们需要

$$
\frac{p(x^{(i)},z^{(i)}; θ)}{Q_i(z^{(i)})} =c
$$

从事实上，

$$
Q_i(z^{(i)})=\frac{p(x^{(i)},z^{(i)}; θ)}{\sum_zp(x^{(i)},z^{(i)}; θ)}= \frac{p(x^{(i)},z^{(i)}; θ)}{p(x^{(i)}; θ)}=p(z^{(i)}|x^{(i)};\theta)
$$

所以选定好后我们进行EM算法

![](Attachments/Pasted%20image%2020240218130447.png)

经过证明，EM算法是收敛的。 

如果定义

$$
J(Q,\theta)=\sum_{i}\sum_{z^{(i)}}Q_i(z^{(i)})log\frac{p(x^{(i)},z^{(i)}; θ)}{Q_i(z^{(i)})} 
$$

EM算法实际就是J函数的不断上升，最终收敛。
### 解决混合高斯问题

=== "对于混合高斯模型，如果我们已知 $z^{(i)}$ "
    只需要取似然函数
    $$
    ℓ(\phi,\mu,Σ) =\sum^m_{i=1} log \ p(x^{(i)}|z^{(i)};\mu, Σ) + log \ p(z^{(i)}; \phi)
    $$

    就可以得到解：

    $$
    \begin{align}
    \phi_j &= \frac{1}{m}\sum^m_{i=1}1\{z^{(i)} = j\} \\
    \mu_j &=\frac{\sum^m_{i=1}1\{z^{(i)} = j\}x^{(i)}}{\sum^m_{i=1}1\{z^{(i)} = j\}}\\
    \Sigma_j &=\frac{\sum^m_{i=1}1\{z^{(i)} = j\}(x^{(i)}-\mu_j)(x^{(i)}-\mu_j)^T}
    {\sum^m_{i=1}1\{z^{(i)} = j\}}\\
    \end{align}
    $$

=== "如果用EM算法来解决"
    !!! note "使用EM算法来解决："
        ![](Attachments/ML_Note5%20Unsupervised%20Learning_image_3.png)
        ![](Attachments/ML_Note5%20Unsupervised%20Learning_image_4.png)
    E-step：

    $$
    w_j^{(i)}=Q_i(z^{(i)}=j)=P(z^{(i)}=j|x^{(i)};\phi,\mu,\Sigma)
    $$

    M-step:

    $$
    \begin{align}
    J(Q,\theta) & = \sum_{i}\sum_{z^{(i)}}Q_i(z^{(i)})\log\frac{p(x^{(i)},z^{(i)}; θ)}{Q_i(z^{(i)})} \\
    & =\sum_{i}\sum_{j=1}^kQ_i(z^{(i)}=j)\log\frac{p(x^{(i)},z^{(i)}=j; θ)}{Q_i(z^{(i)}=j)} \\
    & =\sum_{i}\sum_{j=1}^kw_j^{(i)}\log
    \frac{\frac{1}{(2\pi)^{n/2}|\Sigma_j|^{1/2}}exp(-\frac{1}{2}(x^{(i)}-\mu_j)^T\Sigma_j^{-1})(x^{(i)}-\mu_j)\cdot \phi_j}
    {w_j^{(i)}} \\
    \end{align}
    $$

    对 $\mu_l$ 求导并让导数为0

    $$
    \mu_j=\frac{\sum^m_{i=1}w_l^{(i)}x^{(i)}}{\sum^m_{i=1} w_l^{(i)}}
    $$

    同理可以获得 $\phi$ 和 $\Sigma$ .
