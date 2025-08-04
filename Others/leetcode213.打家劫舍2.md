# 213、打家劫舍2
题目难度：mid

题目网址：https://leetcode.cn/problems/house-robber-ii/

代码语言：cpp

## 题解
### 方法一、动态规划
前置题目：[leetcode198.打家劫舍](../Hot100/leetcode198.打家劫舍.md)

这道题在198的基础上，增加了环的条件，为了解决这一问题，我们对是否偷nums[0]进行分类讨论：

* 如果偷nums[0]，那么题目转换为从下标2到下标nums.size()-2的无环问题
* 如果不偷nums[1]，那么题目转换为从下标1到下标nums.size()-1的无环问题

因此我们只需要在198的代码基础上简单改动即可：

C++

```cpp
class Solution {
private:
    // 0 对应 l
    // r - l 对应 r
    int rob_noloop(vector<int>& nums, int l, int r) {
        if (l > r) return 0;
        vector<vector<int>> dp(r - l + 1, vector<int>(2, 0));
        dp[0][0] = 0;
        dp[0][1] = nums[l];
        for (int i = 1; i <= r - l; i ++ ) {
            dp[i][0] = max(dp[i - 1][0], dp[i - 1][1]);
            dp[i][1] = dp[i - 1][0] + nums[i + l];
        }
        return max(dp[r - l][0], dp[r - l][1]);
    }
public:
    int rob(vector<int>& nums) {
        return max(nums[0] + rob_noloop(nums, 2, nums.size() - 2), rob_noloop(nums, 1, nums.size() - 1));
    }
};
```
