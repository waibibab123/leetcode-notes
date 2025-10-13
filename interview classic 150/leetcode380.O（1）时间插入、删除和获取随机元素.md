# 380、O（1）时间插入、删除和获取随机元素
题目网址：https://leetcode.cn/problems/insert-delete-getrandom-o1/description/?envType=study-plan-v2&envId=top-interview-150

题目难度：mid

代码语言：cpp
## 题解
1.unordered_map的插入、删除、获取元素的平均时间复杂度为O（1）

2.使用类似acwing839的处理方式去进行元素的删除

3.注意代码注释部分hash的键删除必须放在最后，否则当val == nums.back()时，会发生错误

C++
```cpp
class RandomizedSet {
public:
    vector<int> nums;
    unordered_map<int, int> hash;
    RandomizedSet() {

    }
    
    bool insert(int val) {
        if (hash.count(val)) return false;
        nums.push_back(val);
        hash[val] = nums.size() - 1;
        return true; 
    }
    
    bool remove(int val) {
        if (!hash.count(val)) return false;
        int pos = hash[val];
        nums[pos] = nums.back();
        nums.pop_back();
        hash[nums[pos]] = pos;
        hash.erase(val);//一定要放在最后
        return true;
    }
    
    int getRandom() {
        int pos = rand() % nums.size();
        return nums[pos];
    }
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```
