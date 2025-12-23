# Linked List Implementation

A complete **singly linked list** implementation in JavaScript with ES6 modules, demonstrating fundamental linear data structure operations, pointer manipulation, and memory-efficient sequential storage. This project showcases understanding of linked data structures essential for interviews and backend development.

## 🎯 Project Overview

This repository implements a production-ready LinkedList class with 14 core operations covering insertion, deletion, searching, and traversal. The implementation uses modern JavaScript (ES6 modules) and includes methods for efficient list manipulation. Linked lists are fundamental to understanding memory management, pointers, and sequential data access patterns.

## 📚 Data Structure

### Node Class
```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.nextNode = null;  // Pointer to next node
  }
}
```

Each node contains:
- **value**: Data stored in the node
- **nextNode**: Reference/pointer to the next node (or null if last)

### Linked List Structure
```
[Value] → [Value] → [Value] → null
Head              Middle           Tail
```

## 🔧 Complete API (14 Methods)

### Insertion Operations

#### `prepend(value)`
Inserts a new node at the **beginning** of the list.
- **Time Complexity**: O(1) - constant time
- **Process**: Create new node, make it point to current head, update head reference
- **Use Case**: When insertion order needs to be reversed

```javascript
const list = new LinkedList();
list.prepend(3);
list.prepend(2);
list.prepend(1);
// List: 1 → 2 → 3 → null
```

**How it works**:
```
Before: 2 → 3 → null
After:  1 → 2 → 3 → null
        ^newNode points to old head
```

#### `append(value)`
Inserts a new node at the **end** of the list.
- **Time Complexity**: O(n) - must traverse to find tail
- **Process**: Traverse to last node, set its nextNode to new node
- **Use Case**: Building lists in insertion order

```javascript
list.append(1);
list.append(2);
list.append(3);
// List: 1 → 2 → 3 → null
```

**How it works**:
```
Before: 1 →  2 → null
Append 3:
Before: 1 → 2 → (null)
        ^→ Set this nextNode
After:  1 → 2 →  3 → null
```

#### `insertAt(value, index)`
Inserts a new node at a **specific position**.
- **Time Complexity**: O(n) - must traverse to position
- **Parameters**: value = data, index = position (0-based)
- **Behavior**: Updates pointers to maintain list integrity

```javascript
list.append(1);
list.append(2);
list.append(4);
list.insertAt(3, 2);  // Insert 3 at position 2
// List: 1 → 2 → 3 → 4 → null
```

**How it works**:
```
Before: 1 → 2 → 4 → null
Insert 3 at index 2:
Before: 1 → 2 → 4 → null
             ^
             Find node at index 1
After:  1 → 2 → 3 → 4 → null
             newNode.nextNode = 4
             prevNode.nextNode = 3
```

### Deletion Operations

#### `pop()`
Removes the **last node** from the list.
- **Time Complexity**: O(n) - must find second-to-last node
- **No Return Value**: Modifies list in place
- **Use Case**: LIFO (Last In First Out) operations

```javascript
list.append(1);
list.append(2);
list.append(3);
list.pop();  // Removes 3
// List: 1 → 2 → null
```

**How it works**:
```
Before: 1 → 2 → 3 → null
Find node before last (2), set its nextNode to null
After:  1 → 2 → null
```

#### `removeAt(index)`
Removes a node at a **specific position**.
- **Time Complexity**: O(n)
- **Returns**: Error message if index out of bounds
- **Behavior**: Links previous node to next node, skipping target

```javascript
list.append(1);
list.append(2);
list.append(3);
list.removeAt(1);  // Remove node at index 1 (value 2)
// List: 1 → 3 → null
```

**How it works**:
```
Before: 1 → 2 → 3 → null
Remove index 1:
            prev   current
Before: 1 → 2 → 3 → null
After:  1 → 3 → null
        ^
Set prev.nextNode = current.nextNode
```

### Search & Access Operations

#### `at(index)`
Returns the **node at a specific index**.
- **Time Complexity**: O(n) - linear traversal to position
- **Returns**: Node object if found, error message if index out of bounds
- **Use Case**: Random access to list elements

```javascript
list.append(10);
list.append(20);
list.append(30);
const node = list.at(1);  // Returns node with value 20
console.log(node.value);   // 20
```

#### `find(value)`
Searches for a node by **value** and returns its **index**.
- **Time Complexity**: O(n) - linear search
- **Returns**: Index if found, null if not found
- **Use Case**: Finding position of element

```javascript
list.append('apple');
list.append('banana');
list.append('cherry');
const index = list.find('banana');  // Returns: 1
const notFound = list.find('grape'); // Returns: null
```

#### `contains(value)`
Checks if a **value exists** in the list.
- **Time Complexity**: O(n)
- **Returns**: Boolean
- **Use Case**: Membership testing without finding index

```javascript
list.append(5);
list.append(10);
list.contains(5);   // Returns: true
list.contains(15);  // Returns: false
```

#### `head()`
Returns the **first node** in the list.
- **Time Complexity**: O(1) - direct reference
- **Returns**: Head node object
- **Use Case**: Accessing list beginning

```javascript
list.append(1);
list.append(2);
const headNode = list.head();  // Node with value 1
```

#### `tail()`
Returns the **last node** in the list.
- **Time Complexity**: O(n) - must traverse entire list
- **Returns**: Tail node object
- **Use Case**: Accessing list end

