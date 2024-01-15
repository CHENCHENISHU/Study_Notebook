

查看包

```
python -m pip list
```



# 1.Numpy



## 1.1创建数组对象

```python
# object参数，
# dtype数组需要类型默认none
# ndmin生成数组最小维度
np.array(object,dtype,ndmin)
```



## 1.2专门创建数组

| 函数               | 说明                                     |
| ------------------ | ---------------------------------------- |
| np.arange(n)       | range函数，返回ndarray类型，0~n-1        |
| np.ones(shape)     | 根据shape生成全1数组                     |
| np.zeros(shape)    |                                          |
| np.full(shape,val) | 生成一个全val矩阵                        |
| np.eye(n)          | 创建一个对角线元素为1，其余为0方阵       |
| np.linespace()     | 指定开始值，最后值，和元素个数，一维数组 |
| np.logspace()      | 创建一维等比数组                         |

> ndarray属性说明

| 属性     |                    |
| -------- | ------------------ |
| ndim     | 秩。数据轴的个数   |
| shape    | 数组维度           |
| size     | 数组元素个数       |
| dtype    | 数据类型           |
| itemsize | 数组每个元素字节值 |
| nbytes   | 整个数组所需字节数 |



## 1.3随机数

```python
np.random.randint(low,high=None,size=None)

arr1 = np.random.randint(100,200,size =(2,4))
# [[117,175,154,187]
#  [198,175,165,178]]

arr2 = np.random.rand(5)
# 5个随机数的数组

arr3 = np.randon.rand(3,2)
#三行二列
```

相关函数

| 函数          |                                                |
| ------------- | ---------------------------------------------- |
| seed()        | 确定随机数生成器种子                           |
| permutation() | 返回一个序列的随机排列或返回一个随机排列的范围 |
| shuffle()     | 对一个序列进行随机排序                         |
| bionomial()   | 产生二项分布的随机数                           |
| normal()      | 产生正态分布的随机数                           |
| beta()        | 产生贝塔分布的随机数                           |
| chisquare()   | 产生卡方分布的随机数                           |
| gamma()       | 产生伽马分布的随机数                           |
| uniform()     | 产生在[0,1)中均匀分布的随机数                  |

## 1.4数组变换

数组合并

```python
# 数组变换维度
arr1 = np.arrange(12)

arr2 = arr1.reshape(3,4)

arr3 = arr1.reshape(2,-1)

# 数组合并 
# hstack()横向合并 vstack()纵向合并 concatenate()axis=1横向合并，axis=0纵向合并

concatenate((arr1,arr2),axis=1)
```



数组分割

```python
# hsplit()横向 vsplit()纵向 split()指定方向
```



矩阵转置

```python
# transpose

arr1 = np.arange(6).reshape(3,2)
arr2 = arr1.transpose((1,0))
# [[0 1]
# [2 3]
# [4 5]]

# [[0 2 4]
# [1 3 5]]
```

## 1.5数组索引和切片

```python
arr1 = np.arange(6)
print(arr1[2]) # 2

# ufunc函数针对数组
# +(加) -(减) *(乘) **(幂运算)
# < > == >= !=


# where(condition,x,y)满足condition输出x，否则y
```

## 1.6排序，重复数据去重，统计函数

```python
# sort 直接排序
# sort(a,axis,kind,order)
# 要排列数组 按维度排序 排序算法 数组如包含字段，则是要排序的字段
# argsort lexsort 间接排序
arr1 = np.array([9,8,7,3,6,5,1])

arr2 = arr1.sort()

arr3 = np.array([4,3,4,5,6],[1,2,3,6,8],[3,4,6,2,3])
arr3.sort(axis=1) # 横向排序

arr4 = np.array([9,3,4,5,6,7,8,9,1])
arr4.argsort() # 返回值为数组排序后的索引排列
arr4.lexsort(a,b) # 两个一起排，如果a中有相同的，就参考b的



```

>
> 数据重复

```python
# 去重使用 np.unique(arr)

# 重复 tile(arr,3) repeat(arr,reps,axis=none)reps为重复次数
```



> 统计函数

```python
sum(arr,axis=none) # 和
mean(arr,axis=none) # 均值
std(arr,axis=none) # 标准差
var() # 
min(arr,axis=none) # 最小值
max(arr,axis=none) # 最大值
```

# 2.Pandas

Pandas有三种数据结构：series，DataFrame，Series

series类似于数组

DataFrame类似于表格

Panel可视为Excel的多表单Sheet



## Series

```python
import pandas as pd

obj1 = pd.Series([1, 2, 3, 4])
print(obj1)
# 0    1
# 1    2
# 2    3
# 3    4
# dtype: int64
# obj2 = pd.Series(v, index=i, name="col")
obj2 = pd.Series([1, 2, 3], index=["9", "8", "7"], name="col")
print(obj2)
# 9    1
# 8    2
# 7    3
# Name: col, dtype: int64
sdata = {'嘉然': 30000, '向晚': 20000, '奶琳': 25000, '贝拉': 10000}
obj3 = pd.Series(sdata)
print(obj3)
# jiaran      30000
# xiangwan    20000
# nailin      25000
# beila       10000
# dtype: int64
states = ['永雏塔菲', '冬雪莲', '柯洁', '瓶子君']
obj4 = pd.Series(sdata, index=states)
print(obj4)
# 永雏塔菲   NaN
# 冬雪莲    NaN
# 柯洁     NaN
# 瓶子君    NaN
# dtype: float64

obj5 = pd.Series([1, 2, 3, 4, 5])
obj5.index = ['嘉然', '向晚', '冬雪莲', '永雏塔菲', '明前奶绿']
print(obj5)
# 嘉然      1
# 向晚      2
# 冬雪莲     3
# 永雏塔菲    4
# 明前奶绿    5
# dtype: int64
```



DataFrame

```python
import pandas as pd

data = {
    'name': ['张三', '李四', '王五', '嘉然', '向晚', '冬雪莲'],
    'sex': ['男', '女', '男', '女', '男', '女'],
    'year': [2001, 2002, 2003, 2004, 2005, 2002]
}
df1 = pd.DataFrame(data, columns=['name', 'sex', 'year'])
print(df1)
# name sex  year
# 0   张三   男  2001
# 1   李四   女  2002
# 2   王五   男  2003
# 3   嘉然   女  2004
# 4   向晚   男  2005
# 5  冬雪莲   女  2002
```



## DataFrame

```python
import numpy as np
import pandas as pd

a = np.arange(6).reshape(2, 3)
b = np.arange(4).reshape(2, 2)
df1 = pd.DataFrame(a, columns=['a', 'b', 'c'], index=['A', 'C'])
print(df1)
#    a  b  c
# A  0  1  2
# C  3  4  5
df2 = pd.DataFrame(b, columns=['a', 'b'], index=['A', 'B'])
print(df2)
#    a  b
# A  0  1
# B  2  3

print("\n", df1 + df2)
#     a    b   c
# A  0.0  2.0 NaN
# B  NaN  NaN NaN
# C  NaN  NaN NaN
```

map()函数，将函数套到Series每个元素

apply()函数，将函数套到DataFrame的行和列上，行和列通过axis参数设置

applymap()函数，函数套用到DataFrame的每个元素



## 汇总统计