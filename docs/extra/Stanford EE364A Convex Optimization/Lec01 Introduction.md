# Lec01 Introduction
·mathematical optimization
There exist some exceptions that can be solved efficiently and reliably.
## 1.Least-squares and Linear programming
### 1.1Least-squqres
To solve problems:

$$
minimize \quad  ||Ax-b||_2^2
$$

1. solution $x^*=(A^TA)^{-1}A^Tb$
2. is a reliable and efficient algorithm and software.
3. computation time proportional to $n^2k$ (where A belong to $R^{k\times n}$  )
### 1.2 Linear programming
To solve problems:

$$
minimize \quad c^Tx\\
$$

$$
subject \ to\quad a_i^Tx\leq b_i\quad i=1,2,...,m
$$

1. no analytical solution
2. also is a reliable and efficient algorithm and software.
3. computation time proportional to $n^2m$
## 2.Convex Optimization
To solve problems:

$$
minimize \quad f_0(x)\\
$$

$$
subject \ to\quad f_i(x)\leq b_i\quad i=1,2,...,m
$$

where the functions are convex:

!!!NOTE "Convex function"
    - 
    $$f_(αx + βy) ≤ αf_i(x) + βf_i(y)$$

    if α + β = 1, α ≥ 0, β ≥ 0


1. no analytical solution
2. reliable and efficient algorithms
3. computation time (roughly) proportional to max{n3, n2m, F }, where F is cost of evaluating fi’s and their first and second derivatives 