# 离散时间傅立叶变换（DTFT）

设离散时间信号为 $x[n]$，其离散时间傅立叶变换（Discrete-Time Fourier Transform, DTFT）定义为

$$
X(e^{j\omega})=\sum_{n=-\infty}^{\infty}x[n]e^{-j\omega n}
$$

逆变换为

$$
x[n]=\frac{1}{2\pi}\int_{-\pi}^{\pi}X(e^{j\omega})e^{j\omega n}\,d\omega
$$

由于 DTFT 具有 $2\pi$ 周期性，也可写成任意长度为 $2\pi$ 的积分区间。

---

# 常见信号的傅立叶变换

## 1. $x[n]=a^n u[n] \quad (|a|<1)$

$$
X(e^{j\omega})=\sum_{n=0}^{\infty}a^n e^{-j\omega n}
=\frac{1}{1-ae^{-j\omega}}
$$

---

## 2. $x[n]=a^{|n|}$

当 $|a|<1$ 时，

$$
X(e^{j\omega})
=\sum_{n=-\infty}^{\infty}a^{|n|}e^{-j\omega n}
=\frac{1-a^2}{1+a^2-2a\cos\omega}
$$

---

## 3. $x[n]=\delta[n]$

$$
X(e^{j\omega})=1
$$

---

## 4. $x[n]=\begin{cases}1, & |n|\le N\\0, & \text{otherwise}\end{cases}$

$$
X(e^{j\omega})
=\sum_{n=-N}^{N}e^{-j\omega n}
=\frac{\sin\left(\frac{(2N+1)\omega}{2}\right)}{\sin\left(\frac{\omega}{2}\right)}
$$

在 $\omega=0$ 处取极限，得到 $X(e^{j0})=2N+1$。

---

## 5. $X(e^{j\omega})=\begin{cases}1, & |\omega|<W\\0, & \text{otherwise}\end{cases}$

若定义

$$
\operatorname{sinc}(x)=\frac{\sin x}{x},
$$

则对应的时域信号为

$$
x[n]=\frac{W}{\pi}\operatorname{sinc}\left(Wn\right)
$$

---

## 6. $x[n]=1$

常数序列的 DTFT 为冲激列：

$$
X(e^{j\omega})=2\pi\sum_{k=-\infty}^{\infty}\delta(\omega-2\pi k)
$$

---

# 离散时间傅立叶变换的性质

设
$$
x[n]\overset{\mathcal{DTFT}}{\longleftrightarrow}X(e^{j\omega})
$$

## 1. 周期性

$$
X(e^{j(\omega+2\pi)})=X(e^{j\omega})
$$

---

## 2. 线性

若
$$
x_1[n]\leftrightarrow X_1(e^{j\omega}),\quad
x_2[n]\leftrightarrow X_2(e^{j\omega})
$$

则

$$
ax_1[n]+bx_2[n]\leftrightarrow
aX_1(e^{j\omega})+bX_2(e^{j\omega})
$$

---

## 3. 时移与频移

### 时移
若
$$
y[n]=x[n-n_0]
$$

则

$$
Y(e^{j\omega})=e^{-j\omega n_0}X(e^{j\omega})
$$

### 频移（调制）
若
$$
y[n]=e^{j\omega_0 n}x[n]
$$

则

$$
Y(e^{j\omega})=X(e^{j(\omega-\omega_0)})
$$

---

## 4. 时域反转

若
$$
y[n]=x[-n]
$$

则

$$
Y(e^{j\omega})=X(e^{-j\omega})
$$

---

## 5. 共轭与共轭对称性

若
$$
y[n]=x^*[n]
$$

则

$$
Y(e^{j\omega})=X^*(e^{-j\omega})
$$

若 $x[n]$ 为实序列，则有共轭对称性：

$$
X(e^{j\omega})=X^*(e^{-j\omega})
$$

因此实信号的幅度谱是偶函数，相位谱具有相应对称性。

---

## 6. 时域差分与累加

### 差分
若
$$
y[n]=x[n]-x[n-1]
$$

则

$$
Y(e^{j\omega})=(1-e^{-j\omega})X(e^{j\omega})
$$

### 累加
若
$$
y[n]=\sum_{k=-\infty}^{n}x[k]
$$

则在适当收敛条件下，

$$
Y(e^{j\omega})=\frac{X(e^{j\omega})}{1-e^{-j\omega}}
$$

注意：$\omega=0$ 处要结合信号具体性质讨论。

---

## 7. 时域内插（上采样）

若 $L$ 倍上采样定义为

$$
x_u[n]=
\begin{cases}
x[n/L], & n=0,\pm L,\pm 2L,\dots\\
0, & \text{otherwise}
\end{cases}
$$

则其 DTFT 为

$$
X_u(e^{j\omega})=X(e^{jL\omega})
$$

这会导致频谱在 $[-\pi,\pi]$ 内出现周期性重复。

---

## 8. 频率微分

若

$$
y[n]=n\,x[n]
$$

则

$$
Y(e^{j\omega})=j\frac{d}{d\omega}X(e^{j\omega})
$$

