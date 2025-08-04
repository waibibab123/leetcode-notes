# 365、水壶问题
题目网址：https://leetcode.cn/problems/water-and-jug-problem/description/

题目难度：mid

代码语言：cpp
## 题解
### 方法一、数学
考虑以下三种特殊情况：

* A.两个水壶有没有可能同时有水，且不满？  根据三种可以执行的操作可知，只有一个水壶不满的情况，但绝对不可能两个水壶同时不满

* B.填满一个不满的水壶有没有意义？  没有意义，假设另一个水壶为空，那么填满一个不满的水壶等价于从初始状态给这个水壶加满水；假设另一个水壶是满的，那么填满这个不满的水壶相当于从初始状态分别给这两个水壶加满水

* C.把一个不满的水壶里面的水倒掉有没有意义？  没有意义，假设另一个水壶为空，那么把一个不满的水壶里面的水倒掉就回到了初始状态；而如果另一个水壶是满的，那么这个操作的结果等价于从初始状态直接给另一个水壶加满水


综上我们得出结论：每次操作只会让桶里的水**总量**增加x/y，或者减少x/y，因此，如果我们可以找到一对整数a，b使得ax + by = z且z <= x + y，说明目标可以达成。根据**裴蜀定理**知，ax + by = z的条件是`z % gcd(a,b) == 0`

**代码**

C++

```cpp
class Solution {
public:
    int gcd(int a, int b) {
        return !b ? a : gcd(b, a % b);
    }
    bool canMeasureWater(int x, int y, int target) {
        if (x + y < target) return false;
        return target % gcd(x, y) == 0;
    }
};
```
