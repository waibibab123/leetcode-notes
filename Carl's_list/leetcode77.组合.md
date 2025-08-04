# 77、组合
题目网址：https://leetcode.cn/problems/combinations/description/

题目难度：mid

代码语言：cpp
## 题解
回溯

step1.首先确定函数参数，肯定有n和k，其次，由于组合是不区分顺序的，所以要添加一个额外的参数startIndex记录本次回溯的起点。还要有两个数组path和res，分别记录回溯路径上的每种情况以及最终答案

step2.确定边界，当path的元素个数等于k，直接加入res

step3.确定单次递归逻辑，从startIndex开始一直循环到n，对于每一次循环，将当前元素加入path，接着调用递归函数然后再恢复现场将上个元素从path中取出

C++
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    void dfs(int n, int k, int startIndex) {
        if (path.size() == k) {
            res.push_back(path);
            return;
        }
        for (int i = startIndex; i <= n; i ++ ) {
            path.push_back(i);
            dfs(n, k, i + 1);
            path.pop_back();
        }
    }
    vector<vector<int>> combine(int n, int k) {
        dfs(n, k, 1);
        return res;
    }
};
```
