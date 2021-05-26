# Python NumPy 基本使用

NumPy 針對陣列運算提供大量的數學函式函式庫，在深度學習時常會使用到。

## 導入 Numpy

```Python
import numpy
```

## NumPy 基本語法

### 產生 Numpy 陣列

```Python
x = np.array([1, 2, 3])
print(x)  # [1 2 3]
print(type(x))  # <class 'numpy.ndarray'>
```

### NumPy 運算

```Python
x = np.array([1, 2, 3])
y = np.array([2, 4, 6])

print(x + y)  # [3 6 9]
print(x - y)  # [-1 -2 -3]
print(x * y)  # [ 2  8 18]
print(x / y)  # [0.5 0.5 0.5]
```

## NumPy 的 N 維陣列

### 建立 N 維陣列

```Python
x = np.array([[1, 2], [3, 4]])

print(x)
# [[1 2]
#  [3 4]]

print(x.shape)  # (2, 2)
print(x.dtype)  # int32
```

矩陣形狀用 `shape` 參照
矩陣資料型態用 `dtype` 參照

### N 維陣列運算

```Python
x = np.array([[1, 2], [3, 4]])
y = np.array([[3, 0], [0, 6]])

print(x * 10)
# [[10 20]
#  [30 40]]

print(x + y)
# [[ 4  2]
#  [ 3 10]]

print(x * y)
# [[ 3  0]
#  [ 0 24]]
```

### 廣播

```Python
x = np.array([[1, 2], [3, 4]])
y = np.array([3, 0])

print(x * y)
# [[3 0]
#  [9 0]]
```