```javascript
const lastNode = list.tail();  // Last node in list
console.log(lastNode.value);   // Value of last node
```

### List Information

#### `size()`
Returns the **total number of nodes** in the list.
- **Time Complexity**: O(n) - must count all nodes
- **Returns**: Integer count
- **Use Case**: Knowing list length

```javascript
list.append(1);
list.append(2);
list.append(3);
console.log(list.size());  // 3
```

#### `toString()`
Returns a **string representation** of the list.
- **Time Complexity**: O(n)
- **Returns**: String in format: `(val1) -> (val2) -> (val3) -> null`
- **Use Case**: Debugging and visualization

```javascript
list.append('a');
list.append('b');
list.append('c');
console.log(list.toString());
// Output: (a) -> (b) -> (c) -> null
```

## 📊 Example Usage

Complete workflow demonstrating all operations:

```javascript
import LinkedList from './linkedList.js';

const list = new LinkedList();

// 1. Build list
list.append(10);
list.append(20);
list.append(30);
console.log(list.toString());     // (10) -> (20) -> (30) -> null

// 2. Insert at positions
list.prepend(5);                   // Add to beginning
list.insertAt(15, 2);              // Insert 15 at index 2
console.log(list.toString());     // (5) -> (10) -> (15) -> (20) -> (30) -> null

// 3. Query list
console.log(list.size());          // 5
console.log(list.head());          // Node { value: 5, nextNode: ... }
console.log(list.tail());          // Node { value: 30, nextNode: null }

// 4. Search operations
console.log(list.find(20));        // 3 (index)
console.log(list.at(2));           // Node { value: 15, ... }
console.log(list.contains(15));    // true

// 5. Remove elements
list.removeAt(2);                  // Remove 15
list.pop();                        // Remove last (30)
console.log(list.toString());     // (5) -> (10) -> (20) -> null

// 6. Final state
console.log(list.size());          // 3
```

## 🎓 Concepts Demonstrated

### Data Structure Fundamentals
- ✅ **Pointer/Reference**: nextNode points to next element
- ✅ **Head & Tail**: Entry and exit points
- ✅ **Linear Structure**: Sequential access only
- ✅ **Dynamic Allocation**: Nodes created as needed

### Node Operations
- ✅ **Insertion**: At beginning (O(1)), end (O(n)), middle (O(n))
- ✅ **Deletion**: Remove by index, pop from end
- ✅ **Traversal**: Walk from head to tail
- ✅ **Pointer Updates**: Maintain chain integrity

### Algorithm Patterns
- ✅ **Linear Search**: O(n) traversal
- ✅ **Two-Pointer**: Previous and current for insertion/deletion
- ✅ **Sentinel Pattern**: null as end marker

### Modern JavaScript
- ✅ **ES6 Modules**: import/export
- ✅ **Class Syntax**: Object-oriented design
- ✅ **Constructor**: Initialize with listHead

## 💡 Real-World Applications

Linked lists are used in:
- **Browser History**: Back button navigation (doubly-linked)
- **Undo/Redo**: Stack implementation with linked lists
- **Task Schedulers**: Process queue management
- **Memory Allocation**: Kernel memory managers
- **Chat Applications**: Message history
- **Music Playlists**: Song queue
- **Sparse Arrays**: Storing non-zero elements only
- **Symbol Tables**: Compiler variable tracking

## 📈 Performance Comparison

| Operation | Linked List | Array |
|-----------|-------------|-------|
| Prepend | O(1) | O(n) |
| Append | O(n) | O(1) amortized |
| Insert at index | O(n) | O(n) |
| Remove at index | O(n) | O(n) |
| Search by value | O(n) | O(n) |
| Access by index | O(n) | O(1) |
| Space | O(n) | O(n) |

**When to use Linked Lists:**
- Frequent insertions/deletions at beginning
- Unknown/changing size
- Memory fragmentation concerns
- Queue implementations

**When to use Arrays:**
- Frequent random access
- Fixed size or growing slowly
- Cache locality matters
- Simple sequential iteration

## 🎯 Interview & Hiring Value

This project demonstrates:
1. **DSA Knowledge** - Understanding of fundamental data structures
2. **Pointer Manipulation** - Managing node connections
3. **Edge Case Handling** - Empty list, single node, boundaries
4. **Algorithm Optimization** - Trade-offs between O(1) and O(n)
5. **Modern JavaScript** - ES6 modules and classes
6. **Code Organization** - Separation of Node and LinkedList classes

## 🔍 Code Quality

- **Methods**: 14 core operations
- **Classes**: 2 (Node, LinkedList)
- **Lines of Code**: ~100 lines
- **Module System**: ES6 import/export
- **Test Script**: main.js with usage examples
- **Documentation**: Clear method organization

## 📝 Project Files

| File | Purpose |
|------|----------|
| `linkedList.js` | LinkedList class with 14 methods |
| `node.js` | Node class definition |
| `main.js` | Usage examples and test script |
| `package.json` | Project metadata |

## 📝 License

ISC License

---

**Repository**: [github.com/NabeelFarooq/LinkedList](https://github.com/NabeelFarooq/LinkedList)  
**Created**: Fundamental data structures portfolio project  
**Purpose**: Interview preparation and data structure mastery  
**Tech Stack**: JavaScript (ES6 modules), Node.js