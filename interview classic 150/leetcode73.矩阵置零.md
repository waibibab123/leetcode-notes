# 73、矩阵置零
题目难度：mid

代码语言：cpp
## 题解
需要额外增加两个变量rowZero和colZero去特殊处理第零行和第零列

C++
```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        bool rowZero = false;
        bool colZero = false;
        for (int i = 0; i < m; i ++ ) {
            if (matrix[i][0] == 0) colZero = true;
        }
        for (int j = 0; j < n; j ++ ) {
            if (matrix[0][j] == 0) rowZero = true;
        }
        for (int i = 1; i < m; i ++ ) {
            for (int j = 1; j < n; j ++ ) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        for (int i = 1; i < m; i ++ ) {
            if (matrix[i][0] == 0) {
                for (int j = 1; j < n; j ++ ) matrix[i][j] = 0;
            }
        }
        for (int j = 1; j < n; j ++ ) {
            if (matrix[0][j] == 0) {
                for (int i = 1; i < m; i ++ ) matrix[i][j] = 0;
            }
        }
        if (rowZero == true) {
            for (int j = 0; j < n; j ++ ) matrix[0][j] = 0;
        }
        if (colZero == true) {
            for (int i = 0; i < m; i ++ ) matrix[i][0] = 0;
        }
    }
};
```
