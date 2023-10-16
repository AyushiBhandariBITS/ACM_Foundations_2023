# Queues

A queue is a linear data structure in which insertions are done at one end (rear) and deletions are done at the other end (front). The first element to be inserted is the first one to be deleted. Hence, it's called as a First In First Out (FIFO) list.

A Queue is like a line waiting to purchase tickets, where the first person in line is the first person served. (i.e. First come first serve).

![](C:\Users\Ayushi\AppData\Roaming\marktext\images\2023-10-15-23-44-59-image.png)

The queue has two pointers, **Front** and **Rear**. The front points towards the first element while the rear points towards the last element of the queue.

##### Queue Operations

1. `enQueue(int data)` :Inserts and element at the end of the queue. This operation adds a new node after the rear and moves the *rear pointer* to the new node added.

2. `deQueue()`: Removes and returns the elemnt at the front of the queue.This operation removes the front node and moves the *front pointer* to the next node.

3. `isEmpty()`: Indicates whether no elements are stored.

4. `front()`: Returns the element at the front withput removing it from the queue.

5. `QueueSize()`: Returns the number of elements stored in the queue.

##### Implementation of Queue in Python using Linked List

First we'll define a class `Node` - A linked list node to store queue entry

```python
class Node:
 
    def __init__(self, data):
        self.data = data
        self.next = None
```

<img title="" src="file:///C:/Users/Ayushi/AppData/Roaming/marktext/images/2023-10-16-19-51-40-image.png" alt="" data-align="center" width="202">

Then we define a class `Queue`. Its constructor will have 2 pointer: **Front and Rear**. Initially, since the queue is empty, Both of them point at `None`

```python
class Queue:
 
    def __init__(self):
        self.front = self.rear = None


```

<img title="" src="file:///C:/Users/Ayushi/AppData/Roaming/marktext/images/2023-10-16-20-28-45-image.png" alt="" width="207" data-align="center">

**Defining EnQueue(item)**

```python
def EnQueue(self, item):
        temp = Node(item)
 
        if self.rear == None:
            self.front = self.rear = temp
            return
        self.rear.next = temp
        self.rear = temp
```

Case (a): When the Queue is empty initially

<img title="" src="file:///C:/Users/Ayushi/AppData/Roaming/marktext/images/2023-10-16-20-21-03-image.png" alt="" data-align="left" width="222">

Case (b): When the Queue has some elements

<img src="file:///C:/Users/Ayushi/AppData/Roaming/marktext/images/2023-10-16-20-24-49-image.png" title="" alt="" data-align="right">

**Defining DeQueue():**

```python
  def DeQueue(self):
 
        if self.isEmpty():
            return
        temp = self.front
        self.front = temp.next
 
        if(self.front == None):
            self.rear = None
```

![](C:\Users\Ayushi\AppData\Roaming\marktext\images\2023-10-16-20-41-56-image.png)



**Defining isEmpty ():**

```python
    def isEmpty(self):
        return self.front == None
```

**Defining front():**

```python
def front(self):
    return self.front
```

##### Question: Flatten Nested List Iterator

**Description:** You are given a nested list of integers `nestedList`. Each element is either an integer or a list whose elements may also be integers or other lists. Implement an iterator to flatten it.

Implement the `NestedIterator` class:

- `NestedIterator(List<NestedInteger> nestedList)` Initializes the iterator with the nested list `nestedList`.
- `int next()` Returns the next integer in the nested list.
- `boolean hasNext()` Returns `true` if there are still some integers in the nested list and `false` otherwise.

Your code will be tested with the following pseudocode:

```
initialize iterator with nestedList
res = []
while iterator.hasNext()
 append iterator.next() to the end of res
return res
```

If `res` matches the expected flattened list, then your code will be judged as correct.

**Example 1:**

**Input:** nestedList = [[1,1],2,[1,1]]
**Output:** [1,1,2,1,1]
**Explanation:** By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,1,2,1,1].

**Example 2:**

**Input:** nestedList = [1,[4,[6]]]
**Output:** [1,4,6]
**Explanation:** By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,4,6].

**Constraints:**

- `1 <= nestedList.length <= 500`
- The values of the integers in the nested list is in the range `[-106, 106]`.

**Assumptions:**

The question has already defines a **NestedInteger** class with the functions `isInteger()` , `getInteger()` and `getList()`.

We have to implement the **NestedIterator** class.

```python
# This is the interface that allows for creating nested lists.
# You should not implement it, or speculate about its implementation
# class NestedInteger(object):
#    def isInteger(self):
#        @return True if this NestedInteger holds a single integer, rather than a nested list.
#        :rtype bool
#    def getInteger(self):
#        @return the single integer that this NestedInteger holds, if it holds a single integer
#        Return None if this NestedInteger holds a nested list
#        :rtype int
#    def getList(self):
#       return the nested list that this NestedInteger holds, if it holds a nested list
#        Return None if this NestedInteger holds a single integer
#        :rtype List[NestedInteger]

class NestedIterator(object):
    def __init__(self, nestedList):
        """
        Initialize your data structure here.
        :type nestedList: List[NestedInteger]
        """
    def next(self):
        """
        :rtype: int
        """
    def hasNext(self):
        """
        :rtype: bool
        """
# Your NestedIterator object will be instantiated and called as such:
# i, v = NestedIterator(nestedList), []
# while i.hasNext(): v.append(i.next())
```

**Solution:**

*Basically, if you find an integer, add it to the queue or else if you find a nested list, use the function recursively to search for integers in that particular nested list and hence add it to the final queue.*



**Code:**

```python
import queue
class NestedIterator(object):

    def __init__(self, nestedList):
        self.flattenedList= queue.Queue()
        self.flatten(nestedList)

    def flatten(self , nestedList):
        for x in nestedList:
            if x.isInteger():
                self.flattenedList.put(x.getInteger()) 
            else:
                self.flatten(x.getList())   

    def next(self):
        return self.flattenedList.get()

    def hasNext(self):
        return not(self.flattenedList.empty())
```








