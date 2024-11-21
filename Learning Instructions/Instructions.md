<img src="./Images/Topics.JPG?raw=true" alt="PCA1" title="PCA1" width="1000"/>

### Order of learning

<img src="./Images/Order.JPG?raw=true" alt="PCA1" title="PCA1" width="1000"/>

## 1. Arrays

<img src="./Images/Arrays.JPG?raw=true" alt="PCA1" title="PCA1" width="100"/>      

An array organizes items sequentially, one after another in memory. Each position in the array has an index, starting at 0. 

#### Strengths:

* Fast lookups. Retrieving the element at a given index takes O(1) time, regardless of the length of the array.
* Fast appends. Adding a new element at the end of the array takes O(1) time, if the array has space.
  
#### Weaknesses:

* Fixed size. You need to specify how many elements you're going to store in your array ahead of time. (Unless you're using a fancy dynamic array.)
* Costly inserts and deletes. You have to "scoot over" the other elements to fill in or close gaps, which takes worst-case O(n) time.

 #### Arrays in python are dynamic arrays by default. so they can be used as stack.
 
* A dynamic array is an array with a big improvement: automatic resizing.
One limitation of arrays is that they're fixed size, meaning you need to specify the number of elements your array will hold ahead of time.
A dynamic array expands as you add more elements. So you don't need to determine the size ahead of time.

```python 
#Arrays
arr = [1,2,3]
arr.append(4)
print(arr)
arr.pop() #drops number from end of the array
print(arr)
```
[1, 2, 3, 4]

[1, 2, 3]

