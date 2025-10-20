# 6、Z字形变换
题目网址：https://leetcode.cn/problems/zigzag-conversion/description/?envType=study-plan-v2&envId=top-interview-150

题目难度：mid

代码语言：cpp
## 题解
C++
```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows == 1) return s;
        else if (numRows == 2) {
            string res;
            for (int i = 0; i < s.length(); i += 2 ) {
                res += s[i];
            }
            for (int i = 1; i < s.length(); i += 2) {
                res += s[i];
            }
            return res;
        } 
        unordered_map<int, vector<int>> mp;
        for (int i = 0; i < numRows; i ++ ) mp[i] = vector<int>(0);
        int x = 0, y = 0;
        bool inpath = true;
        for (int i = 0; i < s.length(); i ++ ) {
            mp[x].push_back(s[i]);
            cout << x << " " << y << endl;
            if (inpath) {
                if (x + 1 == numRows) {
                    inpath = false;
                    x -- ;
                    y ++ ;
                } 
                else 
                x ++ ;
            } else {
                if (x - 1 == 0) inpath = true;
                x -- ;
                y ++ ;
            }
        }
        string res;
        for (int i = 0; i < numRows; i ++ ) {
            for (int j = 0; j < mp[i].size(); j ++ ) res += mp[i][j];
        }
        return res;
    }
};
```
