# 142、 环形链表
题目难度：mid

题目网址：https://leetcode.cn/problems/linked-list-cycle-ii/description/

代码语言：cpp
## 题解
![](images/2.jpg)
我们分别让快（一次走两格）慢（一次走一格）指针同时从起点出发，若相遇，则有环，否则无环

当有环时，我们根据上图可以推出，再分别让一个指针从起点、相遇点出发，再相遇位置必为环入口

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
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                slow = head;
                while (slow != fast) {
                    slow = slow->next;
                    fast = fast->next;
                }
                return slow;
            }
        }
        return NULL;
    }
};
```