More about arrays Operations: [Arrays](https://github.com/SainaPolis/LeetCode_Notes/blob/main/01.Arrays/Arrays.ipynb)

## 2. Linked Lists

A linked list organizes items sequentially, with each item storing a pointer to the next one.

Picture a linked list like a chain of paperclips linked together. It's quick to add another paperclip to the top or bottom. It's even quick to insert one in the middle—just disconnect the chain at the middle link, add the new paperclip, then reconnect the other half.

An item in a linked list is called a node. The first node is called the head. The last node is called the tail.

<img src="./Images/LinkedList.JPG?raw=true" alt="PCA1" title="PCA1" width="500"/>   

Strengths:
Fast operations on the ends. Adding elements at either end of a linked list is O(1). Removing the first element is also O(1).
Flexible size. There's no need to specify how many elements you're going to store ahead of time. You can keep adding elements as long as there's enough space on the machine.
* Weaknesses: Costly lookups. To access or edit an item in a linked list, you have to take O(i) time to walk from the head of the list to the ith item.
* Uses: Stacks and queues only need fast operations on the ends, so linked lists are ideal.

```python
# Node Class
class Node:
    def __init__(self, data):
        self.data = data  # Holds the data
        self.next = None  # Points to the next node

# LinkedList Class
class LinkedList:
    def __init__(self):
        self.head = None  # Initialize the head of the list

    # Add a node at the end
    def append(self, data):
        new_node = Node(data)
        if not self.head:  # If the list is empty
            self.head = new_node
            return
        last_node = self.head
        while last_node.next:  # Traverse to the end of the list
            last_node = last_node.next
        last_node.next = new_node

    # Add a node at the beginning
    def prepend(self, data):
        new_node = Node(data)
        new_node.next = self.head  # New node points to the current head
        self.head = new_node

    # Delete a node by value
    def delete(self, key):
        temp = self.head

        # If the head node itself holds the key
        if temp and temp.data == key:
            self.head = temp.next
            temp = None
            return

        # Search for the key to be deleted
        prev = None
        while temp and temp.data != key:
            prev = temp
            temp = temp.next

        # Key not found
        if temp is None:
            return

        # Unlink the node from the linked list
        prev.next = temp.next
        temp = None

    # Print the linked list
    def print_list(self):
        current = self.head
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")

    # Search for an element
    def search(self, key):
        current = self.head
        while current:
            if current.data == key:
                return True
            current = current.next
        return False

# Example Usage
if __name__ == "__main__":
    llist = LinkedList()
    llist.append(10)
    llist.append(20)
    llist.prepend(5)
    llist.print_list()  # Output: 5 -> 10 -> 20 -> None
    llist.delete(10)
    llist.print_list()  # Output: 5 -> 20 -> None
    print(llist.search(20))  # Output: True
    print(llist.search(30))  # Output: False

```
## 3. Stacks

A stack stores items in a last-in, first-out (LIFO) order.

<p float="left">
  <img src="./Images/1_uJlB-5Gi87NI9jsiQx2aBA.gif?raw=true" alt="PCA1" title="PCA1" width="200"/> 
  
  <img src="./Images/1_kYeGEFzxOFftWK49hczjOg.gif?raw=true" alt="PCA1" title="PCA1" width="200"/>
</p>

Strengths:
Fast operations. All stack operations take O(1) time.

#### Stack Implementation using List

```python
# Stack Implementation using List
class Stack:
    def __init__(self):
        self.stack = []  # Initialize an empty stack

    # Check if the stack is empty
    def is_empty(self):
        return len(self.stack) == 0

    # Push an element onto the stack
    def push(self, data):
        self.stack.append(data)

    # Pop an element from the stack
    def pop(self):
        if self.is_empty():
            return "Stack is empty!"
        return self.stack.pop()

    # Peek at the top element of the stack
    def peek(self):
        if self.is_empty():
            return "Stack is empty!"
        return self.stack[-1]

    # Get the size of the stack
    def size(self):
        return len(self.stack)

    # Print the stack
    def print_stack(self):
        print("Stack:", self.stack[::-1])  # Print stack from top to bottom

# Example Usage
if __name__ == "__main__":
    stack = Stack()
    stack.push(10)
    stack.push(20)
    stack.push(30)
    stack.print_stack()  # Output: Stack: [30, 20, 10]
    print(stack.pop())   # Output: 30
    print(stack.peek())  # Output: 20
    print(stack.size())  # Output: 2
    print(stack.is_empty())  # Output: False
```

#### Stack Implementation using queue

```python
from collections import deque

# Stack Implementation using deque
class Stack:
    def __init__(self):
        self.stack = deque()

    def is_empty(self):
        return len(self.stack) == 0

    def push(self, data):
        self.stack.append(data)

    def pop(self):
        if self.is_empty():
            return "Stack is empty!"
        return self.stack.pop()

    def peek(self):
        if self.is_empty():
            return "Stack is empty!"
        return self.stack[-1]

    def size(self):
        return len(self.stack)

    def print_stack(self):
        print("Stack:", list(self.stack)[::-1])

# Example Usage
if __name__ == "__main__":
    stack = Stack()
    stack.push(5)
    stack.push(15)
    stack.push(25)
    stack.print_stack()  # Output: Stack: [25, 15, 5]
    print(stack.pop())   # Output: 25
    print(stack.peek())  # Output: 15
```
## 4. Queue

<img src="./Images/queue.gif?raw=true" alt="PCA1" title="PCA1" width="500"/>

* Strengths:
Fast operations. All queue operations take O(1) time.
* Uses
Breadth-first search uses a queue to keep track of the nodes to visit next.
Printers use queues to manage jobs—jobs get printed in the order they're submitted.
Web servers use queues to manage requests—page requests get fulfilled in the order they're received.
Processes wait in the CPU scheduler's queue for their turn to run.

More about queue Operations: [queues](https://github.com/SainaPolis/LeetCode_Notes/blob/main/03.Queue/Que.ipynb)

## 5. Two Pointers

The Two Pointers pattern involves using two pointers to iterate through an array or list, often used to find pairs or elements that meet specific criteria.

Use this pattern when dealing with sorted arrays or lists where you need to find pairs that satisfy a specific condition.

#### Sample Problem:

Find two numbers in a sorted array that add up to a target value.

#### Example:

Input: nums = [1, 2, 3, 4, 6], target = 6

Output: [1, 3]

#### Explanation:

Initialize two pointers, one at the start (left) and one at the end (right) of the array.

Check the sum of the elements at the two pointers.

If the sum equals the target, return the indices.

If the sum is less than the target, move the left pointer to the right.

If the sum is greater than the target, move the right pointer to the left.

```python

```

```python

```
