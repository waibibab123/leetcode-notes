# 203、移除链表元素
题目网址：https://leetcode.cn/problems/remove-linked-list-elements/description/

题目难度：easy

代码语言：cpp，java
## 题解
### 方法一、链表，使用虚拟头结点
非常简单，直接看代码

**代码**

C++
```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy = new ListNode(0, head);
        ListNode* cur = dummy;
        while (cur->next) {
            if (cur->next->val == val) cur->next = cur->next->next;
            else cur = cur->next;
        }
        return dummy->next;
    }
};
```
java
```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0, head);
        ListNode cur = dummy;
        while (cur.next != null) {
            if (cur.next.val == val) cur.next = cur.next.next;
            else cur = cur.next;
        }
        return dummy.next;
    }
}
```
