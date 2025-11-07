# 224、基本计算器
题目难度：hard

代码语言：cpp

## 题解
这道题与acwing3302不同：
* 只有加法和减法
* 存在各种各样的空格
* 存在负数

参考[Spectre](https://leetcode.cn/u/phantomspectre/)的题解
```
1、题目中的符号只有+、-、(、)和空格，也就是只有加减和左右括号，其它的都是数字；如果题目中没有左右括号，那么将是个简单题，依次遍历相加或者相减即可
2、那么考虑，能否除去括号，除去括号，变化的是括号内部的数字前面的符号
（1）如果括号外面是正号，里面都不变
（2）如果括号外面是负号，里面都变相反号，例如 -(3 + 4 - (2 + 8))，括号里面的3和4都变负了，2和8先变-2和-8再变2和8（因为两个负号）
3、综上，申请一个栈，记录左括号外的的符号，对括号内的数字都变号，如果遇到右括号，则弹出栈顶的符号
4、现申请一个sign=1，表明当前的符号为正，和一个栈，栈顶为+1，即对字符串s最外面包括一层括号，且括号外是+号；遍历s
（1）当s[i]为空时，++i，跳过
（2）当s[i]为+时，当前的符号 sign = +1 * stk.top()
（3）当s[i]为- 时，当前的符号 sign = -1 * stk.top()
（4）当s[i]为( 时，将当前sign压入栈中，栈中始终记录的是当前左括号前的符号
（5）当s[i]为) 时，弹栈
（6）遇到数字时，恢复原本的数字，num = num * 10 + s[i] - '0'，直到遇到下一个+、-、(、)或空，结算sign * num到ans中，sign始终是当前数字前的正负号
5、最后返回ans

作者：Spectre
链接：https://leetcode.cn/problems/basic-calculator/solutions/3753196/ji-ben-ji-suan-qi-by-virile_tao-1wi5/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

C++
```cpp
class Solution {
public:
    int calculate(string s) {
        stack<int> st;
        int sign = 1;
        st.push(1);
        int res = 0;
        for (int i = 0; i < s.length(); i ++ ) {
            if (s[i] == ' ') continue;
            else if (s[i] == '+') {
                sign = st.top();
            } 
            else if (s[i] == '-') {
                sign = -st.top();
            } 
            else if (s[i] == '(') {
                st.push(sign);
            } 
            else if (s[i] == ')') {
                st.pop();
            } 
            else {
                int temp = s[i] - '0';
                while (i + 1 < s.length() && isdigit(s[i + 1])) {
                    temp = temp * 10 - '0' + s[i + 1];
                    i ++ ;
                }
                res += sign * temp;
            }
        }
        return res;
    }
};
```
