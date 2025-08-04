# 93、复原IP地址
题目网址：https://leetcode.cn/problems/restore-ip-addresses/description/

题目难度：mid

代码语言：cpp
## 题解
回溯

step1.变量设置：
* 记录答案数组：res

step2.递归参数：
* s:待分割的字符串
* index：本次要分割的起始位置
* pointNum：当前已经加的小数点数量

step3.边界条件：当小数点已经添加了三个，且最后一个小数点后面的数值满足ip地址要求，就将当前的s加入res

step4.确定单次遍历逻辑：从index遍历s，对于每次遍历，在当前遍历的子串是满足ip地址要求的情况下，首先在这个子串最后加上小数点，让pointNum加一，然后调用递归函数，最后恢复现场（pointNum减一、去掉小数点）

C++
```cpp
class Solution {
public:
    vector<string> res;
    bool check(string path) {
        if (path.size() == 0 || path.size() > 3) return false;
        if (path.size() > 1 && path[0] == '0') return false;
        int num = 0;
        for (int i = 0; i < path.size(); i ++ ) {
            if (path[i] < '0' || path[i] > '9') return false;
            num = num * 10 + path[i] - '0';
        }
        if (num >= 0 && num <= 255) return true;
        else return false;
    }
    void dfs(string s, int pointNum, int index) {
        if (pointNum == 3 && check(s.substr(index, s.size() - index + 1))) {
            res.push_back(s);
            return;
        }
        for (int i = index; i < s.size(); i ++ ) {
            if (i - index + 1 > 3) break;
            if (check(s.substr(index, i - index + 1))) {
                s.insert(i + 1, ".");
                pointNum ++ ;
                dfs(s, pointNum, i + 2);
                s.erase(s.begin() + i + 1);
                pointNum -- ;
            }
        }
    }
    vector<string> restoreIpAddresses(string s) {
        dfs(s, 0, 0);
        return res;
    }
};
```
