假设现在的情况中，样本集中的数据中的某两个（或多个）分量是具有较强的关联性的，以至于整个样本空间可以降维，我们使用主成分分析（Principal Components Analysis）来解决。

可以有一个较为直观的认知，就是数据点基本都按照一个轴分布，少数有噪声出现在轴附近

![](Attachments/ML_Note7%20PCA_image_1.png)

在进行PCA前，先对随机变量进行标准化

![](Attachments/ML_Note7%20PCA_image_2.png)

假设标准化后的样本集如下：

![](Attachments/ML_Note7%20PCA_image_3.png)

如何找到合适的u（轴）向量呢？我们先选取两个单位向量，关注他们的投影，可以看到第一个取法的投影数据的方差比较大，这是我们想要的。
=== "第一种"
    ![](Attachments/ML_Note7%20PCA_image_4.png)
=== "第二种"
    ![](Attachments/ML_Note7%20PCA_image_5.png)

为了规范化取向量 $u(||u||=1)$ 的标准，我们求

$$
\max \frac{1}{m}\sum_{i=1}^m(x^{(i)^T}u)^2
=\max u^T(\frac{1}{m}\sum_{i=1}^m x^{(i)}x^{(i)^T})u
$$

令$\Sigma=\frac{1}{m}\sum_{i=1}^m x^{(i)}x^{(i)^T}$

总的来说，如果要用一个一维向量来近似数据，就选 $\Sigma$ 的主特征向量；如果要投影到一个k维子空间，就选k个特征向量（由此构成了一组正交基），对应地，如果要表示 $x^{(i)}$ 就使用

$$
y^{(i)}=
\begin{bmatrix}
u_1^Tx^{(i)}\\
u_2^Tx^{(i)}\\
...\\
u_k^Tx^{(i)}
\end{bmatrix}
\in R^k
$$

作为 $x^{(i)}$ 的一个近似，所以$x^{(i)}$就被降低到了k维。