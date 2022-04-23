```python
pip install pandas
import pandas as pd                         #导入pandas包
data = pd.read_csv("train.csv")           	#读取csv文件
#print(data)                                #打印所有文件
print(data.columns) 						#返回全部列名
print(data.shape)							#f返回csv文件形状
print(data.loc[1:2])						#打印第1到2行
data.loc[2:4, ['PassengerId', 'Sex']]       #打印行中特定列
```
