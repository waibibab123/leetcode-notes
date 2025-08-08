# 96、不同的二叉搜索树
题目网址：https://leetcode.cn/problems/unique-binary-search-trees/description/

题目难度：mid

代码语言：cpp
## 题解
动态规划

状态表示：`dp[i]`表示由i个不同的节点组成的二叉搜索树的种类

对于一个确定的i，假设节点从小到大编号为1、2、3、...、i，假设以k为头结点(k>=1 && k<=i)的二叉搜索树有f[k]种，那么dp[i]=f[1]+f[2]+f[3]+...+f[i]

对于一个确定的k，左子树的可能取值为编号1、2、3、...、k-1组成的二叉搜索树的种类数，也就是dp[k-1]，右子树的可能取值为编号k+1、k+2、...、i，也就是dp[i-k]，因此f[k]=dp[i-k]

C++
```cpp
class Solution {
public:
    int numTrees(int n) {
        vector<int>dp(n + 1, 0);
        dp[0] = 1;
        for (int i = 1; i <= n; i ++ ) {
            for (int k = 1; k <= i; k ++ ) {
                dp[i] += dp[k - 1] * dp[i - k];
            }
        }
        return dp[n];
    }
};
```
