# Python Abstract Data Types (ADTs) Guide in Hinglish

## 📚 Table of Contents

1. [List](#list)
2. [Stack](#stack)
3. [Queue](#queue)
4. [Deque (Double-Ended Queue)](#deque)
5. [Linked List](#linked-list)
6. [Hash Table / Hash Map](#hash-table)
7. [Hash Set](#hash-set)
8. [Tree](#tree)
9. [Binary Search Tree (BST)](#binary-search-tree)
10. [Heap (Min-Heap / Max-Heap)](#heap)
11. [Graph](#graph)
12. [Set](#set)
13. [Trie (Prefix Tree)](#trie)
14. [Priority Queue](#priority-queue)
15. [Matrix (2D Array as ADT)](#matrix)
16. [Circular Queue](#circular-queue)
17. [Circular Linked List](#circular-linked-list)
18. [Multiset / Bag](#multiset)

---

<a id="list"></a>
## 1. List

### Kya hai (What is it?)
List ek basic sequential ADT hai jisme ordered elements store hote hain.

### Implementation
Python mein built-in list hoti hai:

```python
# List banane ke tarike
my_list = []  # Empty list
my_list = [1, 2, 3, 4, 5]  # Pre-populated list
my_list = list()  # Using constructor
```

Ya fir custom implementation:

```python
class MyList:
    def __init__(self):
        self.items = []
        
    def add(self, item):
        self.items.append(item)
        
    def remove(self, index):
        if 0 <= index < len(self.items):
            return self.items.pop(index)
        raise IndexError("Index out of range")
        
    def get(self, index):
        if 0 <= index < len(self.items):
            return self.items[index]
        raise IndexError("Index out of range")
        
    def size(self):
        return len(self.items)
```

### Behavior/Operations
- **add/append**: Element ko end mein add karna (O(1))
- **insert**: Specific position par element add karna (O(n))
- **remove**: Element ko hatana (O(n))
- **get/access**: Index se element access karna (O(1))
- **update**: Element ko update karna (O(1))
- **search**: Element ko dhundhna (O(n))
- **slice**: List ka sub-section nikalna (O(k)) where k is slice size

### Kab aur Kahan Use Karein (When and Where to Use)
- Jab aapko elements ko **order maintain** karke rakhna ho
- Jab aapko **random access** (kisi bhi index par direct access) chahiye
- Jab aapko frequently **add/remove** operations end mein karne hon
- Data collection banane ke liye jab size pehle se pata na ho

### Special Features
- **Dynamic sizing**: automatically grow/shrink hoti hai
- **Heterogeneous data**: different types ke elements rakh sakte hain
- **Versatile**: Python mein sabse flexible data structure

---

<a id="stack"></a>
## 2. Stack

### Kya hai (What is it?)
Stack ek LIFO (Last In First Out) ADT hai - matlab jo last mein aaya wo pehle niklega.

```
    Top
    |
    v
   [30]
   [20]
   [10]
---------
```

### Implementation
```python
class Stack:
    def __init__(self):
        self.items = []
        
    def push(self, item):
        self.items.append(item)
        
    def pop(self):
        if not self.is_empty():
            return self.items.pop()
        raise IndexError("Pop from an empty stack")
        
    def peek(self):
        if not self.is_empty():
            return self.items[-1]
        raise IndexError("Peek from an empty stack")
        
    def is_empty(self):
        return len(self.items) == 0
        
    def size(self):
        return len(self.items)
```

### Behavior/Operations
- **push**: Element ko top par add karna (O(1))
- **pop**: Top element ko hatana aur return karna (O(1))
- **peek/top**: Top element ko dekna bina hataye (O(1))
- **is_empty**: Check karna ki stack khali hai ya nahi (O(1))
- **size**: Elements ki count (O(1))

### Kab aur Kahan Use Karein (When and Where to Use)
- **Function calls** ko track karne ke liye (call stack)
- **Undo** mechanism implement karne ke liye
- **Expression evaluation** (infix to postfix conversion)
- **Backtracking** algorithms mein
- **Syntax parsing** (brackets matching, etc.)
- **Depth-First Search** (DFS) implement karne ke liye

### Special Features
- **Restricted access**: Only top element ko access kar sakte hain
- **Simple implementation**: Very easy to implement
- **Memory efficient**: Fixed operations hi hain

---

<a id="queue"></a>
## 3. Queue

### Kya hai (What is it?)
Queue ek FIFO (First In First Out) ADT hai - matlab jo pehle aaya wo pehle niklega.

```
  Front          Rear
    |             |
    v             v
    [10]-[20]-[30]-[40]
    |             |
   Dequeue      Enqueue
```

### Implementation
```python
class Queue:
    def __init__(self):
        self.items = []
        
    def enqueue(self, item):
        self.items.append(item)
        
    def dequeue(self):
        if not self.is_empty():
            return self.items.pop(0)  # O(n) operation in Python lists
        raise IndexError("Dequeue from an empty queue")
        
    def front(self):
        if not self.is_empty():
            return self.items[0]
        raise IndexError("Front from an empty queue")
        
    def is_empty(self):
        return len(self.items) == 0
        
    def size(self):
        return len(self.items)
```

Better implementation using collections.deque:

```python
from collections import deque

class EfficientQueue:
    def __init__(self):
        self.items = deque()
        
    def enqueue(self, item):
        self.items.append(item)  # O(1)
        
    def dequeue(self):
        if not self.is_empty():
            return self.items.popleft()  # O(1)
        raise IndexError("Dequeue from an empty queue")
        
    def front(self):
        if not self.is_empty():
            return self.items[0]
        raise IndexError("Front from an empty queue")
        
    def is_empty(self):
        return len(self.items) == 0
        
    def size(self):
        return len(self.items)
```

### Behavior/Operations
- **enqueue**: Element ko end (rear) mein add karna (O(1))
- **dequeue**: Front element ko hatana aur return karna (O(1) with deque)
- **front/peek**: Front element ko dekhna bina hataye (O(1))
- **is_empty**: Check karna ki queue khali hai ya nahi (O(1))
- **size**: Elements ki count (O(1))

### Kab aur Kahan Use Karein (When and Where to Use)
- **Task scheduling** mein
- **Resource allocation** mein
- **Print queue** management mein
- **Breadth-First Search** (BFS) implement karne ke liye
- **Message queues** aur asynchronous processing mein
- Jab FIFO (First-In-First-Out) behavior chahiye

### Special Features
- **Order preservation**: Elements jis order mein aate hain usi order mein process hote hain
- **Fair processing**: Har element ko uski arrival order ke hisab se process kiya jata hai

---

<a id="deque"></a>
## 4. Deque (Double-Ended Queue)

### Kya hai (What is it?)
Deque (Double-Ended Queue) aise queue hai jisme dono ends - front aur rear - se insertion aur deletion ho sakti hai.

```
 Front/Left       Rear/Right
    |               |
    v               v
    [10]-[20]-[30]-[40]
    |               |
  Add/Remove     Add/Remove
```

### Implementation
Python collections module mein built-in deque hai:

```python
from collections import deque

# Usage
my_deque = deque()
my_deque.append(10)        # Right side add
my_deque.appendleft(5)     # Left side add
my_deque.pop()             # Right side remove
my_deque.popleft()         # Left side remove
```

Custom implementation:

```python
class Deque:
    def __init__(self):
        self.items = []
        
    def add_front(self, item):
        self.items.insert(0, item)  # O(n) with list
        
    def add_rear(self, item):
        self.items.append(item)  # O(1)
        
    def remove_front(self):
        if not self.is_empty():
            return self.items.pop(0)  # O(n) with list
        raise IndexError("Remove from an empty deque")
        
    def remove_rear(self):
        if not self.is_empty():
            return self.items.pop()  # O(1)
        raise IndexError("Remove from an empty deque")
        
    def front(self):
        if not self.is_empty():
            return self.items[0]
        raise IndexError("Front from an empty deque")
        
    def rear(self):
        if not self.is_empty():
            return self.items[-1]
        raise IndexError("Rear from an empty deque")
        
    def is_empty(self):
        return len(self.items) == 0
        
    def size(self):
        return len(self.items)
```

### Behavior/Operations
- **add_front/appendleft**: Front par element add karna (O(1) with deque)
- **add_rear/append**: Rear par element add karna (O(1))
- **remove_front/popleft**: Front se element hatana (O(1) with deque)
- **remove_rear/pop**: Rear se element hatana (O(1))
- **front/peek**: Front element ko dekhna (O(1))
- **rear**: Rear element ko dekhna (O(1))

### Kab aur Kahan Use Karein (When and Where to Use)
- **Work stealing algorithms** mein
- **Sliding window problems** solve karne ke liye
- **Palindrome checking** ke liye
- **Undo-redo** functionality implement karne ke liye
- Jab both FIFO aur LIFO functionality ek sath chahiye
- **Browser history** jaise applications mein

### Special Features
- **Versatility**: Stack aur Queue dono ki functionality combined
- **Efficiency**: Dono ends se O(1) operations (using proper implementation)
- **Flexibility**: Both ends se operations possible

---

<a id="linked-list"></a>
## 5. Linked List

### Kya hai (What is it?)
Linked List ek dynamic data structure hai jisme nodes ka sequence hota hai, har node mein data aur next node ka reference hota hai.

```
  Head        
   |          
   v          
  [D|•]---->[D|•]---->[D|•]---->[D|•]---->NULL
   Node       Node      Node      Node
```

### Implementation
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
            
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node
        
    def prepend(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def delete(self, data):
        if not self.head:
            return
            
        if self.head.data == data:
            self.head = self.head.next
            return
            
        current = self.head
        while current.next and current.next.data != data:
            current = current.next
            
        if current.next:
            current.next = current.next.next
            
    def display(self):
        elements = []
        current = self.head
        while current:
            elements.append(current.data)
            current = current.next
        return elements
        
    def search(self, data):
        current = self.head
        while current:
            if current.data == data:
                return True
            current = current.next
        return False
```

### Behavior/Operations
- **append**: Element ko end mein add karna (O(n))
- **prepend**: Element ko beginning mein add karna (O(1))
- **insert**: Specific position par element add karna (O(n))
- **delete**: Element ko hatana (O(n))
- **search**: Element ko dhundhna (O(n))
- **traverse**: Har element ko visit karna (O(n))

### Kab aur Kahan Use Karein (When and Where to Use)
- Jab frequent **insertions and deletions** middle mein karna ho
- Jab **memory allocation** dynamic ho
- **Symbol tables** implement karne ke liye
- **Polynomial representation** mein
- **Hash tables** ki collision resolution mein
- **Circular buffer** implement karne ke liye
- **Adjacency list** banane ke liye (for graphs)

### Special Features
- **Dynamic memory allocation**: Dynamically grow/shrink ho sakti hai
- **No memory wastage**: Sirf utna hi memory use karti hai jitna zarurat hai
- **Efficient insertion/deletion**: Middle mein insertion/deletion efficient hai (if you have a pointer to the position)
- **No reallocation**: Size change karne ke liye memory reallocation ki zarurat nahi hai

---

<a id="hash-table"></a>
## 6. Hash Table / Hash Map

### Kya hai (What is it?)
Hash Table ek key-value pairs store karne wala data structure hai jisme keys ko hash function se map kiya jata hai specific array indices mein.

```
    Keys    Hash Function    Array Indices
     |            |               |
     v            v               v
    "apple" ----> h() ----> 3 --> ["apple": data]
    "ball"  ----> h() ----> 0 --> ["ball": data]
    "cat"   ----> h() ----> 7 --> ["cat": data]
```

### Implementation
Python mein built-in dictionary hai jo hash table hai:

```python
# Dictionary use
my_dict = {}
my_dict["key1"] = "value1"
my_dict["key2"] = "value2"
```

Custom implementation (simple):

```python
class HashTable:
    def __init__(self, size=10):
        self.size = size
        self.table = [[] for _ in range(size)]  # Using chaining for collision
        
    def _hash_function(self, key):
        # Simple hash function
        if isinstance(key, str):
            return sum(ord(c) for c in key) % self.size
        return key % self.size
        
    def insert(self, key, value):
        index = self._hash_function(key)
        for i, (k, v) in enumerate(self.table[index]):
            if k == key:  # Update existing key
                self.table[index][i] = (key, value)
                return
        # Key doesn't exist, add new key-value pair
        self.table[index].append((key, value))
        
    def get(self, key):
        index = self._hash_function(key)
        for k, v in self.table[index]:
            if k == key:
                return v
        raise KeyError(f"Key '{key}' not found")
        
    def delete(self, key):
        index = self._hash_function(key)
        for i, (k, v) in enumerate(self.table[index]):
            if k == key:
                del self.table[index][i]
                return
        raise KeyError(f"Key '{key}' not found")
        
    def contains(self, key):
        index = self._hash_function(key)
        return any(k == key for k, v in self.table[index])
```

### Behavior/Operations
- **insert/put**: Key-value pair ko add ya update karna (Average O(1), Worst O(n))
- **get/lookup**: Key se value retrieve karna (Average O(1), Worst O(n))
- **delete/remove**: Key-value pair ko hatana (Average O(1), Worst O(n))
- **contains/has**: Check karna ki key exist karti hai ya nahi (Average O(1), Worst O(n))

### Kab aur Kahan Use Karein (When and Where to Use)
- **Database indexing** mein
- **Caches** implement karne ke liye
- **Symbol tables** mein compilers ke liye
- **Unique values** ko track karne ke liye
- **Counting frequencies** ke liye (e.g., word count)
- **Fast lookup** jab key se value retrieve karni ho
- **Dictionary** implement karne ke liye

### Special Features
- **Fast access**: Average case O(1) lookup
- **Flexible keys**: Any hashable object can be a key
- **Space efficient**: For storing key-value pairs
- **Dynamic resizing**: Modern implementations resize automatically

---

<a id="hash-set"></a>
## 7. Hash Set

### Kya hai (What is it?)
Hash Set ek collection hai jisme unique elements store hote hain, hash table ke principles par based hai, but sirf keys store karta hai, values nahi.

```
    Elements    Hash Function    Array Indices
     |               |               |
     v               v               v
    "apple" -------> h() ----> 3 --> ["apple"]
    "ball"  -------> h() ----> 0 --> ["ball"]
    "cat"   -------> h() ----> 7 --> ["cat"]
```

### Implementation
Python mein built-in set hai:

```python
# Set use
my_set = set()
my_set.add("apple")
my_set.add("ball")
```

Custom implementation:

```python
class HashSet:
    def __init__(self, size=10):
        self.size = size
        self.table = [[] for _ in range(size)]
        
    def _hash_function(self, element):
        # Simple hash function
        if isinstance(element, str):
            return sum(ord(c) for c in element) % self.size
        return element % self.size
        
    def add(self, element):
        index = self._hash_function(element)
        if element not in self.table[index]:
            self.table[index].append(element)
        
    def remove(self, element):
        index = self._hash_function(element)
        if element in self.table[index]:
            self.table[index].remove(element)
        else:
            raise KeyError(f"Element '{element}' not found")
        
    def contains(self, element):
        index = self._hash_function(element)
        return element in self.table[index]
        
    def size(self):
        return sum(len(bucket) for bucket in self.table)
        
    def elements(self):
        result = []
        for bucket in self.table:
            result.extend(bucket)
        return result
```

### Behavior/Operations
- **add**: Element ko add karna (Average O(1), Worst O(n))
- **remove**: Element ko hatana (Average O(1), Worst O(n))
- **contains**: Check karna ki element exist karta hai ya nahi (Average O(1), Worst O(n))
- **size**: Elements ki count
- **union**: Do sets ka union nikalna
- **intersection**: Do sets ka intersection nikalna
- **difference**: Do sets ka difference nikalna

### Kab aur Kahan Use Karein (When and Where to Use)
- **Duplicate removal** ke liye
- **Membership checking** ke liye (quickly check if element exists)
- **Mathematical set operations** ke liye (union, intersection, etc.)
- **Distinct counting** ke liye
- **Data de-duplication** ke liye

### Special Features
- **Fast lookups**: Average case O(1) for contains operation
- **No duplicates**: Automatically handles duplicates
- **Set operations**: Mathematical set operations support
- **Space efficiency**: Only stores each unique element once

---

<a id="tree"></a>
## 8. Tree

### Kya hai (What is it?)
Tree ek hierarchical data structure hai jisme nodes ko parent-child relationship mein organize kiya jata hai. Ek root node hota hai aur uske child nodes, hierarchical manner mein arrange kiye jate hain.

```
          Root
           |
      +----+----+
      |         |
    Child1    Child2
      |         |
   +--+--+     +--+
   |     |     |  |
 Leaf1 Leaf2 Leaf3 Leaf4
```

### Implementation
Basic tree implementation:

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.children = []
        
    def add_child(self, child):
        self.children.append(child)
        
class Tree:
    def __init__(self, root_data):
        self.root = TreeNode(root_data)
        
    def print_tree(self, node=None, level=0):
        if node is None:
            node = self.root
            
        print("  " * level + "|--", node.data)
        for child in node.children:
            self.print_tree(child, level + 1)
    
    def search(self, value, node=None):
        if node is None:
            node = self.root
            
        if node.data == value:
            return node
            
        for child in node.children:
            result = self.search(value, child)
            if result:
                return result
                
        return None
```

### Behavior/Operations
- **insert/add_child**: Node add karna (O(1) if parent reference is available)
- **search/find**: Value ko dhundhna (O(n) in worst case)
- **delete**: Node ko hatana (O(n) to find + O(1) to delete)
- **traversal**: Tree ko traverse karna
  - Pre-order: Root -> Left -> Right
  - In-order: Left -> Root -> Right
  - Post-order: Left -> Right -> Root
  - Level-order: Level by level

### Kab aur Kahan Use Karein (When and Where to Use)
- **File systems** represent karne ke liye
- **Organization charts** banane ke liye
- **XML/HTML parsing** ke liye DOM tree
- **Decision trees** implement karne ke liye
- **Family trees** represent karne ke liye
- **Network routing algorithms** mein
- **AI game trees** (e.g., chess, tic-tac-toe)

### Special Features
- **Hierarchical representation**: Natural hierarchy represent kar sakta hai
- **Efficient operations**: Many operations are efficient with proper implementation
- **Easy traversal**: Different traversal methods support karta hai
- **Versatility**: Many specialized types (BST, AVL, Red-Black, etc.)

---

<a id="binary-search-tree"></a>
## 9. Binary Search Tree (BST)

### Kya hai (What is it?)
Binary Search Tree ek special tree hai jisme har node ke maximum 2 children ho sakte hain, aur left child ki value parent se choti hoti hai aur right child ki value parent se badi hoti hai.

```
          50
         /  \
       30    70
      / \    / \
    20  40  60  80
```

### Implementation
```python
class BSTNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BinarySearchTree:
    def __init__(self):
        self.root = None
        
    def insert(self, data):
        if not self.root:
            self.root = BSTNode(data)
            return
            
        self._insert_recursive(self.root, data)
        
    def _insert_recursive(self, node, data):
        if data < node.data:
            if node.left is None:
                node.left = BSTNode(data)
            else:
                self._insert_recursive(node.left, data)
        else:
            if node.right is None:
                node.right = BSTNode(data)
            else:
                self._insert_recursive(node.right, data)
    
    def search(self, data):
        return self._search_recursive(self.root, data)
        
    def _search_recursive(self, node, data):
        if node is None:
            return False
            
        if node.data == data:
            return True
            
        if data < node.data:
            return self._search_recursive(node.left, data)
        else:
            return self._search_recursive(node.right, data)
    
    def delete(self, data):
        self.root = self._delete_recursive(self.root, data)
        
    def _delete_recursive(self, node, data):
        if node is None:
            return None
            
        if data < node.data:
            node.left = self._delete_recursive(node.left, data)
        elif data > node.data:
            node.right = self._delete_recursive(node.right, data)
        else:
            # Node with only one child or no child
            if node.left is None:
                return node.right
            elif node.right is None:
                return node.left
                
            # Node with two children
            # Get the inorder successor (smallest in the right subtree)
            temp = self._find_min(node.right)
            node.data = temp.data
            node.right = self._delete_recursive(node.right, temp.data)
            
        return node
        
    def _find_min(self, node):
        current = node
        while current.left:
            current = current.left
        return current
        
    def inorder_traversal(self):
        result = []
        self._inorder_recursive(self.root, result)
        return result
        
    def _inorder_recursive(self, node, result):
        if node:
            self._inorder_recursive(node.left, result)
            result.append(node.data)
            self._inorder_recursive(node.right, result)
```

### Behavior/Operations
- **insert**: New node add karna (Average O(log n), Worst O(n))
- **search**: Value ko dhundhna (Average O(log n), Worst O(n))
- **delete**: Node ko hatana (Average O(log n), Worst O(n))
- **traversal**:
  - Inorder (Left -> Root -> Right): Sorted order mein elements deta hai
  - Preorder (Root -> Left -> Right)
  - Postorder (Left -> Right -> Root)

### Kab aur Kahan Use Karein (When and Where to Use)
- **Sorted data** maintain karne ke liye
- **Dictionary implementation** ke liye
- **Priority queues** implement karne ke liye
- **Symbol tables** mein
- **Database indexing** mein
- Jab frequent insertions, deletions, and searches karne ho
- **Range queries** implement karne ke liye

### Special Features
- **Ordered structure**: Elements always remain in sorted order
- **Efficient search**: Average O(log n) search time
- **In-order traversal**: Gives elements in sorted order
- **Range queries**: Efficient for range queries
- **Balanced variants**: Self-balancing BSTs like AVL and Red-Black trees provide guaranteed O(log n) operations

---

<a id="heap"></a>
## 10. Heap (Min-Heap / Max-Heap)

### Kya hai (What is it?)
Heap ek complete binary tree hai jo heap property follow karta hai. Min-heap mein parent node ki value apne child nodes se choti hoti hai (root minimum value hota hai). Max-heap mein parent node ki value apne child nodes se badi hoti hai (root maximum value hota hai).

```
  Max-Heap        Min-Heap
     100             10
    /   \           /  \
   80    90        30   20
  / \   /         / \   /
 70 40  85       40 35  25
```

### Implementation
Python mein heapq module provide karta hai min-heap functionality:

```python
import heapq

# Min-heap
min_heap = []
heapq.heappush(min_heap, 10)
heapq.heappush(min_heap, 5)
min_value = heapq.heappop(min_heap)  # Returns 5

# Convert list to heap
my_list = [5, 7, 9, 1, 3]
heapq.heapify(my_list)  # Now my_list is a min-heap

# For max-heap, use negative values
max_heap = []
heapq.heappush(max_heap, -10)
heapq.heappush(max_heap, -5)
max_value = -heapq.heappop(max_heap)  # Returns 10
```

Custom implementation:

```python
class MinHeap:
    def __init__(self):
        self.heap = []
        
    def parent(self, i):
        return (i - 1) // 2
        
    def left_child(self, i):
        return 2 * i + 1
        
    def right_child(self, i):
        return 2 * i + 2
        
    def get_min(self):
        if len(self.heap) > 0:
            return self.heap[0]
        return None
        
    def insert(self, value):
        self.heap.append(value)
        self._sift_up(len(self.heap) - 1)
        
    def extract_min(self):
        if not self.heap:
            return None
            
        min_value = self.heap[0]
        last_element = self.heap.pop()
        
        if self.heap:  # If heap is not empty after popping
            self.heap[0] = last_element
            self._sift_down(0)
            
        return min_value
        
    def _sift_up(self, i):
        parent_idx = self.parent(i)
        if i > 0 and self.heap[parent_idx] > self.heap[i]:
            self.heap[i], self.heap[parent_idx] = self.heap[parent_idx], self.heap[i]
            self._sift_up(parent_idx)
    
    def _sift_down(self, i):
        smallest = i
        left = self.left_child(i)
        right = self.right_child(i)
        
        if left < len(self.heap) and self.heap[left] < self.heap[smallest]:
            smallest = left
            
        if right < len(self.heap) and self.heap[right] < self.heap[smallest]:
            smallest = right
            
        if smallest != i:
            self.heap[i], self.heap[smallest] = self.heap[smallest], self.heap[i]
            self._sift_down(smallest)
```

### Behavior/Operations
- **insert**: Element ko add karna (O(log n))
- **get_min/get_max**: Minimum/Maximum element ko access karna (O(1))
- **extract_min/extract_max**: Minimum/Maximum element ko remove and return karna (O(log n))
- **heapify**: Array ko heap mein convert karna (O(n))

### Kab aur Kahan Use Karein (When and Where to Use)
- **Priority queues** implement karne ke liye
- **Heap sort algorithm** mein
- **Graph algorithms** mein (Dijkstra, Prim)
- **K largest/smallest elements** find karne ke liye
- **Median maintenance** ke liye
- **Event scheduling** mein
- **Task scheduling** algorithms mein

### Special Features
- **Fast access to min/max**: O(1) time mein minimum/maximum value access kar sakte hain
- **Efficient insertion**: O(log n) insertion time
- **Complete binary tree**: Space efficient representation using array
- **Partially ordered**: Not fully sorted but maintains heap property
- **Used in system processes**: OS process scheduling mein use hota hai

---

<a id="graph"></a>
## 11. Graph

### Kya hai (What is it?)
Graph ek non-linear data structure hai jisme vertices (nodes) aur edges (connections) hote hain. Edges directed (one-way) ya undirected (two-way) ho sakte hain.

```
    A --- B
   / \     \
  C   D --- E
   \ /
    F
```

### Implementation
Using adjacency list:

```python
class Graph:
    def __init__(self, directed=False):
        self.graph = {}
        self.directed = directed
        
    def add_vertex(self, vertex):
        if vertex not in self.graph:
            self.graph[vertex] = []
            
    def add_edge(self, vertex1, vertex2, weight=None):
        if vertex1 not in self.graph:
            self.add_vertex(vertex1)
        if vertex2 not in self.graph:
            self.add_vertex(vertex2)
            
        # Add edge information as a tuple (vertex, weight)
        self.graph[vertex1].append((vertex2, weight))
        
        # If undirected, add the reverse edge too
        if not self.directed:
            self.graph[vertex2].append((vertex1, weight))
            
    def get_neighbors(self, vertex):
        return [v for v, w in self.graph.get(vertex, [])]
            
    def bfs(self, start_vertex):
        """Breadth-First Search traversal"""
        if start_vertex not in self.graph:
            return []
            
        visited = set([start_vertex])
        queue = [start_vertex]
        result = []
        
        while queue:
            current = queue.pop(0)
            result.append(current)
            
            for neighbor, _ in self.graph[current]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)
                    
        return result
        
    def dfs(self, start_vertex):
        """Depth-First Search traversal"""
        if start_vertex not in self.graph:
            return []
            
        visited = set()
        result = []
        
        def dfs_recursive(vertex):
            visited.add(vertex)
            result.append(vertex)
            
            for neighbor, _ in self.graph[vertex]:
                if neighbor not in visited:
                    dfs_recursive(neighbor)
                    
        dfs_recursive(start_vertex)
        return result
        
    def has_path(self, start_vertex, end_vertex):
        """Check if there's a path between two vertices"""
        if start_vertex not in self.graph or end_vertex not in self.graph:
            return False
            
        visited = set()
        
        def dfs_recursive(vertex):
            if vertex == end_vertex:
                return True
                
            visited.add(vertex)
            
            for neighbor, _ in self.graph[vertex]:
                if neighbor not in visited:
                    if dfs_recursive(neighbor):
                        return True
                        
            return False
            
        return dfs_recursive(start_vertex)
```

### Behavior/Operations
- **add_vertex**: Vertex add karna (O(1))
- **add_edge**: Edge add karna (O(1))
- **remove_vertex**: Vertex hatana (O(|V| + |E|))
- **remove_edge**: Edge hatana (O(|E|))
- **has_edge**: Check karna ki do vertices ke beech edge hai ya nahi (O(|E|))
- **get_neighbors**: Vertex ke neighbors return karna (O(1))
- **traversal**:
  - BFS (Breadth-First Search)
  - DFS (Depth-First Search)

### Kab aur Kahan Use Karein (When and Where to Use)
- **Social networks** represent karne ke liye
- **Web pages** aur links represent karne ke liye
- **Maps** aur routing algorithms mein
- **Network topology** represent karne ke liye
- **Recommendation systems** mein
- **Dependency resolution** mein
- **Circuit design** mein

### Special Features
- **Versatility**: Many real-world problems can be modeled as graphs
- **Flexible relationships**: Can represent any kind of relationships
- **Powerful algorithms**: Many algorithms exist for pathfinding, flow, etc.
- **Two representations**: Adjacency matrix (space O(V²)) and adjacency list (space O(V+E))

---

<a id="set"></a>
## 12. Set

### Kya hai (What is it?)
Set ek unordered collection hai jisme unique elements store hote hain, duplicates allowed nahi hote.

### Implementation
Python mein built-in set hai:

```python
# Creating a set
my_set = set()
my_set = {1, 2, 3, 4, 5}

# Operations
my_set.add(6)      # Add element
my_set.remove(3)   # Remove element (raises error if not present)
my_set.discard(10) # Remove if present (no error if not present)
```

Custom implementation (using hash table):

```python
class Set:
    def __init__(self):
        self.elements = {}  # Using dict for O(1) lookups
        
    def add(self, element):
        self.elements[element] = True
        
    def remove(self, element):
        if element in self.elements:
            del self.elements[element]
        else:
            raise KeyError(f"Element '{element}' not found")
    
    def discard(self, element):
        if element in self.elements:
            del self.elements[element]
            
    def contains(self, element):
        return element in self.elements
        
    def size(self):
        return len(self.elements)
        
    def union(self, other_set):
        result = Set()
        for element in self.elements:
            result.add(element)
        for element in other_set.elements:
            result.add(element)
        return result
        
    def intersection(self, other_set):
        result = Set()
        for element in self.elements:
            if element in other_set.elements:
                result.add(element)
        return result
        
    def difference(self, other_set):
        result = Set()
        for element in self.elements:
            if element not in other_set.elements:
                result.add(element)
        return result
```

### Behavior/Operations
- **add**: Element ko add karna (O(1) average)
- **remove/discard**: Element ko hatana (O(1) average)
- **contains**: Check karna ki element set mein hai ya nahi (O(1) average)
- **union**: Do sets ka union nikalna
- **intersection**: Do sets ka intersection nikalna
- **difference**: Do sets ka difference nikalna
- **symmetric_difference**: Do sets ka symmetric difference nikalna

### Kab aur Kahan Use Karein (When and Where to Use)
- **Duplicate elimination** ke liye
- **Membership testing** ke liye
- **Mathematical set operations** perform karne ke liye
- **Distinct counting** ke liye
- **Finding unique items** in a collection
- **Representing groups** with no specific order

### Special Features
- **No duplicates**: Automatically handles duplicates
- **Fast operations**: O(1) average time complexity for most operations
- **Mathematical model**: Direct implementation of mathematical set theory
- **Hashable elements**: Elements must be hashable (immutable)

---

<a id="trie"></a>
## 13. Trie (Prefix Tree)

### Kya hai (What is it?)
Trie (prefix tree) ek specialized tree hai jo string searching ke liye optimize hai, particularly prefix searching. Har node characters store karta hai aur root se leaf tak path ek complete string form karta hai.

```
              root
             /  |  \
            a   b   c
           /    |    \
          p     o     a
         /      |      \
        p       y       t
       /
      l
      |
      e
```

### Implementation
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
        
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True
        
    def search(self, word):
        """Returns True if the word is in the trie"""
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word
        
    def starts_with_prefix(self, prefix):
        """Returns True if there is any word in the trie that starts with the given prefix"""
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
        
    def get_words_with_prefix(self, prefix):
        """Returns all words starting with the given prefix"""
        result = []
        node = self.root
        
        # Navigate to the end of prefix
        for char in prefix:
            if char not in node.children:
                return result
            node = node.children[char]
            
        # Collect all words starting from this node
        def dfs(current_node, current_prefix):
            if current_node.is_end_of_word:
                result.append(current_prefix)
                
            for char, child_node in current_node.children.items():
                dfs(child_node, current_prefix + char)
                
        dfs(node, prefix)
        return result
```

### Behavior/Operations
- **insert**: Word ko trie mein add karna (O(m) where m is word length)
- **search**: Word ko dhundhna (O(m))
- **starts_with_prefix**: Check karna ki koi word given prefix se start hota hai ya nahi (O(m))
- **delete**: Word ko hatana (O(m))
- **get_words_with_prefix**: Given prefix se start hone wale saare words return karna

### Kab aur Kahan Use Karein (When and Where to Use)
- **Autocomplete functionality** implement karne ke liye
- **Spell checkers** banane ke liye
- **IP routing** (longest prefix matching)
- **Predictive text** mein
- **Search engines** ke search suggestions mein
- **Dictionary implementation** ke liye
- **Word games** (e.g., Boggle, Scrabble) mein word searching

### Special Features
- **Space-efficient**: Common prefixes share memory
- **Fast prefix operations**: O(m) time complexity for operations
- **Ordered traversal**: Lexicographically traverse karna easy hai
- **Dynamic spell checking**: As-you-type spell checking enable karta hai

---

<a id="priority-queue"></a>
## 14. Priority Queue

### Kya hai (What is it?)
Priority Queue ek abstract data type hai jisme elements ko unki priority ke according retrieve kiya jata hai, na ki unke insertion order ke according.

```
   Priority: High            Low
             |               |
             v               v
     [Item1, Item2, Item3, Item4]
```

### Implementation
Using Python's heapq (min-heap implementation):

```python
import heapq

class PriorityQueue:
    def __init__(self):
        self.elements = []
        
    def enqueue(self, item, priority):
        """Add item with priority (lower value = higher priority)"""
        heapq.heappush(self.elements, (priority, item))
        
    def dequeue(self):
        """Remove and return highest priority item"""
        if self.is_empty():
            raise IndexError("Priority queue is empty")
        priority, item = heapq.heappop(self.elements)
        return item
        
    def peek(self):
        """View highest priority item without removing"""
        if self.is_empty():
            raise IndexError("Priority queue is empty")
        priority, item = self.elements[0]
        return item
        
    def is_empty(self):
        return len(self.elements) == 0
        
    def size(self):
        return len(self.elements)
```

For max priority queue (higher value = higher priority):

```python
def enqueue_max(self, item, priority):
    """Add item with priority (higher value = higher priority)"""
    heapq.heappush(self.elements, (-priority, item))
```

### Behavior/Operations
- **enqueue/push**: Element ko priority ke sath add karna (O(log n))
- **dequeue/pop**: Highest priority element ko remove aur return karna (O(log n))
- **peek**: Highest priority element ko dekhna bina hataye (O(1))
- **is_empty**: Check karna ki queue empty hai ya nahi (O(1))
- **size**: Elements ki count (O(1))

### Kab aur Kahan Use Karein (When and Where to Use)
- **Task scheduling** mein (high priority tasks first)
- **CPU scheduling** mein operating systems mein
- **Dijkstra's algorithm** mein (shortest path)
- **Huffman coding** mein (compression)
- **Best-first search** algorithms mein
- **Event-driven simulation** mein
- **Network traffic management** mein (QoS - Quality of Service)

### Special Features
- **Ordered by priority**: Elements priority ke hisaab se retrieve hote hain
- **Dynamic ordering**: New elements are inserted in correct priority position
- **Heap implementation**: Typically implemented using heaps for O(log n) operations
- **Priority update**: Some implementations support changing priorities (decrease-key operation)

---

<a id="matrix"></a>
## 15. Matrix (2D Array as ADT)

### Kya hai (What is it?)
Matrix (2D Array) ek tabular data structure hai jisme elements rows aur columns mein organize kiye jate hain.

```
    [a b c]
    [d e f]
    [g h i]
```

### Implementation
Basic using nested lists in Python:

```python
class Matrix:
    def __init__(self, rows, cols, default_value=0):
        self.rows = rows
        self.cols = cols
        self.data = [[default_value for _ in range(cols)] for _ in range(rows)]
        
    def get(self, row, col):
        if 0 <= row < self.rows and 0 <= col < self.cols:
            return self.data[row][col]
        raise IndexError("Matrix indices out of range")
        
    def set(self, row, col, value):
        if 0 <= row < self.rows and 0 <= col < self.cols:
            self.data[row][col] = value
        else:
            raise IndexError("Matrix indices out of range")
    
    def add(self, other_matrix):
        if self.rows != other_matrix.rows or self.cols != other_matrix.cols:
            raise ValueError("Matrix dimensions must match for addition")
            
        result = Matrix(self.rows, self.cols)
        for i in range(self.rows):
            for j in range(self.cols):
                result.data[i][j] = self.data[i][j] + other_matrix.data[i][j]
                
        return result
        
    def multiply(self, other_matrix):
        if self.cols != other_matrix.rows:
            raise ValueError("Number of columns in first matrix must match number of rows in second matrix")
            
        result = Matrix(self.rows, other_matrix.cols)
        for i in range(self.rows):
            for j in range(other_matrix.cols):
                for k in range(self.cols):
                    result.data[i][j] += self.data[i][k] * other_matrix.data[k][j]
                    
        return result
        
    def transpose(self):
        result = Matrix(self.cols, self.rows)
        for i in range(self.rows):
            for j in range(self.cols):
                result.data[j][i] = self.data[i][j]
                
        return result
        
    def __str__(self):
        return '\n'.join([' '.join([str(cell) for cell in row]) for row in self.data])
```

Using NumPy (recommended for real-world use):

```python
import numpy as np

# Create matrix
matrix = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# Operations
matrix + matrix  # Addition
matrix.dot(matrix)  # Matrix multiplication
matrix.T  # Transpose
np.linalg.inv(matrix)  # Inverse (if square and non-singular)
```

### Behavior/Operations
- **get**: Element ko access karna (O(1))
- **set**: Element ko update karna (O(1))
- **add**: Do matrices ko add karna (O(rows*cols))
- **multiply**: Do matrices ko multiply karna (O(n³) for n×n matrices with naive algorithm)
- **transpose**: Matrix ko transpose karna (O(rows*cols))
- **determinant**: Matrix ka determinant nikalna (O(n³) for naive implementation)
- **inverse**: Matrix ka inverse nikalna (if possible)

### Kab aur Kahan Use Karein (When and Where to Use)
- **Linear algebra** calculations mein
- **Graph representation** (adjacency matrix) ke liye
- **Image processing** mein (images as 2D matrices)
- **Game boards** represent karne ke liye (chess, tic-tac-toe)
- **Dynamic programming** problems mein
- **Machine learning** algorithms mein
- **3D graphics** (transformation matrices)

### Special Features
- **Direct access**: O(1) time to access any element
- **Mathematical operations**: Matrix algebra operations support
- **Spatial relationships**: Captures relationships between rows and columns
- **Regular structure**: Fixed dimensions with contiguous memory representation

---

<a id="circular-queue"></a>
## 16. Circular Queue

### Kya hai (What is it?)
Circular Queue ek linear data structure hai jisme last position ke baad first position aati hai, forming a circle. Isse memory efficient use hota hai.

```
       front      rear
         |         |
         v         v
       +---+---+---+---+---+---+
       | 1 | 2 | 3 |   |   |   |
       +---+---+---+---+---+---+
         ^                 ^
         |                 |
        Elements        Empty spaces
```

### Implementation
```python
class CircularQueue:
    def __init__(self, capacity):
        self.capacity = capacity
        self.queue = [None] * capacity
        self.front = -1
        self.rear = -1
        self.size = 0
        
    def is_empty(self):
        return self.size == 0
        
    def is_full(self):
        return self.size == self.capacity
        
    def enqueue(self, item):
        if self.is_full():
            raise Exception("Queue is full")
            
        if self.is_empty():
            self.front = 0
            
        self.rear = (self.rear + 1) % self.capacity
        self.queue[self.rear] = item
        self.size += 1
        
    def dequeue(self):
        if self.is_empty():
            raise Exception("Queue is empty")
            
        item = self.queue[self.front]
        self.queue[self.front] = None
        
        if self.front == self.rear:  # Last element
            self.front = -1
            self.rear = -1
        else:
            self.front = (self.front + 1) % self.capacity
            
        self.size -= 1
        return item
        
    def peek(self):
        if self.is_empty():
            raise Exception("Queue is empty")
        return self.queue[self.front]
        
    def __len__(self):
        return self.size
        
    def __str__(self):
        if self.is_empty():
            return "Queue: []"
            
        result = "Queue: ["
        i = self.front
        
        for _ in range(self.size):
            result += str(self.queue[i]) + ", "
            i = (i + 1) % self.capacity
            
        return result[:-2] + "]"
```

### Behavior/Operations
- **enqueue**: Element ko add karna (O(1))
- **dequeue**: Front element ko hatana aur return karna (O(1))
- **peek/front**: Front element ko dekhna bina hataye (O(1))
- **is_empty**: Check karna ki queue empty hai ya nahi (O(1))
- **is_full**: Check karna ki queue full hai ya nahi (O(1))

### Kab aur Kahan Use Karein (When and Where to Use)
- **Clock buffers** implement karne ke liye
- **Traffic light management** systems mein
- **Streaming data** process karne ke liye (finite buffer)
- **CPU scheduling** (Round-robin algorithm) mein
- **Memory management** mein 
- **Circular lists** implement karne ke liye with fixed size
- **Loop execution** in embedded systems

### Special Features
- **Space efficiency**: Reuses empty spaces
- **Fixed capacity**: Bounded memory usage
- **Wrap-around property**: Elements can wrap around
- **Fast operations**: All operations are O(1)
- **No shifting**: Unlike arrays, no need to shift elements when removing

---

<a id="circular-linked-list"></a>
## 17. Circular Linked List

### Kya hai (What is it?)
Circular Linked List ek modified linked list hai jisme last node ka next pointer first node ko point karta hai, forming a circle.

```
    +---+    +---+    +---+    +---+
    | 1 |----| 2 |----|	3 |----| 4 |
    +---+    +---+    +---+    +---+
      ^                          |
      |                          |
      +--------------------------+
```

### Implementation
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class CircularLinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        new_node = Node(data)
        
        if not self.head:
            self.head = new_node
            new_node.next = self.head  # Point to itself
            return
            
        current = self.head
        while current.next != self.head:
            current = current.next
            
        current.next = new_node
        new_node.next = self.head
        
    def prepend(self, data):
        new_node = Node(data)
        
        if not self.head:
            self.head = new_node
            new_node.next = self.head  # Point to itself
            return
            
        current = self.head
        while current.next != self.head:
            current = current.next
            
        new_node.next = self.head
        current.next = new_node
        self.head = new_node
        
    def delete(self, key):
        if not self.head:
            return
            
        # Case 1: Head node to be deleted
        if self.head.data == key:
            # If it's the only node
            if self.head.next == self.head:
                self.head = None
                return
                
            # Find the last node
            current = self.head
            while current.next != self.head:
                current = current.next
                
            # Update references
            current.next = self.head.next
            self.head = self.head.next
            return
            
        # Case 2: Non-head node to be deleted
        prev = None
        current = self.head
        
        while current.next != self.head:
            if current.data == key:
                prev.next = current.next
                return
            prev = current
            current = current.next
            
        # Check the last node
        if current.data == key:
            prev.next = self.head
            
    def display(self):
        if not self.head:
            return "Empty list"
            
        elements = []
        current = self.head
        
        while True:
            elements.append(current.data)
            current = current.next
            if current == self.head:
                break
                
        return elements
        
    def size(self):
        if not self.head:
            return 0
            
        count = 0
        current = self.head
        
        while True:
            count += 1
            current = current.next
            if current == self.head:
                break
                
        return count
```

### Behavior/Operations
- **append**: Element ko end mein add karna (O(n))
- **prepend**: Element ko beginning mein add karna (O(n))
- **delete**: Element ko hatana (O(n))
- **display**: List ke elements ko show karna (O(n))
- **search**: Element ko dhundhna (O(n))

### Kab aur Kahan Use Karein (When and Where to Use)
- **Round-robin scheduling** (CPU scheduling) mein
- **Circular buffers** implement karne ke liye
- **Loop execution** jahan repeatedly list traverse karni ho
- **Game turns** manage karne ke liye (players in a circle)
- **Circular playlist** implement karne ke liye
- **Josephus Problem** solve karne ke liye
- **Multiplayer board games** mein player turns handling

### Special Features
- **No end**: No beginning or end; continuous loop
- **Simplifies circular operations**: Natural for circular processes
- **Space efficient**: No need to store tail reference separately
- **Continuous traversal**: Can traverse indefinitely
- **Elegant for circular problems**: More natural than standard linked list for circular problems

---

<a id="multiset"></a>
## 18. Multiset / Bag

### Kya hai (What is it?)
Multiset (ya Bag) ek collection hai jisme duplicate elements allowed hote hain. Yeh basically ek set hai with frequency count for each element.

### Implementation
Python mein Counter ya defaultdict use karke implement kiya ja sakta hai:

```python
from collections import Counter

# Using Counter
my_multiset = Counter()
my_multiset.update(['a', 'b', 'a', 'c', 'a', 'b'])
# my_multiset now contains: {'a': 3, 'b': 2, 'c': 1}
```

Custom implementation:

```python
class Multiset:
    def __init__(self):
        self.elements = {}  # element -> frequency
        
    def add(self, element):
        """Add one occurrence of element"""
        if element in self.elements:
            self.elements[element] += 1
        else:
            self.elements[element] = 1
            
    def remove(self, element):
        """Remove one occurrence of element"""
        if element in self.elements:
            self.elements[element] -= 1
            if self.elements[element] == 0:
                del self.elements[element]
        else:
            raise KeyError(f"Element '{element}' not found")
            
    def count(self, element):
        """Return the count of element"""
        return self.elements.get(element, 0)
        
    def contains(self, element):
        """Check if element exists at least once"""
        return element in self.elements
        
    def total_elements(self):
        """Return total number of elements (including duplicates)"""
        return sum(self.elements.values())
        
    def unique_elements(self):
        """Return number of unique elements"""
        return len(self.elements)
        
    def union(self, other_multiset):
        """Return new multiset with max frequency of each element"""
        result = Multiset()
        all_elements = set(self.elements.keys()) | set(other_multiset.elements.keys())
        
        for element in all_elements:
            count = max(self.count(element), other_multiset.count(element))
            for _ in range(count):
                result.add(element)
                
        return result
        
    def intersection(self, other_multiset):
        """Return new multiset with min frequency of each element"""
        result = Multiset()
        common_elements = set(self.elements.keys()) & set(other_multiset.elements.keys())
        
        for element in common_elements:
            count = min(self.count(element), other_multiset.count(element))
            for _ in range(count):
                result.add(element)
                
        return result
```

### Behavior/Operations
- **add**: Element ko add karna (O(1))
- **remove**: Element ka ek occurrence hatana (O(1))
- **count**: Element ki frequency return karna (O(1))
- **contains**: Check karna ki element exist karta hai ya nahi (O(1))
- **union**: Do multisets ka union (max frequency wala)
- **intersection**: Do multisets ka intersection (min frequency wala)
- **
