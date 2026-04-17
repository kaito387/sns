## 离散时间傅立叶变换

$$
X(e^{j\omega}) = \sum_{n=-\infty}^{\infty} x[n]e^{-j\omega n}
$$

逆变换
$$
x[n] = \int_{2\pi} X(e^{j\omega}) e^{j\omega n} \mathrm d\omega
$$

## 常见信号的傅立叶变换

### 1. $x[n] = a^n u[n]~(|a| < 1)$

$$
X(e^{j\omega}) = \frac{1}{1-ae^{-j\omega}}
$$

### 2. $x[n] = a^{|n|}$

\[
X(e^{j\omega}) = \frac{1-a^2}{1+a^2-2a\cos \omega}
\]

### 3. $x[n] = \delta[n]$

\[
X(e^{j\omega}) =1
\]

### 4. $x[n] = [|n| \le N]$

\[
X(e^{j\omega}) = \frac{\sin\left[(2N+1)\omega/2\right]}{\sin(\omega/2)}
\]

### 5. $X(e^{j\omega}) = [|\omega| < W]$

\[
x[n] = \frac{W}{\pi}\operatorname{sinc}\left(\frac{Wn}{\pi}\right)
\]

### 6. $x[n] = 1$

\[
X(e^{j\omega}) = 2\pi\sum_{l=-\infty}^{\infty} \delta(\omega - 2\pi l)
\]

## 离散时间傅利叶变换的性质

1. 周期性
2. 线性
3. 时移与频移
4. 时域反转
5. 共轭与共轭对称性
6. 时域差分与累加
7. 时域内插
8. 频率微分
9. Parseval 定理

## 卷积性质

若 $x[n]\overset{\mathcal{DTFT}}\longleftrightarrow X(e^{j\omega})$，$h[n]\overset{\mathcal{DTFT}}\longleftrightarrow H(e^{j\omega})$，则
\[
x[n]*h[n] \overset{\mathcal{DTFT}}\longleftrightarrow X(e^{j\omega})H(e^{j\omega})
\]

## 相乘性质

## 对偶性质

$$
x[n] \overset{\mathcal{DFS}}\longleftrightarrow a_k
$$

$$
a_n \overset{\mathcal{DFS}}\longleftrightarrow \frac{1}{N} x[-k]
$$

\[
x[n]\overset{\mathcal{DTFT}}\longleftrightarrow X(e^{j\omega})
\]

\[
X(e^{j\omega}) \overset{\mathcal{DFS}}\longleftrightarrow x[-k]
\]

