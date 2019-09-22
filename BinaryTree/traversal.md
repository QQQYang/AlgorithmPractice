二叉树遍历是一个基础问题，可以分为递归和非递归写法。一般而言，非递归版本更具有挑战性，在算法面试中更加重要。
# 递归版本
基本思路：直接根据二叉树遍历的递归定义来写即可。
## 前序遍历
```python
def preOrder(node):
    if node is None:
        return None
    print(node.val)
    preOrder(node.left)
    preOrder(node.right)
```
以此类推，中序遍历和后续遍历相似。
## 中序遍历
```python
def inOrder(node):
    if node is None:
        return None
    inOrder(node.left)
    print(node.val)
    inOrder(node.right)
```
## 后序遍历
```python
def postOrder(node):
    if node is Node:
        return None
    postOrder(node.left)
    postOrder(node.right)
    print(node.val)
```
# 非递归版本
整体思路：采用栈来存放节点，然后根据每种遍历的顺序调整入栈、出栈和打印节点的顺序
## 前序遍历
前序遍历比较简单，根据根节点、左、右的顺序，可以分析出先输出根节点，然后按顺序将右孩子、左孩子进栈。
```python
def preOrder(node):
    stack = [node]
    while len(stack)>0:
        print(node.val)
        if node.left is not None:
            stack.append(node.left)
        if node.right is not None:
            stack.append(node.right)
        node = stack.pop()
```
## 中序遍历
中序遍历需要先输出左孩子，因此需要在到达左孩子之前，先把路径上遇到的根节点入栈。当到达最“左”的左孩子时，出栈输出根节点，然后该根节点的右孩子入栈。循环该过程，直到当前节点为None且栈为空。
```python
def inOrder(node):
    stack = []
    while node is not None or len(stack)>0:
        if node is not None:
            # 寻找左孩子
            stack.append(node)
            node = node.left
        else:
            node = stack.pop()
            print(node.val)
            node = node.right
```
## 后序遍历
必须等到走完所有的路径之后根节点才能输出，因此仅用一个栈来存放一条路径上的节点是不够的。单纯一个栈保存的节点顺序是左右交错的，需要用第二个栈来记录第一个栈的弹出过程，从而记录一个干净的后序遍历序列：左-右-根，反推第一个栈的出栈顺序也是根-右-左。
```python
def postOrder(node):
    stack = [node]
    stack2 = []
    while len(stack)>0:
        node = stack.pop()
        stack2.append(node)
        if node.left is not None:
            stack.append(node.left)
        if node.right is not None:
            stack.append(node.right)
    while len(stack2)>0:
        print(stack2.pop().val)
```