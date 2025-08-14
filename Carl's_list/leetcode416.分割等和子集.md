# 416、分割等和子集
题目网址：https://leetcode.cn/problems/partition-equal-subset-sum/description/

题目难度：mid

代码语言：cpp
## 题解
动态规划

首先，可以求出nums的元素总和sum，如果sum是奇数，一定是不能划分的因此就返回false

如果sum为偶数，那就是去看是否可以通过组合nums中若干个元素的和得到sum/2，在这里设状态表示`dp[j]`为背包容量为j时，最多可以装入的元素总和，这样实际上就变成了一个总容量为sum/2的01背包的问题

最后，再去判断dp[sum]是否等于sum即可

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for (int i = 0; i < nums.size(); i ++ ) sum += nums[i];
        if (sum % 2 != 0) return false;
        sum /= 2;
        vector<int>dp(sum + 1, 0);
        for (int i = 0; i < nums.size(); i ++ ) {
          for (int j = sum; j >= nums[i]; j -- ) {
            dp[j] = max(dp[j], dp[j - nums[i]] + nums[i]);
          }
        }
        return dp[sum] == sum;
    }
};
```
