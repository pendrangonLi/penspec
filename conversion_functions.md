# some function to convert variable
代码语言：python
## conversion_function0
该函数主要用于reshape输入数据，将其转变为方便运算的形式
输入变量有mass, omega, modes, force四个参数，输出新的mass, omega, modes, force。
调用形式是mass, omega, modes, force = conversion_function0(mass, omega, modes, force)
下面将介绍输入与输出变量的信息
### mass
mass是shape=N\*1的数组 N为原子数量，物理意义是原子的质量，需要将其reshape为一个3N\*3N的矩阵，矩阵只有主对角线上元素不为0，
主对角线上的值共有3N个其中第1-3个值等于原mass的第一个值，4-6对应原mass的第2个值，以此类推最后得到新的mass矩阵，记为mass1，对应关系为mass1[3i+k,3i+k]=mass[i,1];i=1,2,...,N;k=1,2,3;
### omega
omega是shape=(3N-6)\*1的数组 3N-6为自由度，物理意义是振动的角频率需要将其reshape为一个(3N-6)\*(3N-6)的矩阵
原来的数据在新矩阵的对角线上，矩阵其他元素为0。新omega记为omega1，对应关系为omega1[3i+k,3i+k]=omega[i,1];i=1,2,...,N;k=1,2,3;
### modes
modes是一个shape=(3N-6)\*N\*3的数组 3N-6对应振动模式数量 N对应原子，3对应x y z三个方向，物理意义是振动模式在原子各个方向上的分量
首先需要将其转化为3N\*(3N-6)的矩阵每一列对应原来的一个振动模式，第1，2，3行分别表示第一个原子的x,y,z分量，新modes记为modes1，这里直接说明modes1与modes的对应关系modes1[3i+k,j] = modes[j,i,k];i=1,2..,N;j=1,2...,3N-6;k=1,2,3;
### force
force是shape=N*3的数组 行对应原子，列对应x y z三个方向，需要转变为3N\*1的矩阵force1，对应关系为force[3i+k,1]=force[i, k];i=1,2,..,N;k=1,2,3;
### 注意
我写的ijk索引都是从1开始的如M[1,2]就表示矩阵M的第1行第2列的元素，再代码中索引是从0开始的，你可能得注意并避免这中间可能会导致的bug

## conversion_function1
这个函数用于计算无量纲振动模式L和振动模式的受力F
input: modes, mass, force
ouput: L, F
调用格式：
L, F = conversion_function1(modes, mass, force)
参数解释：
### modes 
振动模式，3N\*(3N-6)的矩阵，没一列表示一个振动模式
### mass
质量矩阵，3N\*3N的矩阵，只有主对角线上的元素不为0，对角线上的元素每三个表示同一个原子的质量
### force
受力矩阵，3N\*1的矩阵，依次为某原子在xyz方向的受力
### L, F的计算
记modes为$M_o$,mass为$M$,force为$F_x$有：

$L=M^{\frac{1}{2}}M_o$

$F = LM^{\frac{-1}{2}}F_x$

