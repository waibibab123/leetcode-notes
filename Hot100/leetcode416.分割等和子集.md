# 416、分割等和子集
难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/partition-equal-subset-sum/description/

## 题解
### 方法一、动态规划
假设数组的所有元素的和为sum，如果sum是奇数，那么必然无法分割成等和子集，直接返回false，接下来，我们只讨论sum为偶数的情况。

当sum为偶数时，我们可以把这个问题转换为背包容量为sum / 2的01背包问题

step1.状态表示：dp[i]表示为背包容量为i时，我们最多可以包含的物品体积

step2.状态转移：当背包容量为j时，对于一件物品nums[i]，我们可以讨论包含或不包含这个物品两种情况，如果包含那么`dp[j] = dp[j - nums[i]] + nums[i]`，如果不包含，那么dp[j]保持不变，所以每一次状态转移，我们只需要取这两种情况的最大值即可。

step3.边界处理：当背包容量为0时，我们最多可以包含的物品体积必然为0，因此`dp[0] = 0`

## 代码
C++ 

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for (int i = 0; i < nums.size(); i ++ ) sum += nums[i];
        if (sum % 2 == 1) return false;
        sum /= 2;
        vector<int> dp(sum + 1, 0);
        for (int i = 0; i < nums.size(); i ++ ) {
            for (int j = sum; j >= nums[i]; j -- ) {
                dp[j] = max(dp[j], dp[j - nums[i]] + nums[i]);
            }
        } 
        return dp[sum] == sum;
    }
};
```
