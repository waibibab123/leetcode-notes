# 138、随机链表的复制
mid

cpp
## 题解
分三个步骤：
* 在每个结点cur的后面添加一个cur的备份，其中random域暂时赋值为null
* 给每个cur的备份的random域赋值，指向的元素必须也是备份的结点
* 将每个结点与它后面的备份结点进行剥离

C++
```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        if (head == NULL) return NULL;
        for (Node* cur = head; cur; cur = cur->next->next) {
            cur->next = new Node(cur->val, cur->next, NULL);
        }
        for (Node* cur = head; cur; cur = cur->next->next) {
            if (cur->random) {
                cur->next->random = cur->random->next;
            }
        }
        Node* head_new = head->next;
        Node* cur = head;
        for (; cur->next->next; cur = cur->next) {
            Node* copy = cur->next;
            cur->next = copy->next;
            copy->next = copy->next->next;
        }
        cur->next = NULL;
        return head_new;
    }
};
```
