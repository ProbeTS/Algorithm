# 232. Implement Queue using Stacks

Implement the following operations of a queue using stacks.

- push(x) -- Push element x to the back of queue.
- pop() -- Removes the element from in front of queue.
- peek() -- Get the front element.
- empty() -- Return whether the queue is empty.

**Example:**

```
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // returns 1
queue.pop();   // returns 1
queue.empty(); // returns false
```

## Solution

We can initialize two stack, s1 and s2. s1 is the main stack and s2 is the assistant stack. 

During the push operation of MyQueue, just s1.push().

During the top operation of MyQueue, pop all the elements in s1 to the s2. Then the top of s2 is the top of MyQueue. Finally, pop all the elements in s2 to s1.

During the pop operation of MyQueue, the general process is the same as the top operation but pop the top of the MyQueue.

 During the empty operation of MyQueue, just return s1.empty() & s2.empty().

```C++
class MyQueue {
public:
    stack<int> s1, s2;
    
    /** Initialize your data structure here. */
    MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        s1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        while (s1.size()) {
            s2.push(s1.top());
            s1.pop();
        }
        int x = s2.top();
        s2.pop();
        while (s2.size()) {
            s1.push(s2.top());
            s2.pop();
        }
        return x;
    }
    
    /** Get the front element. */
    int peek() {
        while (s1.size()) {
            s2.push(s1.top());
            s1.pop();
        }
        int x = s2.top();
        while (s2.size()) {
            s1.push(s2.top());
            s2.pop();
        }
        return x;
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return s1.empty() & s2.empty();
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

​     