# 31、下一个排列
题目难度：mid

题目网址：https://leetcode.cn/problems/next-permutation/?envType=study-plan-v2&envId=top-100-liked

代码语言：cpp
## 题解
### 方法一、双指针
思路来源：[【LeetCode 每日一题】31. 下一个排列 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1dT4y1y78u/?spm_id_from=333.337.search-card.all.click&vd_source=5a9892c5685e5b7e1d5cbd33baa8869e)

step1.**从后往前**找到第一个降序的元素，如果找不到，直接将整个数组反转即可，如果可以找到，假设为nums[k-1]，则进入第二步

step2.**从后往前**找到第一个大于nums[k-1]的元素nums[t]，并将nums[k-1]的值与nums[t]进行交换

step3.翻转从nums[k]到nums[nums.size()-1]之间的所有元素

举一个例子：
2、3、5、4、1、0

step1、可以找到第一个降序的元素是3

step2、可以找到第一个大于3的元素是4，并交换它们的位置，序列变成：2、4、5、3、1、0

step3、翻转从5到0的元素，序列变成：2、4、0、1、3、5

**代码**

C++

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int k = nums.size() - 1;
        while (k > 0 && nums[k - 1] >= nums[k]) k -- ;
        if (k <= 0) {
            reverse(nums.begin(), nums.end());
        } else {
            int t = nums.size() - 1;
            while (nums[k - 1] >= nums[t]) t -- ;
            swap(nums[k - 1], nums[t]);
            reverse(nums.begin() + k, nums.end());
        }
    }
};
```
