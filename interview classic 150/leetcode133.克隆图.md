# 133、克隆图
mid

cpp
## 题解
```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/

class Solution {
public:
    unordered_map<int, Node*> mp;
    Node* cloneGraph(Node* node) {
        if (node == NULL) return NULL;
        Node* res = new Node(node->val);
        mp[res->val] = res;
        for (int i = 0; i < node->neighbors.size(); i ++ ) {
            if (!mp.count(node->neighbors[i]->val)) {
                Node* temp = cloneGraph(node->neighbors[i]);
                mp[node->neighbors[i]->val] = temp;
            }
            res->neighbors.push_back(mp[node->neighbors[i]->val]);
        }
        return res;
    }
};
```
