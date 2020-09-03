## 二分法
[34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。
你的算法时间复杂度必须是 O(log n) 级别。
如果数组中不存在目标值，返回 [-1, -1]。

示例 1:
```text
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```

示例 2:
```text
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int start = 0;
        int end = nums.length - 1;
        int mid;
        while (start <= end) {
            mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                int r1 = mid;
                int r2 = mid;
                while (r1 - 1 >= 0 && nums[r1 - 1] == target) {
                    r1--;
                }
                while (r2 + 1 < nums.length && nums[r2 + 1] == target) {
                    r2++;
                }
                return new int[]{r1, r2};
            }
            if (nums[mid] > target) {
                // 在左侧
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        return new int[]{-1, -1};
    }
}
```
