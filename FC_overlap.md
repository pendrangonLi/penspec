# generate function to caculate FC overlap
使用语言： python
## FCFromZero(N, n, A, b, C, d, E)
计算<i_k|0>积分的函数，i=1-n;k=1-N; <br>
input: N, n, A, b, C, d, E <br>
output: FCfrom0 <br>
参数说明： <br>
### 输入参数
N: int 振动模式数量 <br>
n: int 振动激发态最大量子数 <br>
A,C,E: N\*N矩阵 <br>
b,d: N\*1矩阵 <br>
### 输出参数
FCfrom0: n\*N的矩阵
### 计算
FCfrom0[0,:] = 1 <br>
FCfrom0[1,k] = b[k,0] / sqrt(2) <br>
从第三行开始满足递推关系：<br>
`FCfrom0[i,k] = (b[k, 0] * FCfrom0[i-1,k] + sqrt(2 * (i - 1)) * A[k,k] * FCfrom0[i-2,k]) / sqrt(2 * i)`

## FCfromOne(FCfrom0, N, n, A, b, C, d, E)
计算<i_k|1_k>积分的函数，i=1-n;k=1-N; <br>
input: FCfrom0, N, n, A, b, C, d, E <br>
output: FCfrom0 <br>
参数说明： <br>
### 输入参数
FCfrom0：N*N矩阵 <br>
N: int 振动模式数量 <br>
n: int 振动激发态最大量子数 <br>
A,C,E: N\*N矩阵 <br>
b,d: N\*1矩阵 <br>
### 输出参数
FCfrom1: n\*N的矩阵
### 计算
FCfrom1[0,k] = b[k,0] / sqrt(2) <br>
从第二行开始满足：<br>
`FCfrom1[i,k] = (b[k,0]*FCfrom0[i,k] + sqrt(i/2)*E[k,k]*FCfrom0[i-1,k])/sqrt(2)`

## HTfromZero(FCfrom0, N, n, omega, A, b, C, d, E)
计算<i_k|Q_j|0>积分的函数，i=1-n;k=1-N,j=1-N; <br>
input: FCfrom0, N, n, omega, A, b, C, d, E <br>
output: HTfrom0 <br>
参数说明： <br>
### 输入参数
FCfrom0：N*N矩阵 <br>
N: int 振动模式数量 <br>
n: int 振动激发态最大量子数 <br>
omega: N\*1 矩阵 <br>
A,C,E: N\*N矩阵 <br>
b,d: N\*1矩阵 <br>
### 输出参数
HTfrom0: n\*N\*N的矩阵
### 计算
HTfrom0[0,k,j] = d[j,0] / sqrt(omega[j]) / 2 <br>
从第二行开始满足：<br>
`HTfrom0[i,k,j] = (d[j,0]*FCfrom0[i,k] + sqrt(i/2)*E[j,k]*FCfrom0[i-1,k]) / sqrt(omega[j]) / 2`

## HTfromOne(FCfrom0, FCfrom1, N, n, omega, A, b, C, d, E)
计算<i_k|Q_j|1_k>积分的函数，i=1-n;k=1-N,j=1-N; <br>
input: FCfrom0, FCfrom1, N, n, omega, A, b, C, d, E <br>
output: HTfrom1 <br>
参数说明： <br>
### 输入参数
FCfrom0, FCfrom1：N*N矩阵 <br>
N: int 振动模式数量 <br>
n: int 振动激发态最大量子数 <br>
omega: N\*1 矩阵 <br>
A,C,E: N\*N矩阵 <br>
b,d: N\*1矩阵 <br>
### 输出参数
HTfrom1: n\*N\*N的矩阵
### 计算
i=0, j!=k时: <br>
`HTfrom1[0,k,j] = (d[j,0] * FCfrom1[0,k] + (C[j,k]+C[k,j])*FCfrom0[0,k]/sqrt(2)) / sqrt(omega[j]) / 2 ` <br>
j=k时：<br>
`HTfrom1[0,k,j] = ((d[j,0] * FCfrom1[0,k] + (C[j,k]+C[k,j])*FCfrom0[0,k]/sqrt(2))*sqrt(2) + FCfrom0[0,k]) / sqrt(2*omega[j])  ` <br>
从i>0,j!=k开始满足：<br>
`HTfrom1[i,k,j] = (d[j,0] * FCfrom1[0,k] + (C[j,k]+C[k,j])*FCfrom0[0,k]/sqrt(2) + E[j,k]*FCfrom1[i-1,k]/sqrt(i/2)) / sqrt(omega[j]) / 2 ` <br>
j=k时：<br>
`HTfrom1[i,k,j] = ((d[j,0] * FCfrom1[0,k] + (C[j,k]+C[k,j])*FCfrom0[0,k]/sqrt(2) + E[j,k]*FCfrom1[i-1,k]/sqrt(i/2))*sqrt(2) + FCfrom0[i,k]) / sqrt(2*omega[j])  ` <br>
