## 1.Signals
### 1.1Classification
**DT/CT**

**Real/Complex**

**Periodic/Aperiodic** 周期/非周期

**Casual/Anti-casual** 因果/非因果

**Right-/Left-sided**

**Bounded/Unbounded**

**Even/Odd**

#### Energy and Power
For CT signals:

$$
\begin{align}
E_{\infty}&=\lim_{T\to \infty}\int_{-T}^T|x(t)|^2dt=\int_{-\infty}^\infty|x(t)|^2dt \\
P_{\infty}&=\lim_{T\to \infty}\frac{1}{2T}\int_{-T}^T|x(t)|^2dt
\end{align}
$$

For DT signals:

$$
\begin{align}
E_{\infty}&=\lim_{N\to \infty}\sum_{n=-N}^{+N}|x[n]|^2dt=\sum_{n=-\infty}^{+\infty}|x[n]|^2 \\
P_{\infty}&=\lim_{N\to \infty}\frac{1}{2N+1}\sum_{n=-N}^N|x[n]|^2
\end{align}
$$

### 1.2Building-Block Signals
#### For DT signal

$$
\delta[n]=
\begin{cases}
1 \quad if \ n=0\\
0 \quad otherwise
\end{cases}
$$

#### For CT signal
Unit-Impulse signal

![](Attachments/1_Introduction_image_1.png)
Unit-Step signal

$$
u(t)=\int_{-\infty}^t\delta(\lambda)d\lambda=
\begin{cases}
1 \quad if \ t\geq 0\\
0 \quad otherwise
\end{cases}
$$

### 1.3Transformations of time
Time **shift/reversal/scaling**

---


## 2.Systems
### 2.1Classification
**with/without memory**

**Stable/Non-stable**

**Causal/Noncausal**
: A system is **casual** if the output at time $t_0$ depends only on the input for $t\leq t_0$
判断系统是否是因果的，只需要判断x(·)的因变量是否永远小于等于y(·)

**Time-invariant**时不变
: 判据：t在x()里，且只能是t

**Linear**
: 判据：所有项都有x，且都是一次