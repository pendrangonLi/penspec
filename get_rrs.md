# caculate alpha and show spec
## get_alpha(omega_e, omega00, omega, Gamma, etdm, etdm_grad, FC0, FC1, HT0, HT1)
计算跃迁极化率
### 输入说明
omega_e: 浮点数，表示入射（角）频率
omega00: 浮点数，表示基态与激发态00能量差
omega: N\*1 数组，N为振动模式数量，表示振动频率
Gamma: 浮点数，表示展宽
etdm: 1\*3 数组
etdm_grad: N\*3 数组，N振动模式数量
FC0: n\*N 数组，n为最大振动量子数，N为振动模式数量
FC1: n\*N 数组，n为最大振动量子数，N为振动模式数量
HT0: n\*N\*N 数组，n为最大振动量子数，N为振动模式数量
HT1: n\*N\*N 数组，n为最大振动量子数，N为振动模式数量
### 函数实现
```


alpha0,alpha1为n*N*3数组 
alpha0 = etdm[np.newaxis, :,:] * FC0[:,:,np.newaxis] + np.sum(etdm_grad[np.newaxis, np.newaxis, :,:] * HT0[:,:,:,np.newaxis], axis=2)
alpha1 = etdm[np.newaxis, :,:] * FC1[:,:,np.newaxis] + np.sum(etdm_grad[np.newaxis, np.newaxis, :,:] * HT1[:,:,:,np.newaxis], axis=2)

alpha33 为 N*3*3数组
alpha33[k] = sum_n{np.outer(alpha0[n, k], alpha1[n, k]) * Gamma / sqrt((omega00 + omega[k]*n - omega)^2 + Gamma^2)}

alpha, a, b2, c2 为长度为N的一维数组
a[k] = np.trace(alpha33[k])
b2[k] = 0.5 * ((alpha33[k,0,0] - alpha33[k,1,1]) ** 2 + (alpha33[k,1,1] - alpha33[k,2,2]) ** 2 + (alpha33[k,2,2] - alpha33[k,0,0]) ** 2) + 0.75 * ((alpha33[k,0,1] + alpha33[k,1,0]) ** 2 + (alpha33[k,1,2] + alpha33[k,2,1]) ** 2 + (alpha33[k,2,0] + alpha33[k,0,2]) ** 2)
c2[k] = 0.75 * ((alpha33[k,0,1] - alpha33[k,1,0]) ** 2 + (alpha33[k,1,2] - alpha33[k,2,1]) ** 2 + (alpha33[k,2,0] - alpha33[k,0,2]) ** 2)

alpha = 45 * a ** 2 + 7 * b2 + 5 * c2

```
### 输出 alpha[:, np.newaxis]

## show_spec(omega, alpha, gamma, x)
展宽alpha为光谱
### 输入说明
```
omega: N*1 array 振动模式频率
alpha: N*1 array
gamma: 浮点数 rrs展宽
x: 一维数组 光谱范围
```
### 函数实现
```
I = np.sum(alpha * gamma / np.sqrt((omega - x) ** 2 + gamma ** 2， axis=0)
接下来要进行单位转化，x目前的单位时原子单位制(a.u.)下的角频率单位，需要将将其转化为对应的国际单位制下的波数(cm-1)，转化系数我已经准备好了在constant库中，总之x = x / constant.E_wavenum2au
D = np.hstack([x.reshape(-1,1), I])
保存D为文本文件
画出D[:,1]关于D[:,0]的图像
```
