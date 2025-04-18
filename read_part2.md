# generate some function to read basis info
使用python完成以下函数，不准用re库的正则表达式
## function table
|function name|input|output|basis explain|
|-----|----|---|---|
|get_etdm_grad|file_name: str : 输入文件名 <br> N: int : 原子数量|shape=3N*3的数组 行对应原子，列对应x y z三个方向|从 gaussian log 中读取跃迁偶极矩梯度|
## additional explanation
### get_etdm_grad

从 "Electronic Transition Derivatives"开始，到空行结束中间的数据是我们要处理的区域（不包括开头和结束行），使用open读取为二维列表，其中每一行为共有以空格分隔的数据若干，首先你需要对每一行进行分割变成一个列表，并将所有的'D'换成'e'，再将列表中的元素转化为float。然后将所有第一个元素是2的列表提取出来，去掉第一个数后通过extend拼接为一个列表，记为A2；同样的方法处理第一个元素是3和4的列表得到A3和A4。将A2 A3 A4拼起来得到一个三行的二维列表，将该二维列表转化为np.array后去掉前三列，输出剩余数据
