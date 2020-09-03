## [16. 最接近的三数之和](https://leetcode-cn.com/problems/3sum-closest/)
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

示例：
```text
输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
```

提示：
```text
3 <= nums.length <= 10^3
-10^3 <= nums[i] <= 10^3
-10^4 <= target <= 10^4
```

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        // 返回的值是最接近target的三数和
        int result = 20000; // |20000 - 3000| > |-10000 - 3000|
        Arrays.sort(nums);
        for (int first = 0; first < nums.length; first++) {
            int second = first + 1;
            int third = nums.length - 1;
            while (second < third) {
                int curTarget = nums[first] + nums[second] + nums[third];
                if (curTarget == target) {
                    // 找到一个等值答案，不必再往下算了
                    return curTarget;
                }
                if (Math.abs(result - target) > Math.abs(curTarget - target)) {
                    result = curTarget;
                }
                if (curTarget > target) {
                    // 右指针左移
                    third--;
                } else {
                    // 左指针右移
                    second++;
                }
            }
        }
        return result;
    }
}
```