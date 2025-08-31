# 377、组合总和4
题目网址：https://leetcode.cn/problems/combination-sum-iv/

代码语言：cpp

题目难度：mid

前置题目：[leetcode518、零钱兑换](leetcode518.零钱兑换2.md)
## 题解
这道题目和零钱兑换2不同之处仅在于每一种组合是区分顺序的，这种情况下，我们采用的方法是**先遍历容量再遍历物品**

可以这样理解：

* 当我们先遍历物品再遍历容量时，因为每个物品只会被考虑一次，得到的将是组合数
* 当先遍历容量再遍历物品时，对于每个容量我们会尝试所有可能性的物品，从而自然地考虑了不同的排列顺序

C++
```cpp
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        int n = nums.size();
        vector<int> dp(target + 1, 0);
        dp[0] = 1;
        for (int j = 0; j <= target; j ++ ) {
            for (int i = 0; i < n; i ++ ) 
                if (j >= nums[i] && dp[j] <= INT_MAX - dp[j - nums[i]])
                dp[j] += dp[j - nums[i]];
        }
        return dp[target];
    }
};
```
