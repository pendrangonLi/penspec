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
alpha0,alpha1为n\*N数组 


