# 221、最大正方形
题目难度：mid

题目网址：https://leetcode.cn/problems/maximal-square/description/

代码语言：cpp

## 题解
### 方法一、前缀和
三层遍历，前两层遍历起点的坐标(i,j)，第三层遍历正方形的边长k，如果某一次遍历(i,j)到(i+k-1,j+k-1)构成的正方形中所有元素的和（转换为整数）恰好为$`k^2`$，那么就说明这个正方形内全为1

时间复杂度：$`O(N*M*K)`$， 空间复杂度：$`O(N*M)`$

方法局限性：如果除了0和1还包含其他值，那么该方法不可用

**代码**

C++

```cpp
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int n = matrix.size(), m = matrix[0].size();
        vector<vector<int>> S(n + 1, vector<int>(m + 1, 0));
        for (int i = 1; i <= n; i ++ ) {
            for (int j = 1; j <= m; j ++ ) {
                S[i][j] = S[i - 1][j] + S[i][j - 1] + matrix[i - 1][j - 1] - S[i - 1][j - 1] - '0';//注意这里将字符转换为整数值
            }
        }
        int res = 0;
        for (int i = 1; i <= n; i ++ ) {
            for (int j = 1; j <= m; j ++ ) {
                for (int k = 1; k <= min(n, m); k ++ ) {
                    int ri = i + k - 1;
                    int rj = j + k - 1;
                    if (ri > n || rj > m) break;
                    if (S[ri][rj] - S[i - 1][rj] - S[ri][j - 1] + S[i - 1][j - 1] == pow(k, 2)) res = max(res, k);
                }
            }
        }
        return pow(res, 2);
    }
};
```
