# 216、组合总和3
题目网址：https://leetcode.cn/problems/combination-sum-iii/description/

题目难度：mid

代码语言：cpp
## 题解
回溯

step1.变量设置：创建一个path数组和res数组分别记录回溯路径上的元素以及最终答案数组

step2.递归函数参数：
* startIndex：遍历的起始位置，防止出现相同的组合或者一个数字使用多次的情况
* sum：记录当前的元素和离目标和n的差值，当sum == 0时说明此时回溯路径上的元素和为n
* k：限定组合中元素的个数

step3.递归边界：
当path数组的长度，也就是当前递归路径上的元素数量等于k，并且当前递归路径上的元素和离目标和的差值sum等于0时，将本次递归路径上元素组成的数组path加入答案数组res

step4.单次递归逻辑
从startIndex开始遍历一直到9，期间，首先将遍历到的元素加入递归路径数组，然后开始递归，最后“恢复现场”

C++
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    void dfs(int sum, int k, int startIndex) {
        if (sum == 0 && path.size() == k) {
            res.push_back(path);
            return;
        }
        for (int i = startIndex; i <= 9; i ++ ) {
            path.push_back(i);
            dfs(sum - i, k, i + 1);
            path.pop_back();
        }
    }
    vector<vector<int>> combinationSum3(int k, int n) {
        dfs(n, k, 1);
        return res;
    }
};
```
