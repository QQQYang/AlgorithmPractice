# 问题描述
给定一个有n个正整数的数组A和一个整数sum,求选择数组A中部分数字和为sum的方案数。

当两种选取方案有一个数字的下标不一样,我们就认为是不同的组成方案。

# 基本思路
回溯
```python
def numSum(A, n, s):
    result = [0]
    dfs(A, s, result)
    return result[0]

def dfs(nums, s, result):
    if s>0:
        for i in range(len(nums)):
            if nums[i]==s:
                result[0] += 1
            else:
                dfs(nums[i+1:], s-nums[i], result)
```

动态规划

dp[i][j]表示前i个数和为j的方案数。if j>A[i], dp[i][j]=dp[i-1][j]+dp[i-1][j-A[i]]; else, dp[i][j]=dp[i-1][j]

```python
def numSum(A, n, s):
    dp = [[0 for _ in range(s+1)] for _ in range(n+1)]
    for i in range(1, n+1):
        for j in range(1, s+1):
            if j>A[i]:
                dp[i][j] = dp[i-1][j] + dp[i-1][j-A[i]]
            else:
                dp[i][j] = dp[i-1][j]
    return dp[-1][-1]
```