# 198、打家劫舍

难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/house-robber/

## 解法
### 方法一、动态规划
状态表示：

* $`dp[i][0]`$表示为对前i个房屋进行偷窃且不偷窃第i个房屋时，一夜之内能够偷窃的最高金额
* $`dp[i][1]`$表示为对前i个房屋进行偷窃且偷窃第i个房屋时，一夜之内能够偷窃的最高金额

状态转移：

* 如果不偷窃第i个房屋，那么可以对第i-1个房屋进行偷窃，也可以不偷窃第i-1个房屋，取最大值即可，因此`dp[i][0] = max(dp[i - 1][0], dp[i - 1][1])`
* 如果偷窃第i个房屋，那么绝对不能再对第i-1个房屋进行偷窃，因此`dp[i][1] = dp[i - 1][0] + nums[i]`

边界处理：易知，`dp[0][0] = 0, dp[0][1] = nums[0]`

## 代码
C++

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        vector<vector<int>> dp(nums.size(), vector<int>(2, 0));
        dp[0][0] = 0;
        dp[0][1] = nums[0];
        for (int i = 1; i < nums.size(); i ++ ) {
            dp[i][0] = max(dp[i - 1][0], dp[i - 1][1]);
            dp[i][1] = dp[i - 1][0] + nums[i];
        }
        return max(dp[nums.size() - 1][0], dp[nums.size() - 1][1]);
    }
};
```
