# 1 TwoSum
基本思路：
1. 采用hash表存放访问过的元素。每访问一个新的元素x，在hash表中查找s-x是否存在。若存在，则返回结果；否则将该元素加入hash表。
```python
def twoSum(p, s):
    hash_p = {}
    for i in range(len(p)):
        if s-p[i] in hash_p:
            return [p[i], s-p[i]]
        else:
            hash_p[p[i]] = i
    return []
```
评价：时间和空间复杂度都是O(n)，且支持输出元素的下标

2. 排序+双指针。
评价：时间复杂度为O(nlogn)，空间复杂度为O(1)，但不支持输出元素的下标

## 扩展问题：和小于K的两个数
问题描述：给你一个整数数组 p 和一个整数 K，请在该数组中找出两个元素，使它们的和小于 K 但尽可能地接近 K，返回这两个元素的和

基本思路：采用排序+双指针的方法，记录小于K的情况中的最大值即可。
```python
def lessK(p, K):
    if not p:
        return -1
    p.sort()
    l, r = 0, len(p)-1
    result = -float('inf')
    while l<r:
        if p[l]+p[r]>=K:
            r -= 1
        else:
            result = max(result, p[l]+p[r])
            l += 1
    if result == -float('inf'):
        return -1
    else:
        return result
```
# 2 ThreeSum
问题描述：给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

基本思路：a + b = -c。因此，原问题转化为TwoSum问题。
```python
def threeSum(nums):
    if not nums or len(nums)<3:
        return []
    nums.sort()
    result = []
    for i in range(len(nums)-2):
        if i!=0 and nums[i]==nums[i-1]:
            continue
        twoSum(nums, i+1, -nums[i], result)
    return result
```
## 扩展问题：有效三角形的个数
问题描述：给定一个包含非负整数的数组，你的任务是统计其中可以组成三角形三条边的三元组个数。

基本思路：组成三角形三条边的充要条件是较小的两边之和大于第三边，即a + b > c。因此，思路与TwoSum一样。采用排序+双指针的方法。
```python
def validTriangle(nums):
    if not nums or len(nums)<3:
        return 0
    nums.sort()
    result = 0
    for i in range(2, len(nums)):
        start, end = 0, i-1
        while start<end:
            if nums[start]+nums[end]<=nums[i]:
                start += 1
            else:
                result += (end-start)
                end -= 1
    return result
```
# 3 FourSum
问题描述：给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

基本思路：与ThreeSum问题类似，将其转化为ThreeSum问题。
```python
def fourSum(nums, target):
    if not nums or len(nums)<4:
        return []
    nums.sort()
    result = []
    for i in range(len(nums)-3):
        if i!=0 and nums[i]==nums[i-1]:
            continue
        threeSum(nums, i+1, target-nums[i], result)
    return result
```
# 4 两数之差
问题描述：给定一个 target，求出两数之差等于 target 的情况。

基本思路：最直接的思路是采用hash表。如果想采用双指针的方法，则需要将首尾指针替换为同向前后指针。