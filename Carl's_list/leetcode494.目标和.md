# 494、目标和
题目网址：https://leetcode.cn/problems/target-sum/

题目难度：mid

代码语言：cpp
## 题解
动态规划

假设nums所有元素的和为sum

假设正值的和为pos，复制的和为neg，有：

`pos + neg == abs(target); pos - neg = sum`，为了方便起见，我们取target的绝对值以防止讨论正负号而且不会改变结果的值，此时可以推出：`pos = (abs(target) + sum) / 2`

此时，我们知道，如果`abs(target) + sum`是必须能被2除尽的，否则直接返回0即可

接下来，问题就转换为了nums中元素组合成pos的方法数，我们设状态表示`dp[j]`为背包容量为j时，挑选物品的方法数，以转换为类似01背包的问题

状态表示为:`dp[j] = dp[j] + dp[j - nums[i]]`，意思是：dp[j]有两种情况组成，要么不选nums[i]这个物品，要么不选nums[i]这个物品

最终返回dp[pos]即可

```cpp
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        int sum = 0;
        for (int i = 0; i < nums.size(); i ++ ) sum += nums[i];
        int maxSize = sum + abs(target);
        if (sum < abs(target) || maxSize % 2 == 1) return 0;
        maxSize /= 2;
        vector<int>dp(maxSize + 1, 0);
        dp[0] = 1;
        for (int i = 0; i < nums.size(); i ++ ) {
            for (int j = maxSize; j >= nums[i]; j -- ) {
                dp[j] += dp[j - nums[i]];
            }
        } 
        return dp[maxSize];
    }
};
```
