# 179、最大数
难度：mid

题目网址：https://leetcode.cn/problems/largest-number/description/

代码语言：cpp

## 题解
### 方法一、贪心
我们可以将原数组以某种方式进行排序，要使排序之后从下标0到最后的数字拼接起来最大（全局最优），只需要使排序后的每两个相邻的数字a和b中，以a、b为顺序拼接出的整数一定大于以b、a为顺序拼接出的整数（局部最优），因此只需要自定义一个cmp函数，
将上述规则写入。

注意：拼接之后，一定要记得去掉答案字符串中的前导零！

C++

```cpp
class Solution {
private:
    static bool cmp(int a, int b) {
        string ab = to_string(a) + to_string(b);
        string ba = to_string(b) + to_string(a);
        return ab > ba;
    }
public:
    string largestNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end(), cmp);
        string res = "";
        for (int i = 0; i < nums.size(); i ++ ) res += to_string(nums[i]);
        while (res.length() > 1 && res[0] == '0') res = res.substr(1, res.length() - 1);
        return res;
    }
};
```
