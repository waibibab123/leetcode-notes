# 134、加油站
首先算出来每个坐标处gas与cost的差值，记为数组diff，如果diff所有元素之和小于0，则直接返回-1

否则，说明必然有解，那么这个起始坐标在哪里呢？这个起始坐标对应的元素在diff数组中是一个尽可能靠前的正数，并且满足：这个正数加上后面所有的数大于等于0，如果不满足，那么我们就找下一个正数：

例如：100，-99，-2,2，刚开始我们选的是100，但是遍历到下标2时发现此时已经没油了，因此重置我们的选择继续向后找下一个正数，直到我们找到2

C++
```cpp
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        vector<int> diff;
        int sum = 0;
        for (int i = 0; i < gas.size(); i ++ ) {
            diff.push_back(gas[i] - cost[i]);
            sum += diff[i];
        }
        if (sum < 0) return -1;
        int res = -1;
        sum = 0;
        for (int i = 0; i < diff.size(); i ++ ) {
            if (sum == 0) res = i;
            sum += diff[i];
            if (sum < 0){
                res = -1;
                sum = 0;
            }
        }
        return res;
    }
};
```
