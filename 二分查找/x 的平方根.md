# 问题描述
实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

# 基本思路
二分查找。
```python
def sqrt(x):
    left, right = 0, x
    while left+1<right:
        mid = left + ((right-left)>>1)
        if mid*mid<x:
            right = mid
        elif mid*mid>x:
            left = mid
        else:
            return x
    if right*right<=x:
        return right
    else:
        return left
```

# 扩展
如果输入参数是任意的浮点数，应该如何调整。

注意：此时当x小于1时，x*x < x，因此left和right需要颠倒。
```python
def sqrt(x, eps):
    if x==0.0 or x==1.0:
        return x
    if x<1.0:
        left = x
        right = 1.0
    else:
        left = 0
        right = x
    while abs(right-left)<eps:
        mid = left + (right-left)/2
        if abs(mid**2-x)<eps:
            return mid
        elif mid**2<x:
            left = mid
        else:
            right = mid
    return left
```