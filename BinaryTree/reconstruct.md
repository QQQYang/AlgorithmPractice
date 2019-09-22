问题：根据二叉树前序遍历和中序的的结果，重建一棵二叉树。

基本思路：前序遍历的第一个元素为根节点，利用该节点将中序遍历的结果分为左子树和右子树。获得左子树的长度，从而也将前序遍历的结果分为了左子树和右子树。接下来的过程就是一个递归过程，代码如下：
```python
def reconstructBinaryTree(pre_res, in_res):
    if len(pre_res)>0:
        root = TreeNode(pre_res[0])
        root_id = in_res.index(root.val)
        root.left = reconstructBinaryTre(pre_res[1:1+root_id], in_re[:root_id])
        root.right = reconstructBinaryTre(pre_res[1+root_id:], in_res[root_i+1:])
        return root
```