# 17、电话号码的字母组合
题目网址：https://leetcode.cn/problems/letter-combinations-of-a-phone-number/description/

题目难度：mid

代码语言：cpp
## 题解
回溯

step1.变量设置：
* 记录数字与字母的映射：mp
* 记录递归路径上的字符串：path
* 记录答案数组：res

step2.递归参数：
* digits：按下的数字集合
* index：记录当前递归的是digits的第几个数字

step3.边界条件：当index==digits.size()说明到达了递归树的叶子结点

step4.确定单次遍历逻辑：遍历字符串digits中第index个数字对应的字符串，对于每次遍历，首先将此元素加入path，然后调用递归函数，最后恢复现场

C++
```cpp
class Solution {
public:
    static constexpr string mp[] = {
        "",
        "",
        "abc",
        "def",
        "ghi",
        "jkl",
        "mno",
        "pqrs",
        "tuv",
        "wxyz"
    };
    vector<string> res;
    string path;
    void dfs(string digits, int index) {
        if (index == digits.size()) {
            res.push_back(path);
            return;
        }
        string str = mp[digits[index] - '0'];
        for (int j = 0; j < str.size(); j ++ ) {
            path = path + str[j];
            dfs(digits, index + 1);
            path.resize(path.size() - 1);
        }
    }
    vector<string> letterCombinations(string digits) {
        if (digits == "") return res;
        dfs(digits, 0);
        return res;
    }
};
```
