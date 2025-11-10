# 92、反转链表2
mid

cpp
## 题解
206、反转链表的加强版

可以分为以下几步：
* 通过right值，确定反转后链表的最后一个结点的指向位置end
* 通过left，确定开始反转链表的起点cur
* 使用206的反转链表经典while循环进行一段的链表反转，区别在于原来的循环条件cur != NULL改为cur != end
* 反转之后：
  * 如果left == 1，那么pre就是所求的答案
  * 如果left != 1，需要将前半段和后半段链表断开的地方进行连接

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
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        ListNode* pre = head;
        while (right -- ) pre = pre->next;
        ListNode* end = pre;
        ListNode* cur = head;
        for (int i = 1; i < left; i ++ ) cur = cur->next;
        while (cur != end) {
            ListNode* nxt = cur->next;
            cur->next = pre;
            pre = cur;
            cur = nxt;
        }
        if (left == 1) return pre;
        ListNode* pre_head = head;
        for (int i = 1; i < left - 1; i ++ ) pre_head = pre_head->next;
        pre_head->next = pre;
        return head;
    }
};
```
