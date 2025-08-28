

### **Part B: "Undo System for Text Editor"**

A simple text editor uses a **stack** to support **undo** operations. Every time the user types a word, it is pushed onto the `actionStack`. The editor also supports a **"redo"** feature, but only **immediately after an undo**, and only **once**.

You are to design a system using **two stacks**:
- `actionStack`: stores words typed (most recent on top)
- `redoStack`: stores words that were undone (only one level of redo allowed)

Implement a method:
```java
public String undoLastAction()
```
- Pops the last word from `actionStack`
- Pushes it to `redoStack` (only if `redoStack` is empty — no multiple redos)
- Returns the undone word

Also implement:
```java
public String redoLastUndo()
```
- Only works if `redoStack` is not empty
- Moves the word back to `actionStack`
- Returns the word, or `null` if redo not possible


```java
import java.util.Stack;

public class TextEditor {
    private Stack<String> actionStack;
    private Stack<String> redoStack;

    public TextEditor() {
        actionStack = new Stack<>();
        redoStack = new Stack<>();
    }

    /**
     * Undo the last action: pop from actionStack, push to redoStack (if empty)
     * @return the undone word, or null if no action to undo
     */
    public String undoLastAction() {
        if (actionStack.isEmpty()) {
            return null;
        }
        String word = actionStack.pop();
        redoStack.push(word);
        return word;
        
    }

    /**
     * Redo the last undone action
     * @return the word restored, or null if redo not possible
     */
    public String redoLastUndo() {
        if(redoStack.isEmpty()){
            String word = actionStack.push(redoStack.pop());
            return word;
        }
        return null;
    }
}
```

---

**[7 marks]**

> 🎯 *Tests understanding of stack use in real systems and constraints.*

---

## **Question 3: Binary Trees – Diagram-Based Operations**

### **Given**:
A **binary search tree (BST)** with the following nodes inserted in this order:  
**50, 30, 70, 20, 40, 60, 80**

---

### **Part A**:
Draw the **final structure** of the BST after all insertions. Label all nodes.

**[3 marks]**

        50
        /  \
       30  70
      / \  / \
     20 40 60 80
---

### **Part B**:
Now perform the following operations **in sequence**, drawing the tree **after each step**:

1. Insert **35**
2. Insert **75**
3. Delete **30** (use standard BST deletion: if two children, replace with **in-order predecessor**)
4. Delete **70**

Show the tree after **each** operation.

**[8 marks – 2 each]**

> 📌 *Ensure diagrams are clear, with left/right children correctly positioned.*
> 
1.       50
        /  \
       30  70
      / \  / \
     20 40 60 80
        /
       35

2.      50
        /  \
       30  70
      / \  / \
     20 40 60 80
       /      /
      35     75

3.      50
       /  \
      20  70
     / \  / \
    35 40 60 80
            /
          75
4.       50
        /  \
       20  75
       / \  / \
      35 40 60 80
              
---


### **Part C**:
After the final tree, state:
- The **height** of the tree
- Whether it is **balanced**
- One advantage of a **balanced BST** over an unbalanced one

**[3 marks]**

The height of the final tree is 3 nodes tall. It is a balanced binary search tree as there
is an equal number of nodes on the left and right side of the parent node, 50. One advantage
of a balanced BST over an unbalanced one is that it allows for more consisted and faster in-order traversal
and insertion of nodes. 
---

## **Question 4: Vocabulary & Diagram Quiz**

### **Part A: Definitions**
Define the following terms (1 mark each):

1. Node
2. Singly linked list
3. Stack (LIFO)
4. Binary search tree (BST)
5. Balanced tree
6. In-order traversal
7. Overflow (in stack context)
8. Head (in linked list)

**[8 marks]**

1.A fundamental unit in a datastructure that contains data as well as a reference to other nodes via pointers.
2. A linear data structure that is composed of a list of nodes where each node points to the next node in the sequence. 
   3. A collection where the last added element is the first element to be removed via push() and pop() operations.
   4. A binary tree where each nodes subtree contains only smaller values than the parent node. The right subtree contains only values greater than the parent node.
   5. A tree where the height difference between the left and right subtree is at most 1. 
   6. Visiting nodes first starting from the left, then to the root, and then to the right. This produces a sorted output.
   7. Pushing an element onto a full stack.
   8. The first node in a linked list. 


---

### **Part B: Diagram Interpretation**

You are given the following **singly linked list diagram**:

```
[Anna] -> [Bob] -> [Cara] -> null
```

Each node contains a `Customer` object.

1. Label the **head node**.
2. What is the **successor** of Bob?
3. What happens if the reference from Bob to Cara is lost?
4. Why can't you traverse from Cara to Bob?

**[4 marks]**
1. The head node from this singly linked list is the node, [Anna]
2. The successor of the Bob node is the Anna Node.
3. If the reference from Bob to Cara is lost, the singly linked list will only consist of Anna and Bob
4. In a singly linked list you can only traverse forwards in a linked list, and since Cara is after Bob, you cannot traverse from Cara to Bob since there is no reference.
---

### **Part C: Tree Type Identification**

Given three tree diagrams (describe them verbally or sketch in exam):
- **Tree A**: All leaves at same level, full at every level
- **Tree B**: Skewed heavily to the left, height = n-1
- **Tree C**: Height difference between left and right subtrees ≤ 1 at every node

Identify each as:
- Full binary tree
- Skewed (unbalanced) tree
- Balanced BST

And state which would give **best search performance** and why.

**[5 marks]**

Tree A is a Full binary tree
Tree B is a Skewed (unbalanced) tree
Tree C is a Balanced BST

The Balanced BST has the best performance because it would maintain its O(logn) time complexity,
however other trees such as the skewed(unbalanced) tree can have possibly an O(n) time complexity if its 
the worst case. 


---