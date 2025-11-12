# 86、分割链表
mid

cpp
## 题解
1. 总体思路：使用虚拟节点，不断将小于x的结点插入前部
2. 维护三个指针
   * p：始终指向已经遍历过的节点中最后一个小于x的，并且这个结点已经插到链表前部
   * cur：当前遍历到的节点
   * pre：当前遍历到的节点的上一个结点
3. 遍历过程：三种情况
   * 若cur的值大于等于x：最简单的情况，直接让cur和pre后移一个结点
   * 若cur的值小于x但是cur==p->next：这种情况下，不用将cur往前插，因为本身就是在前部了，所以只需让p、cur、pre均后移一个结点即可
   * 若cur的值小于x且cur!=p->next：这种情况下，就需要将cur指向的节点插入前部，具体见代码
  
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
    ListNode* partition(ListNode* head, int x) {
        ListNode dummy(0, head);
        ListNode* pre = &dummy;
        ListNode* cur = head;
        ListNode* p = &dummy;
        while (cur) {
            if (cur->val >= x || (cur->val < x && cur == p->next)) {
                if (cur->val < x) p = p->next;
                cur = cur->next;
                pre = pre->next;
            } else {
                pre->next = cur->next;
                cur->next = p->next;
                p->next = cur;
                cur = pre->next;
                p = p->next;
            }
        }
        return dummy.next;
    }
};
```
