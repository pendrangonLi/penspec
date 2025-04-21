# caculate alpha and show spec
## get_alpha(omega_e, omega00, omega, Gamma, etdm, etdm_grad, FC0, FC1, HT0, HT1)
计算跃迁极化率
### 输入说明
omega_e: 浮点数，表示入射（角）频率
omega00: 浮点数，表示基态与激发态00能量差
omega: N\*1 数组，N为振动模式数量，表示振动频率
etdm: 1\*3 数组
etdm_grad: N\*3 数组，N振动模式数量
FC0: n\*N 数组，n为最大振动量子数，N为振动模式数量
FC0: n\*N 数组，n为最大振动量子数，N为振动模式数量
HT0: n\*N\*N 数组，n为最大振动量子数，N为振动模式数量
HT0: n\*N\*N 数组，n为最大振动量子数，N为振动模式数量
### 函数实现
```
alpha0,alpha1为n*N*3数组 
alpha0[n, k] = etdm[0] * FC0[n, k] + sum_j{etdm_grad[j] * HT0[n, k, j]}
alpha1[n, k] = etdm[0] * FC1[n, k] + sum_j{etdm_grad[j] * HT1[n, k, j]}

alpha33 为 N*3*3数组
alpha33[k] = sum_n{np.outer(alpha0[n, k], alpha1[n, k]) / sqrt((omega00 + omega[k,0]*n - omega)^2 + Gamma^2)}

```
### 输出 alpha33

