# Chap 4 连续时间傅里叶变换（CTFT）

## 1. 概念跃迁：从“离散谐波”到“连续频谱密度”

对于周期信号 $x(t)$，傅里叶级数（FS）告诉我们：信号由一系列离散频率 $k\omega_0$ 的复指数信号叠加而成，系数为 $a_k$。

**Aha Moment：非周期信号怎么分解？**
如果一个信号是非周期的（比如只闪烁一次的脉冲），我们可以将其视为**周期 $T \to \infty$ 的周期信号**。
当 $T \to \infty$ 时，基波频率 $\omega_0 = 2\pi/T \to 0$。这意味着：

1. 离散的频率点 $k\omega_0$ 变得无限密集，最终连成了一片连续的频率变量 $\omega$。
2. 因为信号能量散布在无限长的时间里，单个频率的强度 $a_k \to 0$。但是，如果考查“单位频率带上的成分”（类似概率密度），它就成了一个有意义的连续函数。

这就极其自然地导出了**傅里叶变换对**：

$$
\begin{aligned}
X(j\omega) &= \int_{-\infty}^{\infty} x(t) e^{-j\omega t} \, \mathrm d t \quad &\text{(求连续频谱密度)} \\
x(t) &= \frac{1}{2\pi} \int_{-\infty}^{\infty} X(j\omega) e^{j\omega t} \, \mathrm d\omega \quad &\text{(用连续频率合成信号)}
\end{aligned}
$$

> **直觉条件反射**：看到 $X(j\omega)$，就要想到它是信号在频率 $\omega$ 处的“密度”。

---

## 2. 降维打击：用 CTFT 统一周期信号

既然 CTFT 是为了非周期信号发明的，那把周期信号塞进去会怎样？
周期信号（如纯正弦波）的频率是极其“纯粹”的。在连续的频率轴 $\omega$ 上，要表示这种绝对集中的频率分布，只能召唤**冲激函数 $\delta(\omega)$**。

对周期信号做 CTFT，其频域表现为一系列等间距的“钉子”（冲激函数）：

$$
X(j\omega) = 2\pi \sum_{k=-\infty}^{\infty} a_k \delta(\omega - k\omega_0)
$$

> **总结**：傅里叶变换是一个“大一统”理论。非周期信号对应平滑的连续曲线；周期信号对应离散的冲激钉子。

---

## 3. CTFT 的核心性质（时频联动的法则）

假设 $x(t) \overset{\mathcal F}{\longleftrightarrow} X(j\omega)$。这些性质不需要死记，它们是现实物理法则的数学投影：

1. **线性**：$\alpha x_1(t) + \beta x_2(t) \implies \alpha X_1(j\omega) + \beta X_2(j\omega)$
2. **时移**：$x(t-t_0) \implies e^{-j\omega t_0} X(j\omega)$
   > **直觉**：信号发生的时间推迟了，但它听起来的“音色”绝对没变（幅度 $|X(j\omega)|$ 没变），只是各个频率的波形起点变了（增加了一个线性相位偏移）。
3. **共轭与实信号**：$x^*(t) \implies X^*(-j\omega)$
   > **推论**：现实中能测量的信号大多是实信号，所以必然有 $X(j\omega) = X^*(-j\omega)$。也就是幅度偶对称，相位奇对称。
4. **微分与积分**：
   * $\frac{\mathrm dx}{\mathrm dt} \implies j\omega X(j\omega)$
   * $\int_{-\infty}^{t} x(\tau) \mathrm d\tau \implies \frac{X(j\omega)}{j\omega} + \pi X(0) \delta(\omega)$
   > **直觉**：微分是找突变，突变意味着高频，所以乘上 $j\omega$ 恰好能放大高频、压制低频（高通）。积分是平滑和累加，相当于除以 $j\omega$（低通），并且零频（直流偏置）的无限累积必须用一个 $\delta(\omega)$ 来补偿。
