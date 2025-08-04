# 707、设计链表
题目网址：https://leetcode.cn/problems/design-linked-list/description/

题目难度：mid

代码语言：cpp

## 题解
使用虚拟头结点以便进行插入、删除等操作，以下代码为准

C++
```cpp
class LinkNode {
public:
    int val;
    LinkNode* next;
    LinkNode(){}
    LinkNode(int val) : val(val){}
    LinkNode(int val, LinkNode* next) : val(val), next(next){}
};
class MyLinkedList {
private:
    LinkNode* dummy;
    int size;
public:
    MyLinkedList() {
        dummy = new LinkNode(0, NULL);
        size = 0;
    }
    
    int get(int index) {
        if (index >= size || index < 0) return -1;
        LinkNode* cur = dummy;
        while(index -- ) cur = cur->next;
        return cur->next->val;
    }
    
    void addAtHead(int val) {
        LinkNode* node = new LinkNode(val, dummy->next);
        dummy->next = node;
        size ++ ;
    }
    
    void addAtTail(int val) {
        LinkNode* node = new LinkNode(val, NULL);
        LinkNode* cur = dummy;
        while (cur->next) cur = cur->next;
        cur->next = node;
        size ++ ;
    }
    
    void addAtIndex(int index, int val) {
        if (index < 0 || index > size) return;
        if (index == size) {
            addAtTail(val);
            return;
        }
        LinkNode* cur = dummy;
        while (index -- ) cur = cur->next;
        LinkNode* node = new LinkNode(val, cur->next);
        cur->next = node;
        size ++ ;
    }
    
    void deleteAtIndex(int index) {
        if (index < 0 || index >= size) return;
        LinkNode* cur = dummy;
        while (index -- ) cur = cur->next;
        cur->next = cur->next->next;
        size -- ;
    }
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
```
