# 82、删除排序链表中的重复元素2
mid

cpp
## 题解
C++
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode dummy(0, NULL);
        ListNode* p = &dummy;
        ListNode* cur = head;
        while (cur) {
            if (cur->next && cur->val == cur->next->val) {
                while (cur->next && cur->val == cur->next->val) cur = cur->next;
                cur = cur->next;
            } 
            else 
            {
                p->next = new ListNode(cur->val);
                p = p->next;
                cur = cur->next;
            }
        }
        return dummy.next;
    }
};
```