5. **时间缩放（测不准原理）**：$x(at) \implies \frac{1}{|a|} X\left(\frac{j\omega}{a}\right)$
   > **直觉**：把录音带快进（压缩时间，像手风琴一样捏紧），声音会变尖（频率展宽）。**信号不可能在时域和频域同时被压缩。**
6. **对偶性**：如果 $f(t) \leftrightarrow F(j\omega)$，那么 $F(t) \leftrightarrow 2\pi f(-\omega)$
   > **直觉**：时域和频域是高度对称的平行宇宙。时域里的某种形状，在频域一定也有对应的信号能长成这个形状。
7. **能量守恒（帕斯瓦尔定理）**：$\int |x(t)|^2 \mathrm d t = \frac{1}{2\pi} \int |X(j\omega)|^2 \mathrm d\omega$
   > **直觉**：无论是在时间长河里一点点算，还是按频率一块块算，总能量是不变的。

---

## 4. 卷积与乘积（工程应用的基石）

* **时域卷积定理（滤波的本质）**：$x(t) * h(t) \implies X(j\omega) H(j\omega)$
  > **条件反射**：看到时域系统卷积，立刻想到频域就是乘法！系统响应 $H(j\omega)$ 就是一个“面具（Filter）”，输入信号的频谱乘上这个面具，不需要的频率就被滤除了。
* **频域卷积定理（通信的本质）**：$x(t) h(t) \implies \frac{1}{2\pi} X(j\omega) * H(j\omega)$
  > **条件反射**：看到时域信号相乘（调制），立刻想到频谱发生了卷积平移。这就是 AM 广播的原理：用低频声音去乘高频载波，把声音的频谱“搬”到高频去发射。

---

## 5. 跨界打击：与常微分方程的关系

这是极其惊艳的一个结论！
对于线性常系数微分方程（LCCD）：

$$
\sum_{k=0}^N a_k\frac{\mathrm d^k y(t)}{\mathrm d t^k} = \sum_{k=0}^M b_k\frac{\mathrm d^k x(t)}{\mathrm d t^k}
$$

由于 CTFT 的微分性质（每次求导就是乘一个 $j\omega$），两边做傅里叶变换后，微积分瞬间变成了纯代数多项式！

$$
H(j\omega) = \frac{Y(j\omega)}{X(j\omega)} = \frac{\sum_{k=0}^M b_k (j\omega)^k}{\sum_{k=0}^N a_k (j\omega)^k}
$$

> **直觉**：有了傅里叶变换，我们**再也不用去解痛苦的微分方程了**。任何物理系统（电路、机械阻尼），只要写出微分方程，一眼就能写出它的频率响应 $H(j\omega)$（一个有理分式），进而分析出它是高通还是低通系统。

---

## 6. 四大“圣杯”傅里叶变换对

这四个变换对极其经典，完美展示了对偶性和缩放性质：

1. **冲激函数与常数（对偶的极点）**
   * $\delta(t) \overset{\mathcal F}{\longleftrightarrow} 1$
     *(时域极度压缩的“点”，意味着频域极其宽广，包含了所有频率，这叫“白噪声”。)*
   * $1 \overset{\mathcal F}{\longleftrightarrow} 2\pi \delta(\omega)$
     *(时域无限延伸的常数/直流电，在频域就是绝对纯粹的 0 频率“点”。)*

2. **矩形框与 Sinc 函数（测不准原理的完美体现）**

   $$
   \operatorname{rect}\left(\frac{t}{2a}\right) \overset{\mathcal F}{\longleftrightarrow} \frac{2\sin(a\omega)}{\omega} = 2a \operatorname{sinc}\left(\frac{a\omega}{\pi}\right)
   $$

   *(时域如果被框死（有明确的持续时间），频域就会变成无限延伸、不断振荡的 Sinc 波。注意：时域越窄，频域的 Sinc 主瓣就越宽！)*

3. **单边指数衰减（真实物理系统的常客）**

   $$
   e^{-at}u(t) \overset{\mathcal F}{\longleftrightarrow} \frac{1}{a + j\omega} \quad (a > 0)
   $$

   *(这是最典型的一阶 RC 低通电路的冲激响应。)*

