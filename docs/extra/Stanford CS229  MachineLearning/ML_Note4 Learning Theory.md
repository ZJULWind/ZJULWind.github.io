
## 1.Bias\/variance tradeoff

## 2.Regularization and model selection
在前面的内容里，我们已经学习了很多模型，那么在面对一个样本集的时候，如何选取最好的模型来进行拟合？

定义模型集
$$
M=\{M_1,...M_d\}
$$

$M_i$可以是我们谈论过的任意模型。
### Cross validation
一个很自然的想法是

1. 对于样本集S，对每个 $M_i$ 进行学习，获得一些  $h_i$.
2. 选择具有最小误差的那个算法。

但是这个想法是不可行的，拿多项式来举例，对于更高阶数的多项式拟合，拟合后的误差虽然小了，但是方差变大了，这是我们不想看到的，于是有以下的交叉验证

!!! NOTE  "交叉验证"
    1. 随机将样本集S分为 $S_{train}$ 和 $S_{CV}$（可以叫它保留交叉验证集）
    2. 对每个模型，仅对训练集进行训练，获得 $h_i$
    3. 使用保留交叉检验集 $S_{CV}$ 进行检验，输出误差最小的一个模型。

这个验证方法的缺点在于，它损失了30%的数据，如果样本数比较少的话，那么很有可能导致训练集数据比较少，拟合结果随即变差。

!!! NOTE  "K折交叉验证"
    1. 将样本集分为k份， $S_1,...,S_k$
    2. 对于每一个模型，利用以下方法来评估
    	1. 选择一个样本集 $S_j$ ，对除本样本集$S_j$以外的所有样本集进行训练，最后拿$S_j$获得误差 $\hat{\varepsilon}_{S_j}(h_{ij})$ 。
     	2. 最后对于 $M_i$ 的泛化误差，就采用$\hat{\varepsilon}_{S_j}(h_{ij})$的平均值
    3. 选择估计泛化误差最小的模型 $M_i$ ，并在整个训练集S上重新训练该模型，然后输出结果假设 作为我们的最终答案。

k=10是一个比较常见的选择，但是我们如果在样本数极小的情况下，令m=k，这种被称为留一交叉验证(leave-one-out cross validation)

### Feature Selection
当你认为样本数量过多但输出特性只与少数变量有关时，那么如果采取上述的方法很有可能会造成过拟合的现象，

!!! NOTE  "正向搜索(forward search)"
    - ![](Attachments/ML_Note4%20Learning%20Theory_image_1.png)
    - 结束循环的条件可以设定为特征数达到一定数量
    - 除此之外，还有反向搜索(backward search)

但是我们在这个方法中频繁做添加/删减特征然后重新评估性能的动作，这其实是费时的。

!!! NOTE "Filter feature selectio"
    - 核心思想是利用分数 $S(i)$ 来衡量每个特征 $x_i$ 对于y的信息含量大小，然后选取最大的k个。
    - 实际中较常见地取互信息(mutual information)来衡量：

    $$MI(x_i,y)=\sum_{x_i\in \{0,1\} }\sum_{y\in \{0,1\} } p( x_i,y) log \frac{p(x_i,y)}{p(x_i)p(y)} $$

    - 上面的方程假设xi和y是二值的;更一般地求和将在变量的域上
    - 还可以用KL散度来表示
    $$MI(x_i,y)=KL( p( x_i,y) || p(x_i)p(y)) $$

### Bayesian statistics and regularization
利用贝叶斯视角能更好解决过拟合的情况，贝叶斯视角下，把需要衡量的 $\theta$ 视为一个随机变量，在这个情况下有一个先验概率 $p(\theta)$ ，那么

$$
\begin{align}
p(\theta|S)&= \frac{p(S|\theta)p(\theta)}{p(S)} \\
&=\frac{\prod_{i=1}^mp(y^{(i)}|x^{(i)},\theta)p(\theta)}{\int_\theta (\prod_{i=1}^mp(y^{(i)}|x^{(i)},\theta)p(\theta))d\theta}
\end{align}
$$

实质上,p(S)是一个常数，那么MAP问题的解为

$$
\theta_{MAP}=\arg \max_\theta \prod_{i=1}^mp(y^{(i)}|x^{(i)},\theta)p(\theta)
$$

在实际问题中，一般先假设

$$
θ ∼ N(0; τ ^2I)
$$
