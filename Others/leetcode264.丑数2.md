# 264、丑数2
题目难度：mid

题目网址：https://leetcode.cn/problems/ugly-number-ii/description/

代码语言：cpp

## 题解
### 方法一、堆
思路来源：[力扣：宫水三叶大佬的题解](https://leetcode.cn/problems/ugly-number-ii/solutions/714340/gong-shui-san-xie-yi-ti-shuang-jie-you-x-3nvs/)

根据丑数的定义可知，如果一个丑数x与（2,3,5）想乘，结果也必然是丑数

因此这道题可以使用堆：

step1.起始先将最小丑数1放入堆

step2.每次从堆中弹出最小值x，然后将x所对应的丑数2x、3x、5x入堆

step3.对步骤2循环多次，第n次弹出的值即是答案

为了防止同一个丑数多次入对堆，我们可以使用set保存之前入堆的所有丑数

**代码**

C++

```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        int nums[] = {2, 3, 5};
        set<int> S;
        priority_queue<int, vector<int>, greater<int>> q;
        q.push(1);
        S.insert(1);
        for (int i = 1; i <= n; i ++ ) {
            int x = q.top();
            q.pop();
            // cout << x << endl;
            if (i == n) return x;
            for (int j = 0; j < 3; j ++ ) {
                if (x > INT_MAX / nums[j]) break;
                int temp = x * nums[j];
                if (!S.contains(temp)) {
                    S.insert(temp);
                    q.push(temp);
                }
            }
        }
        return -1;
    }
};
```
