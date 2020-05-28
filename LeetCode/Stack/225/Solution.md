# 225. Implement Stack using Queues

Implement the following operations of a stack using queues.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- empty() -- Return whether the stack is empty.

**Example:**

```c++
MyStack stack = new MyStack();

stack.push(1);
stack.push(2);  
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false
```

## Solution1

We can initialize two queue, q1 and q2. q1 is the main queue and q2 is the assistant queue. 

During the push operation of MyStack, just q1.push().

During the top operation of MyStack, pop the elements in q1 to the q2 until there is only one element in q1.   Then the top of MyStack is the only one element in q1. Finally, pop all the elements in q2 to q1 including the top of MyStack.

During the pop operation of MyStack, the general process is the same as the top operation but pop the top of the MyStack.

 During the empty operation of MyStack, just return q1.empty() & q2.empty().

```C++
class MyStack {
public:
    queue<int> q1, q2;
    
    /** Initialize your data structure here. */
    MyStack() {
        
    }
    
    /** Push element x onto stack. */
    void push(int x) {
        q1.push(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        while (q1.size() != 1) {
            q2.push(q1.front());
            q1.pop();
        }
        int x = q1.front();
        q1.pop();
        while (q2.size()) {
            q1.push(q2.front());
            q2.pop();
        }
        return x;
    }
    
    /** Get the top element. */
    int top() {
        while (q1.size() != 1) {
            q2.push(q1.front());
            q1.pop();
        }
        int x = q1.front();
        q1.pop();
        while (q2.size()) {
            q1.push(q2.front());
            q2.pop();
        }
        q1.push(x);
        return x;
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return q1.empty() & q2.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```

## Solution2

We can initialize one queue and use its back method.

```c++
class MyStack {
public:
    queue<int> q;
    
    /** Initialize your data structure here. */
    MyStack() {
        
    }
    
    /** Push element x onto stack. */
    void push(int x) {
        q.push(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int t = top();
        while (t != q.front()) {
            q.push(q.front());
            q.pop();
        }
        q.pop();
        return t;
    }
    
    /** Get the top element. */
    int top() {
        return q.back();
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return q.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```