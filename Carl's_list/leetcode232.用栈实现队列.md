# 232、用栈实现队列
题目网址：https://leetcode.cn/problems/implement-queue-using-stacks/description/

题目难度：easy

代码语言：cpp

## 题解
准备两个栈st1和st2，具体操作如下：
* 入队：直接往st1中push数据
* 取队头元素：若st2不为空，直接取st2的栈顶，如果st2为空，则把st1的栈顶依次出栈并压入st2直到st1为空，随后再取st2栈顶
* 出队：先调用peek()，记录返回值res，调用之后弹出st2栈顶元素，返回res
* 判空：如果st1和st2均为空，则队列为空

C++

```cpp
class MyQueue {
public:
    stack<int> st1;
    stack<int> st2;
    MyQueue() {
        
    }
    
    void push(int x) {
        st1.push(x);
    }
    
    int pop() {
        int res = peek();
        st2.pop();
        return res;
    }
    
    int peek() {
        if (st2.empty()) {
            while (!st1.empty()) {
                st2.push(st1.top());
                st1.pop();
            }
        }
        return st2.top();
    }
    
    bool empty() {
        return st1.empty() && st2.empty();
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```
