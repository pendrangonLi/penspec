# generate some function to read basis info
使用python完成以下函数，不准用re库的正则表达式
## function table
|function name|input|output|basis explain|
|-----|----|---|---|
|get_etdm_grad|file_name: str : 输入文件名 <br> N: int : 原子数量|shape=3N*3的数组 行对应原子，列对应x y z三个方向|从 gaussian log 中读取跃迁偶极矩梯度|
## additional explanation
### get_etdm_grad

从 "Electronic Transition Derivatives"开始，到空行结束中间的数据是我们要处理的区域（不包括开头和结束行），其中每一行为共有以空格分隔的数据若干，首先你需要对每一行进行分割变成一个列表，并将所有的'D'换成'e'，再将列表转化为数组，注意大部分行都是6个数字，但有的行只有5个数字，对于只有5个数据的行可以再前面插入0使其变为6个。然后将所有第一个元素是2的数组去掉第一个数并拼接起来（压缩为一个一维数组），将所有第一个元素是3的数组去掉第一个数并拼接起来，将所有第一个元素是4的数组去掉第一个数并拼接起来，将这三个一维数组推起来（变为一个有三行的二维数组），去掉前三列，输出剩余数据
