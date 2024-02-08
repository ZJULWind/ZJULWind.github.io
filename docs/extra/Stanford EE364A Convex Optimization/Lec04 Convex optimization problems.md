# Lec04 Convex optimization problems
## 1.Optimization problem 优化问题
### 1.1Optimization problem in standard form
![](Attachments/Lec04 Convex optimization problems_image_1.png)
#### option value
$$p^*= inf\{f_0(x) | f_i(x) ≤ 0, i = 1, . . . , m, h_i(x) = 0, i = 1, . . . , p\}$$

如果问题不可行，取 p* 为 ∞

如果问题无下界，取 p* 为-∞

如果x可行且 $f_i(x)=0$，我们称约束 $f_i(x)\leq 0$ 的第i个不等式x处起作用

### 1.2 Optimal and locally optimal points
#### feasible 
x is feasible if $x ∈ dom f_0$ and it satisfies the constraints  
a feasible x is optimal if $f_0(x) = p^*$;$X_{opt}$ is the set of optimal points
#### local optimal 
x is local optimal if there is an R>0 such that x is optimal for   
![](Attachments/Lec04 Convex optimization problems_image_2.png)

### 1.3 Implict constraints
we call the domain of the problem is   
![](Attachments/Lec04 Convex optimization problems_image_3.png)


---
## 2.Convex optimization  凸优化
### 2.1 standard form convex optimization problem 
![](Attachments/Lec04 Convex optimization problems_image_4.png)
!!! NOTE "important property:"
    - feasible set of a convex optimization problem is convex
### 2.2 Local and global optima

!!! NOTE "In fact"
    - any locally optimal point of a convex problem is (globally) optimal
### 2.3 Optimality criterion for differentiable f0
x is optimal if and only if it is feasible and

$$
∇f_0(x)^T (y - x) ≥ 0
$$

### 2.4 Equivalent convex problems
### Equivalent convex problems
![](Attachments/Lec04 Convex optimization problems_image_5.png)
### introducing equality constraints
![](Attachments/Lec04 Convex optimization problems_image_6.png)
### introducing slack variables for linear inequalities
![](Attachments/Lec04 Convex optimization problems_image_7.png)
### epigraph form 
![](Attachments/Lec04 Convex optimization problems_image_8.png)
### minimizing over some variables(partial optimate)
![](Attachments/Lec04 Convex optimization problems_image_9.png)

### 2.5 Quasiconvex optimization
when the $f_0$  is quaisconvex ,can have locally optimal points that are not globally optimal
### solution
![](Attachments/Lec04 Convex optimization problems_image_10.png)
![](Attachments/Lec04 Convex optimization problems_image_11.png)

---
## 3. Linear program 线性规划问题 
$$
minimize \  c^Tx+d
$$

$$
subject \ to \ Gx≼ h
$$

$$
Ax=b
$$

feasible set is a polyhedron.
### Linear-fractional program 线性分式规划问题
![](Attachments/Lec04 Convex optimization problems_image_12.png)

---
## 4.Quadratic program二次优化问题
### QP
目标函数为凸二次型，且约束函数为仿射。
![](Attachments/Lec04 Convex optimization problems_image_13.png)
### QCQP
不等式约束也是凸二次型，则是QCQP
![](Attachments/Lec04 Convex optimization problems_image_14.png)

### Sencond-order cone programming (SOCP)
![](Attachments/Lec04 Convex optimization problems_image_15.png)

---
## 5.Geometric programming几何规划
### monimal function and posyminal function
 ![](Attachments/Lec04 Convex optimization problems_image_16.png)
### GP
![](Attachments/Lec04 Convex optimization problems_image_17.png)

GP一般来说都不是凸问题，在此情况下可以转化为凸优化问题
#### solution 
$$
y_i=log\ x_i
$$

![](Attachments/Lec04 Convex optimization problems_image_18.png)

---
## 6.Generalized inequality constraints广义不等式约束
### convex problem with generalized inequality constraints
![](Attachments/Lec04 Convex optimization problems_image_19.png)
### conic form problem
![](Attachments/Lec04 Convex optimization problems_image_20.png)
### Semidefinite program (SDP)
![](Attachments/Lec04 Convex optimization problems_image_21.png)

---
## 7.Vector optimization向量优化
### general and convex vector optimization problem
![](Attachments/Lec04 Convex optimization problems_image_22.png)