更一般地，

$$
n^m x[n]\leftrightarrow j^m\frac{d^m}{d\omega^m}X(e^{j\omega})
$$

---

## 9. Parseval 定理

若
$$
x[n]\leftrightarrow X(e^{j\omega}),\quad
y[n]\leftrightarrow Y(e^{j\omega})
$$

则有内积形式：

$$
\sum_{n=-\infty}^{\infty}x[n]y^*[n]
=
\frac{1}{2\pi}\int_{-\pi}^{\pi}X(e^{j\omega})Y^*(e^{j\omega})\,d\omega
$$

特别地，令 $y[n]=x[n]$，得到能量守恒公式：

$$
\sum_{n=-\infty}^{\infty}|x[n]|^2
=
\frac{1}{2\pi}\int_{-\pi}^{\pi}|X(e^{j\omega})|^2\,d\omega
$$

---

# 卷积性质

若
$$
x[n]\leftrightarrow X(e^{j\omega}),\quad
h[n]\leftrightarrow H(e^{j\omega})
$$

则时域卷积满足

$$
x[n]*h[n]\leftrightarrow X(e^{j\omega})H(e^{j\omega})
$$

其中

$$
(x*h)[n]=\sum_{k=-\infty}^{\infty}x[k]h[n-k]
$$

---

# 相乘性质

若
$$
y[n]=x[n]h[n]
$$

则频域中对应为周期卷积：

$$
Y(e^{j\omega})=\frac{1}{2\pi}\int_{-\pi}^{\pi}
X(e^{j\theta})H(e^{j(\omega-\theta)})\,d\theta
$$

也就是说，**时域相乘 $\leftrightarrow$ 频域卷积**。

---

# 对偶性质

## 1. DFS（离散傅立叶级数）的对偶

若 $x[n]$ 以 $N$ 为周期，其 DFS 系数为 $a_k$，则

$$
x[n]\leftrightarrow a_k
$$

并且有对偶关系

$$
a_n\leftrightarrow \frac{1}{N}x[-k]
$$

这里索引按 $N$ 周期理解。

---

## 2. DTFT 的相关对偶观点

DTFT 不是完全像 DFS 那样的“序列-序列”对偶，但可以记住：

- 时域与频域互为变换对；
- 时移对应频域乘线性相位；
- 频移对应时域乘复指数；
- 乘积对应卷积，卷积对应乘积。

---

# 由线性常系数差分方程表征的系统

设 LCCDE（linear constant-coefficient difference equation）为

$$
\sum_{k=0}^{N}a_k y[n-k]
=
\sum_{k=0}^{M}b_k x[n-k]
$$

通常记系统的传递函数为

$$
H(z)=\frac{Y(z)}{X(z)}
=\frac{b_0+b_1z^{-1}+\cdots+b_Mz^{-M}}
{a_0+a_1z^{-1}+\cdots+a_Nz^{-N}}
$$

若单位圆属于收敛域，则可在单位圆上取 DTFT，得到频率响应

$$
H(e^{j\omega})=\frac{B(e^{j\omega})}{A(e^{j\omega})}
$$

其中

$$
A(e^{j\omega})=\sum_{k=0}^{N}a_k e^{-j\omega k},\quad
B(e^{j\omega})=\sum_{k=0}^{M}b_k e^{-j\omega k}
$$

---

## 1. 零输入响应与零状态响应

系统输出可分为：

$$
y[n]=y_{zi}[n]+y_{zs}[n]
$$

- **零输入响应**：由初始条件引起
- **零状态响应**：由输入信号引起

在线性时不变系统中，零状态响应满足

$$
y_{zs}[n]=x[n]*h[n]
$$

其中 $h[n]$ 为系统的单位脉冲响应。

---

## 2. 稳定性与因果性

对于有理系统：

- **因果性**：$h[n]=0,\; n<0$
- **BIBO 稳定性**：$\sum_{n=-\infty}^{\infty}|h[n]|<\infty$

若系统是因果且有理，则稳定当且仅当所有极点都严格位于单位圆内。

---

## 3. 频率响应的求法

若系统的差分方程为

$$
y[n]-ay[n-1]=x[n]
$$

则

$$
H(z)=\frac{1}{1-az^{-1}}
$$

在单位圆 $z=e^{j\omega}$ 上，

$$
H(e^{j\omega})=\frac{1}{1-ae^{-j\omega}}
$$

这与前面的常见信号 $a^n u[n]$ 的 DTFT 一致。

---

# 常用记号

- $u[n]$：单位阶跃序列
- $\delta[n]$：单位冲激序列
- $\ast$：卷积
- $X(e^{j\omega})$：DTFT
- $H(e^{j\omega})$：频率响应
- $H(z)$：系统函数 / 传递函数

---

# 小结

DTFT 的核心记忆方式：

1. **时移 → 乘相位**
2. **调制 → 频移**
3. **卷积 → 乘积**
4. **乘积 → 周期卷积**
5. **差分 → 乘 $(1-e^{-j\omega})$**
6. **能量 → Parseval**
