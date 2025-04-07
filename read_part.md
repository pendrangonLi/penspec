# generate some function to read basis info
## function table
|function name|input|output|basis explain|additional explanation|
|-----|----|---|---|---|
|get_atom_num|filename: str : 输入文件名|N: int :原子数量|从 gaussian log文件中读取体系的原子数量|pass|
|get_atom_mass|file_name: str : 输入文件名 <br> N: int : 原子数量|M: np.array : 原子质量 shape=N*1| 从 gaussian log文件中读取体系的原子数量 |pass|
