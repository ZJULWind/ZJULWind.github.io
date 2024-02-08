# Lec02 Convex sets
## 1.Affine and Convex sets
#### Line:
all point x 
$$
x=\theta x_1+(1-\theta )x_2 
$$

#### Line segment:
line that the

$$
0 \leq \theta \leq1
$$

#### Affine set:
for any two distinct points in the set , exist a line.
	every affine set can be expressed as solution of system of linear equations.
#### Convex combination and convex hull
![](Attachments/Lec02%20Convex%20sets_image_1.png)

convex hull 仿射包，记为aff C。
仿射包是包含C的最小仿射集合，或者我们可以理解为壳。

### 仿射维数与相对内部
定义C的仿射维数为其仿射包的维数

!!! question  "相对内部与相对边界"
	- ![](Attachments/Lec02%20Convex%20sets_image_2.png)

### Convex set:
for any two distinct points in the set ,exist a line setment.
### Convex cone 
#### conic combination 锥组合

$$
x=\theta_1x_1+\theta_2x_2
$$

with $\theta_1\geq 0, \theta_2\geq 0$
#### convex cone 凸锥
set that contains all conic combination of points in the set.
#### 锥包
集合C的锥包为C中元素的所有锥组合的集合。


---

## 2.Some important examples
### 2.1Hyperplanes and Halfspaces
#### Hyperplane
set of the form $\{x|a^Tx=b\}(a\neq 0)$
#### Halfpspaces
set of the form $\{x|a^Tx\leq b\}(a\neq 0)$

1. a is a normal vector
2. hyperplanes are affine and convex; halfspaces are convex
### 2.2 Euclidean balls and Ellipsoids

#### (Euclidean) Ball 

with center $x_c$ and radius $r$:

$$B(x_c, r) =\{x |\ ||x - x_c||_2 ≤ r\} = \{x_c + ru\ |\  ||u||_2 ≤ 1\}$$

#### Ellipsoid: 
set of the form:

$$
\{x | (x - x_c)^T P^{ -1}(x - x_c) ≤ 1\}
$$

with $P ∈ S^n _{++}$(i.e., P symmetric positive definite)

other representation: $\{xc + Au | \ ||u||_2 ≤ 1\}$ with A square and nonsingular
### 2.3 Norm balls and norm cones
#### norm
a function ||·|| that satisfies

1. $||x||≥ 0;||x|| = 0$ if and only if $x = 0$ 
2. $||tx||= |t|||x||$ for $t ∈ R$ 
3. $||x+y|| ≤ ||x|| + ||y||$
#### norm ball
with center $x_c$ and radius r:

$$
\{x | ||x - x_c|| ≤ r\}
$$
#### norm cone: 

$$\{(x, t) | ||x|| ≤ t\}\subseteq R^{n+1}$$

Euclidean norm cone is called secondorder cone

norm balls and cones are convex
## 2.4 Polyhedra 多面体
![](Attachments/Lec02%20Convex%20sets_image_3.png)
#### 单纯形

!!! question  "Title"
	- Contents

## 2.5 Positive semidefinite cone
some notations  
![](Attachments/Lec02%20Convex%20sets_image_4.png)

---

## 3.Operations that preserve convexity
### 3.1 intersection 交集
the intersection of (any number of) convex sets is conve
### 3.2 affine functions
![](Attachments/Lec02%20Convex%20sets_image_5.png)

!!! example  "Exmaple"
   -  Scaling 放缩 Translation平移 Projection 投影
   -  加法 直积 部分和 
   -  线性矩阵不等式的解是凸集
   -  双曲锥是凸集
### 3.3 perspective and linear-fractional function
#### Perspective funtcion

$P:R^{n+1}→R^n$

$$P (x, t) = x/t, dom P = \{(x, t) | t > 0\}$$

images and inverse images of convex sets under perspective are convex. 这说明了domP 的子集C如果是凸集，那么他的象也是凸集。

透视函数可以理解为，规范化使得最后一维的分量为1，然后舍弃他。
#### Linear-fractional
$f : R^n → R^m:$

$$f(x) = \frac{Ax + b}{c^T x + d},\quad dom \ f = \{x | c^T x + d > 0\}$$

images and inverse images of convex sets under linear-fractional functions are convex

---

## 4.Generalized Inequalities 
### 4.1Proper cone and generalized inequalities
#### proper cone 
a convex cone K is a proper cone if 

