# 连续时间傅里叶变换（CTFT）

## 1. 从傅里叶级数到傅里叶变换

对周期信号 \(x(t)\)：
\[
a_k = \frac{1}{T} \int_{-T/2}^{T/2} x(t) e^{-jk\omega_0 t} \, dt
\]

当信号**非周期**时，周期 \(T \to \infty\)。注意：

- 公式中的 \(1/T \to 0\)，使得系数趋向零
- 积分项
\[
\int_{-T/2}^{T/2} x(t) e^{-jk\omega_0 t} \, dt
\]
在 \(T \to \infty\) 时形成连续频率函数。

于是自然定义**傅里叶变换**：
\[
X(j\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t} \, dt
\]

逆变换：
\[
x(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} X(j\omega) e^{j\omega t} \, d\omega
\]

> **直觉**：\(x(t)\) 可以看作由**连续频率** \(\omega\) 的复指数 \(e^{j\omega t}\) 叠加而成，每个频率的“权重”由 \(X(j\omega)\) 决定。

---

## 2. 周期信号的傅里叶变换视角

- 对周期信号，频率离散：\(k\omega_0\)
- 频域表现为**冲激函数**：
\[
X(j\omega) = 2\pi \sum_{k=-\infty}^{\infty} a_k \delta(\omega - k\omega_0)
\]

> **总结**：傅里叶变换是傅里叶级数的“连续推广”，离散频率 → 连续频率。

---

## 3. CTFT 的主要性质（直观理解）

假设 \(x(t) \overset{\mathcal F}{\longleftrightarrow} X(j\omega)\)：

1. **线性**  
\(\alpha x_1(t) + \beta x_2(t) \implies \alpha X_1(j\omega) + \beta X_2(j\omega)\)

2. **时移**  
\[
x(t-t_0) \implies e^{-j\omega t_0} X(j\omega)
\]

> 延迟信号 → 频域旋转因子

1. **共轭与实信号**  
\[
x^*(t) \implies X^*(-j\omega)
\]

- 如果 \(x(t)\) 实，\(X(j\omega)\) 关于频率中心对称

1. **微分与积分**  
\[
\frac{dx}{dt} \implies j\omega X(j\omega)
\]
\[
\int_{-\infty}^{t} x(\tau) d\tau \implies \frac{X(j\omega)}{j\omega} + \pi X(0) \delta(\omega)
\]

> 微分强调高频，积分强调低频；0 频率需特别处理

1. **时间缩放**  
\[
x(at) \implies \frac{1}{|a|} X\left(\frac{j\omega}{a}\right)
\]

> 压缩时间 → 展宽频率，拉伸时间 → 压缩频率

1. **对偶性**  
\[
x(t) \leftrightarrow X(j\omega) \implies X(t) \leftrightarrow 2\pi x(-\omega)
\]

> 时域与频域可互换角色

1. **能量守恒（帕斯瓦尔定理）**  
\[
\int |x(t)|^2 dt = \frac{1}{2\pi} \int |X(j\omega)|^2 d\omega
\]

> 能量在频域重新分配

---

## 4. 卷积与乘积直觉

- **卷积定理**  
\[
y(t) = x(t) * h(t) \implies Y(j\omega) = X(j\omega) H(j\omega)
\]

> 时域卷积 → 频域乘法，每个频率分量独立放大

- **乘积定理**  
\[
r(t) = x(t) h(t) \implies R(j\omega) = \frac{1}{2\pi} X(j\omega) * H(j\omega)
\]

> 时域乘积 → 频域卷积，频率分量混合

---

## 5. 与微分方程的关系

对于微分方程：
\[
\sum_{k=0}^N a_k\frac{d^k}{dt^k} y(t) = \sum_{k=0}^M b_k\frac{d^k}{dt^k} x(t)
\]

其频域表示：
\[
H(j\omega) = \frac{Y(j\omega)}{X(j\omega)} = \frac{\sum b_k (j\omega)^k}{\sum a_k (j\omega)^k}
\]

---

## 6. 重要傅里叶变换结果

1. **冲激函数**
\[
\delta(t) \overset{\mathcal F}{\longleftrightarrow} 1
\]

2. **常数函数**
\[
1(t) \overset{\mathcal F}{\longleftrightarrow} 2\pi \delta(\omega)
\]

3. **矩形函数**
\[
\operatorname{rect}\left(\frac{t}{2a}\right) =
\begin{cases}
1 & |t| < a\\
1/2 & |t| = a\\
0 & |t| > a
\end{cases}
\]
\[
\operatorname{rect}\left(\frac{t}{2a}\right) \overset{\mathcal F}{\longleftrightarrow} \frac{2\sin(a\omega)}{\omega}
\]

4. **指数衰减**

\[
e^{-at}u(t) \overset{\mathcal F}{\longleftrightarrow} \frac{1}{a + j\omega}
\]
