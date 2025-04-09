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
`FCfrom0[i,k] = (b[k, 0] * FCfrom0[i-1,k] + sqrt(2 * (i - 1)) * A[k,k] * FCfrom0[i-2,k]) / sqrt(2 * k)`