1. K is closed 
2. K is solid 
3. K is pointed - which means K contains no line 
#### generalized inequalities
suppose K is a proper cone,we define 

$$
x ≼_K y \iff y-x \in K
$$

to be more strict
$$
x ≺_K y \iff y-x \in  int \  K
$$

!!! Example  "Examples"
	- 非负象限及分量不等式
	- 半正定锥及矩阵不等式
	- \[0.1\]上的多项式锥

!!! NOTe  "Properties"
	- ![](Attachments/Lec02%20Convex%20sets_image_6.png)
	- ![](Attachments/Lec02%20Convex%20sets_image_7.png)
### 4.2 Minimum and minimal elements
#### minimum elements
$x ∈ S$ is the minimum element of S with respect to $≼_K$if

$$y ∈ S ⇒ x ≼_K y$$
#### minimal element
$x ∈ S$ is a minimal element of S with respect to $≼_K$ if

$$
y ∈ S, y ≼_K x ⇒ y = x
$$

!!! Example  集合符号语言且建立在$R_+^2$上的一个例子
	- 首先，用简单的集合符号我们可以让 $x\in S$，目标是如何判断x是否是最小元/极小元。
	- 1.如果 $S\subseteq x+K$，那么x是最小元
	- 2.如果 $(x-K)\cap S = \{x\}$，那么x是极小元
	- 示意图如下
	- ![](Attachments/Lec02%20Convex%20sets_image_8.png)

---

## 5.Separating and supporting hyperplane 
### 5.1 Separating hyperplane theorem
if C and D are disjoint convex sets, then there exists $a \neq 0$, b such that

$$a^T x ≤ b \ for\  x ∈ C, a^T x ≥ b \ for\  x ∈ D$$

then we can say the hyperplane $\{x | a^T x = b\}$ separates C and D

 question  Deeper learning
	- 超平面分离定理的证明、严格分离、逆定理……

### 5.2 Supporting hyperplane theorem
#### hyperplane 
suppose $x_0$ is a point on the boundary of C,if for any $x\in C$,
$$
a^Tx\leq a^Tx_0
$$
then we can say hyperplane 
$$
\{x|a^Tx=a^Tx_0\}
$$
is a supporting hyperplane of C at point $x_0$
#### Supporting hyperplane theorem
if C is convex, then there exists a supporting hyperplane at every boundary point of C

---

## 6. Dual cones and generalized inequalities
#### Dual cone $K^*$
$$
K^*=\{y | y^T x ≥ 0 \ for \ all \ x ∈ K\}
$$
!!! Example Examples
	- $K = R^n_+: K^∗ = R^n _+$
$K = S^n_+: K^∗ = S^n _+$
 $K = \{(x, t) | ||x||_2 ≤ t\}: K^∗ = \{(x, t) | ||x||_2 ≤ t\}$
$K = \{(x, t) | ||x||_1 ≤ t\}: K^∗ = \{(x, t) | ||x||_∞ ≤ t\}$
	- first three examples are self-dual cones

!!! NOTE "一些性质"
	- 对偶锥总是凸的，即使K不是凸锥
	- 如果 $K_1 \subseteq K_2$,那么 $K_2^* \subseteq K_1^*$
	- 如果K有非空内部，那么$K^*$ 是尖的
	- 如果K 的闭包是尖的，那么$K^*$ 必有非空内部
	- $K^{**}$ 是K的凸包的闭包，因此如果K是凸的且是闭的，那么$K^{**}$ = K
	- 这些最终说明了 如果K是一个proper cone 那么它的对偶锥也是，进一步有$K^{**}$ = K
#### Dual generalized inequalities

$$
y ≽_{K^*} 0 \iff  y^T x ≥ 0 \ for\  all \ x ≽_K 0
$$
### Minimum and minimal elements via dual inequalities
#### mininum element 
x is minimum element of S iff for all $λ ≻_{K^∗} 0$, x is the unique minimizer of $λ^T z$ over S

从几何上来看，这样意味着对于任意  $λ ≻_{K^∗} 0$，超平面 $\{z|\ \lambda ^T(z-x)=0\}$是x在S的一个严格支撑超平面
#### minimal elements
if x minimizes $λ^T z$ over S for some $λ ≻_{K^∗} 0$, then x is minimal.
