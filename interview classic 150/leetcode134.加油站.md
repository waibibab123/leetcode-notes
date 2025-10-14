# 134、加油站
题目网址：https://leetcode.cn/problems/gas-station/?envType=study-plan-v2&envId=top-interview-150

题目难度：mid

代码语言：cpp
## 题解
贪心

判断可行性：首先计算每站的「剩余油量」（gas [i] - cost [i]），如果所有站的剩余油量总和小于 0，说明无论从哪出发都无法绕一圈，直接返回 - 1。

寻找起点：如果整体可行，就从第 0 站开始尝试：
* 累计当前的剩余油量（temp_sum）
* 若累计值小于 0，说明从当前起点到当前站之间的所有站点都不能作为起点，将起点更新为下一站（i+1），并重置累计值
* 返回结果：循环结束后，最后的起点就是答案

C++
```cpp
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n = gas.size();
        int sum = 0;
        vector<int> diff(n, 0);
        for (int i = 0; i < n; i ++ ) {
            diff[i] = gas[i] - cost[i];
            sum += diff[i];
        }
        if (sum < 0) return -1;
        int res = 0;
        int temp_sum = 0;
        for (int i = 0; i < n; i ++ ) {
            temp_sum += diff[i];
            if (temp_sum < 0) {
                temp_sum = 0;
                res = i + 1;
            }
        }
        return res;
    }
};
```
