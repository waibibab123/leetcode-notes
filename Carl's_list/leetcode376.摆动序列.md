# 376、摆动序列
维护两个变量，一个是上次的差值prediff，一个是本次的差值diff，然后开始遍历，只有当`(diff > 0 && prediff <= 0) || (diff < 0 && prediff >= 0)`时，让结果res++，并更新prediff至diff

为什么prediff可以等于0？主要为了解决初始的特殊情况：当序列前两个元素相等时，prediff会被初始化为 0，此时摆动序列的初始长度为 1（因为两个相等的元素只能算 1 个有效元素）。prediff=0表示 “上一个没有有效摆动方向”（比如初始时元素相等）
这时候，只要后续出现第一个非 0 的diff（正或负），就可以被视为摆动序列的 “第一次有效趋势”，从而触发长度累加。

为什么diff不能等于0？摆动序列的要求：只有差值为正（上升）或负（下降）时，才可能形成 “交替”。差值为 0（相邻元素相等）不属于 “上升” 或 “下降”，无法参与 “正负交替”。

C++
```cpp
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        int n = nums.size();
        if (n < 2) return n;
        int prediff = nums[1] - nums[0];
        int ret = prediff == 0 ? 1 : 2;
        for (int i = 2; i < n; i ++ ) {
            int diff = nums[i] - nums[i - 1];
            if ((diff > 0 && prediff <= 0) || (diff < 0 && prediff >= 0)) {
                ret ++ ;
                prediff = diff;
            }
        }
        return ret;
    }
};
```
