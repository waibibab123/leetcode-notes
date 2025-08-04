# 165.比较版本号

难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/compare-version-numbers/

## 解法

### 方法一、分割字符串

以'.'为分割符对version1和version2进行分隔，分隔之后依次进行两两比较即可，时间复杂度和空间复杂度均为$`O(N)`$

## 代码

C++ 

```cpp
class Solution {
public:
    int compareVersion(string version1, string version2) {
        vector<string> str1;
        vector<string> str2;
        stringstream ss;
        ss << version1;
        string temp;
        while (getline(ss, temp, '.')) {
            str1.push_back(temp);
        }
        ss.str("");
        ss.clear();
        ss << version2;
        while (getline(ss, temp, '.')) {
            str2.push_back(temp);
        }
        for (int i = 0; i < str1.size() || i < str2.size(); i ++ ) {
            int a = (i < str1.size()) ? stoi(str1[i]) : 0;
            int b = (i < str2.size()) ? stoi(str2[i]) : 0;
            if (a < b) return -1;
            else if (a > b) return 1;
        }
        return 0;
    }
};
```
