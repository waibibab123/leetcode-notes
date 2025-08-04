# 237、删除链表中的节点
题目难度：mid

题目网址：https://leetcode.cn/problems/delete-node-in-a-linked-list/description/

代码语言：cpp

## 题解
### 方法一、链表
这是一道很有意思的题目，刚开始看到的时候感觉很奇怪，只给出了一个结点，根本拿不到这个结点的前一个结点，那么怎么可能把这个结点删除呢，但仔细
看了题目发现有这么一句话：“删除节点并不是指从内存中删除它”，所有想到将需要删除的这个元素与下一个元素进行值交换，然后删除下一个元素就可以了

**代码**

C++

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    void deleteNode(ListNode* node) {
        swap(node->val, node->next->val);
        node->next = node->next->next;
    }
};
```
