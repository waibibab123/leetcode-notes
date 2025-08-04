# 341、扁平化嵌套列表迭代器

题目难度：mid

题目网址：https://leetcode.cn/problems/flatten-nested-list-iterator/description/

代码语言：cpp

## 题解
### 方法一、栈
思路来源：https://leetcode.cn/problems/flatten-nested-list-iterator/solutions/162992/python-zhan-dai-ma-jian-dan-yi-li-jie-by-hsyv5897/

我们维护一个栈，初始化时，将nestedList中的内容反转之后全部入栈，由于任何时候调用next函数之前要先调用hasNext，因此，只需要在hasNext中保证栈顶元素始终为整数，那么就可以在next中直接返回栈顶元素了，因此接下来的关键是hasNext的设计。

在hasNext中，我们只需要依次判断栈顶元素是不是整数，如果不是，那么就将这个列表反转后，**将列表中的元素**依次入栈，直到栈顶元素为整数即可

举一个例子，`[[1,2],3,[4,5]]`，初始化入栈：`[4,5],3,[1,2]`，调用hasNext变成：`[4,5],3,2,1`

**代码**

C++

```cpp
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */

class NestedIterator {
public:
    vector<NestedInteger> stack;
    NestedIterator(vector<NestedInteger> &nestedList) {
        stack = nestedList;
        reverse(stack.begin(), stack.end());
    }
    
    int next() {
        int res = stack.back().getInteger();
        stack.pop_back();
        return res;
    }
    
    bool hasNext() {
        while (stack.size() && !stack.back().isInteger()) {
            auto temp = stack.back().getList();
            stack.pop_back();
            for (int i = temp.size() - 1; i >= 0; i -- ) stack.push_back(temp[i]);
        }
        return stack.size();
    }
};

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */
```
