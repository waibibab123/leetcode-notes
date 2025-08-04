# 241、为运算表达式设计优先级
题目难度：mid

题目网址：https://leetcode.cn/problems/different-ways-to-add-parentheses/description/

代码语言：cpp
## 题解
### 方法一、递归（分治+记忆化搜索）
思路来源：[力扣用户：才半页的题解](https://leetcode.cn/problems/different-ways-to-add-parentheses/solutions/1636227/fen-zhi-ji-sou-by-heren1229-hp0o/)

对于一个算式来说，总是可以根据运算符分为两个部分，接着分别计算结果并合并，每一个结果都是一个数组，包含这个算式的所有可能结果，计算时将左右部分排列组合

递归的边界有两个：1.纯数字，直接返回  2.为了使用记忆化搜索，我们可以使用哈希表作为备忘录，保存算式到结果数组的映射，因此当哈希表存放的有当前处理的算式时，可以直接返回

这里使用到了一个之前陌生的函数是STL的string的`find_first_of`，之前使用的一直是`find`函数，find函数用于查找给定的字符串，而`find_first_of`可以用来查找字符集合，当查询失败会返回s.npos，搭配while一起使用可以方便地找到所有的运算符分割点

**代码**

C++

```cpp
class Solution {
public:
    unordered_map<string, vector<int>> memo;
    vector<int> diffWaysToCompute(string expression) {
        if (memo.count(expression)) return memo[expression];
        if (expression.find_first_of("+-*") == expression.npos) return vector<int>{stoi(expression)};
        int pos = 0;
        vector<int> ans;
        while ((pos = expression.find_first_of("+-*", pos + 1)) != expression.npos) {  //注意这里是如何方便地找到所有运算符分割点的
            vector<int> left = diffWaysToCompute(expression.substr(0, pos));
            vector<int> right = diffWaysToCompute(expression.substr(pos + 1));
            char op = expression[pos];
            for (int l : left) {
                for (int r : right) {
                    ans.push_back(op == '+' ? l + r : op == '-' ? l - r : l * r);
                }
            }
        }
        memo[expression] = ans;
        return memo[expression];
    }
};
```
