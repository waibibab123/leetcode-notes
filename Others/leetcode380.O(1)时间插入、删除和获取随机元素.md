# 380、O（1）时间插入、删除和获取随机元素

题目网址：https://leetcode.cn/problems/insert-delete-getrandom-o1/description/

题目难度：mid

代码语言：cpp

## 题解
### 方法一、哈希
思路来源：https://leetcode.cn/problems/insert-delete-getrandom-o1/solutions/468200/cchang-shu-shi-jian-cha-ru-shan-chu-he-huo-qu-sui-/

用一个vector和一个unordered_map来共同完成这个数据结构

**1、插入元素**

直接在数组后push_back这个val，并且在hash中记录这个val对应数组的下标位置即可

**2、删除元素**

先将要删除的元素与数组最后一个元素交换位置，之后直接使用pop_back()函数在O（1）的复杂度内完成删除，随后更新哈希表即可

**3、获取元素**

使用C++的rand()函数，先对数组长度取模，然后直接返回对应下标的元素即可

**代码**

C++

```cpp
class RandomizedSet {
public:
    unordered_map<int, int> hash;
    vector<int> nums;
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
        int val_pos = hash[val];
        int last_pos = nums.size() - 1;
        nums[val_pos] = nums[last_pos];
        nums.pop_back();
        hash[nums[val_pos]] = val_pos;
        hash.erase(val);
        return true;
    }
    
    int getRandom() {
        int index = rand() % nums.size();
        return nums[index];
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
