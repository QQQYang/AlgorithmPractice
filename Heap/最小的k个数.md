**问题描述**：输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

**基本思路**：1. 链表，按顺序存储最小的K个数，时间复杂度为O(nK)；2. 最大堆，时间复杂度为O(nlogK)；3. 类似快速排序中的partition操作，采用二分法。
```python
def findKSmallestNum(nums, K):
    max_heap = []
    import heapq
    for i in range(len(nums)):
        if len(max_heap)==K and -max_heap[0]>nums[i]:
            heapq.heappush(max_heap, -nums[i])
            heapq.heappop(max_heap)
        else:
            heapq.heappush(max_heap, -nums[i])
    return max_heap
```