# Chap 2：线性时不变系统（LTI Systems）

## 1. 卷积与单位元

- 对任意信号 $x(t)$：

  $$
  x(t) * \delta(t) = x(t)
  $$

  即 $\delta(t)$ 是卷积意义下的 **单位元**，具有阿贝尔群性质。

## 2. 冲激响应（Impulse Response）

- 对于线性时不变系统 $\mathcal{S}$：
  - 输入输出关系：$y(t) = \mathcal{S}(x(t))$
  - 冲激响应：$h(t) = \mathcal{S}(\delta(t))$
  - 输出可表示为卷积：

    $$
    y(t) = x(t) * h(t)
    $$

  > 系统只作用在卷积中的一个信号上。

## 3. LTI 系统分类

1. **无记忆 (Memoryless)**  
   - 条件：$t \neq 0$ 时 $h(t) = 0$
2. **可逆性 (Invertibility)**  
   - 条件：$h(t) * h^{-1}(t) = \delta(t)$
3. **因果性 (Causality)**  
   - 条件：$t < 0$ 时 $h(t) = 0$
4. **稳定性 (Stability)**  
   - 条件：$h(t)$ **绝对可和 / 绝对可积**（BIBO 稳定）

## 4. 奇异函数（Singular / Generalized Functions）

- **单位冲激函数**：$\delta(t)$  
- **单位跃迁函数**：$u(t)$  

### 扩展定义

- 定义单位冲激偶函数 $u_1(t)$：

  $$
  \frac{\mathrm d\, x(t)}{\mathrm d\, t} = x(t) * u_1(t)
  $$

- 类似地，定义 $u_k$ 为 $k$ 阶导数：
  - $u_0(t) = \delta(t)$  
  - $u_{-1}(t) = u(t)$  
  - **单位斜坡函数**：$u_{-2}(t) = u(t) * u(t) = t u(t)$
