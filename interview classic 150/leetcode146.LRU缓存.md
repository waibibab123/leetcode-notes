# 146、LRU缓存
mid

cpp
## 题解
双向循环链表

在最前面的是最新的，在最后面的是最近未使用的结点

封装一个专门get结点的函数get_node，每次get都将这个结点从后面拉到前面，拉的过程涉及两个功能，即删除节点remove和向前面插入节点push_front

那么：
构造函数：构造一个虚拟节点满足双向循环链表的特性

get：调用get_node，微调

put：不管是否存在都访问了这个结点，先调用get_node确保从后面拉到前面
* 若已存在，直接更新
* 不存在，插入，若超容量，去除最后的节点，由于是双向循环链表，最后节点就是虚拟节点的上一个结点

C++
```cpp
class Node{
public:
    int key;
    int value;
    Node* next;
    Node* prev;
    Node(int key = 0, int value = 0) : key(key), value(value) {}
};
class LRUCache {
private:
    int capacity;
    Node* dummy;
    unordered_map<int, Node*> key_to_node;
    void remove(Node* node) {
        node->next->prev = node->prev;
        node->prev->next = node->next;
    }
    void push_front(Node* node) {
        node->next = dummy->next;
        node->prev = dummy;
        dummy->next->prev = node;
        dummy->next = node;
    }
    Node* get_node(int key) {
        if (!key_to_node.count(key)) return NULL;
        Node* node = key_to_node[key];
        remove(node);
        push_front(node);
        return node;
    }
public:
    LRUCache(int capacity) {
        this->capacity = capacity;
        dummy = new Node();
        dummy->next = dummy;
        dummy->prev = dummy;
    }
    
    int get(int key) {
        Node* node = get_node(key);
        return node == NULL ? -1 : node->value;
    }
    
    void put(int key, int value) {
        Node* node = get_node(key);
        if (node != NULL) {
            node->value = value;
            return;
        }
        node = new Node(key, value);
        key_to_node[key] = node;
        push_front(node);
        if (key_to_node.size() > capacity) {
            Node* old = dummy->prev;
            remove(old);
            key_to_node.erase(old->key);
            delete old;
        }
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
