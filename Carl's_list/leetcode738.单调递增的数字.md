# 738、单调递增的数字
贪心

思路：先找到第一次下降的数字，假设其下标为k，然后让下标k-1的元素减一然后让k以及后面的元素变为9，例如123454->123399

但出现一个问题：123354->123299不符合题意，因此找到k之后，假设k-1对应的元素还有p个元素值与k-1对应的元素相同，让这些元素的**第一个元素**减一，然后让后面变为9，比如1233333354，找到k之后，需要让第一个3减去一，然后让后面全变9，即
12229999999

此外，还有一个特殊情况，当这个元素减一之后，如果结果为0，需要去掉这个前导零

C++
```cpp
class Solution {
public:
    int monotoneIncreasingDigits(int n) {
        string num = to_string(n);
        int drop_index = -1;
        for (int i = 1; i < num.size(); i ++ ) {
            if (num[i] < num[i - 1]) {
                drop_index = i;
                break;
            }
        }
        if (drop_index == -1) return n;
        int decrease_index = drop_index - 1;
        for (; decrease_index >= 1; decrease_index -- ) {
            if (num[decrease_index] != num[decrease_index - 1]) break;
        }
        num[decrease_index] -- ;
        for (int i = decrease_index + 1; i < num.size(); i ++ ) num[i] = '9';
        if (num[0] == '0') num = num.substr(1);
        return stoi(num);
    }
};
```
