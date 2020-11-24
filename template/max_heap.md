## 数组建堆 - 大顶堆
> [215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/description/)

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:
```text
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

示例 2:
```text
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

说明:
你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        // 数组建最大堆
        for (int i = nums.length / 2; i >= 0; i--) {
            // 叶子节点已经满足最大堆条件（只有一个节点，当然满足条件）
            // 因此，我们从非叶子节点开始处理（自下往上，倒序处理）
            maxHeapify(nums, i, nums.length);
        }
        // 移除首项并修复最大堆
        for (int i = 1; i < k; i++) {
            // 移除第一项，移除k-1次后，nums[0]即为第k大值
            // 移除操作就是把最后一位赋给根节点，同时堆大小减一
            swap(nums, 0, nums.length - i);
            // 修复堆
            maxHeapify(nums, 0, nums.length - i);
        }
        return nums[0];
    }

    public void maxHeapify(int[] nums, int index, int size) {
        // 父节点是index，则对应左节点/右节点分别为 index * 2 + 1 和 index * 2 + 2
        int left = index * 2 + 1;
        int right = index * 2 + 2;
        int largest = index;
        if (left < size && nums[left] > nums[largest]) {
            largest = left;
        }
        if (right < size && nums[right] > nums[largest]) {
            largest = right;
        }
        // 至此，父节点与其左右子节点的最大值，就是索引largest对应的值
        if(largest != index) {
            // 父节点小于某个子节点，修正大顶堆
            swap(nums, largest, index);
            maxHeapify(nums, largest, size);
        }
    }

    public void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```
