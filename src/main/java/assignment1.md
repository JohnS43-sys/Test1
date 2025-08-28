
## ✅ **IB Computer Science – Paper 2 Style Exam Question**
### **Topic: OOP, Linked Lists, Stacks, and Data Structure Selection**

---
### Part A
### **Question 1 – Customer Discount Correction System**
**[Total: 17 marks]**

A retail store uses a transaction system to record each customer's purchase at checkout. Each customer has a name, purchase amount, loyalty tier, and the hour of purchase (in 24-hour format). The store operates from 9:00 AM to 9:00 PM (21:00).

Due to a software bug, a **flat 5% discount** was mistakenly applied to all customers during the **last hour of operation (20:00–21:00)**. The correct discount policy is based on loyalty:

- **Bronze**: 5%
- **Silver**: 10%
- **Gold**: 25%

The system currently stores customers in a **singly linked list** in the order they checked out.

---

### **Given Classes:**

```java
class Customer {
    private String name;
    private double lastPurchase;  // already reduced by 5% due to bug
    private String loyaltyTier;   // "Bronze", "Silver", "Gold"
    private int hour;             // 9 to 21 (24-hour format)

    public Customer(String name, double lastPurchase, String loyaltyTier, int hour) {
        this.name = name;
        this.lastPurchase = lastPurchase;
        this.loyaltyTier = loyaltyTier;
        this.hour = hour;
    }

    // Getters
    public String getName() { return name; }
    public double getLastPurchase() { return lastPurchase; }
    public String getLoyaltyTier() { return loyaltyTier; }
    public int getHour() { return hour; }

    // Setter
    public void setLastPurchase(double amount) { this.lastPurchase = amount; }

    // Returns correct discount rate
    public double getCorrectDiscountRate() {
        switch(loyaltyTier) {
            case "Gold": return 0.25;
            case "Silver": return 0.10;
            case "Bronze": return 0.05;
            default: return 0.05; 
        }
    }
}
```

```java
class TransactionLog {
    private Node head;

    private class Node {
        Customer customer;
        Node next;

        public Node(Customer customer) {
            this.customer = customer;
            this.next = null;
        }
    }

    public TransactionLog() {
        head = null;
    }

    // Adds customer to the end of the list (chronological order)
    public void addCustomer(Customer customer) {
        Node newNode = new Node(customer);
        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }
}
```

---

### **(a)**
Write a method in the `TransactionLog` class called:
```java
//public void correctLastHourDiscounts()
        
```
This method must:
- Traverse the **entire linked list**
- Identify customers who checked out between **20:00 and 21:00 (inclusive)**
- For each such customer:
    - **Reverse the incorrect 5% discount**
    - Apply the **correct discount** based on loyalty tier
    - Update the `lastPurchase` with the corrected value


**[8 marks]**

public void correctLastHourDiscounts(){
  Node current = head;
  while(current != null){
    if(current.customer.getHour() >= 20 && current.customer.getHour() <= 21){
      int original = current.customer.getLastPurchase() / 0.95;
      int corrected = 0;
      switch(current.customer.getLoyaltyTier()){
        case "Gold": corrected = original * 0.75;
        break;
        case "Silver": corrected = original * 0.9;
        break;
        case "Bronze": corrected = original * 0.95;
        break;
      }
    }
    current.customer.setLastPurchase(corrected);
  }
  current = current.next;
}



---

### **(b)**
Explain why using a **singly linked list** is **inefficient** for this type of operation — especially if the store needs to **frequently correct the most recent transactions**.

Suggest a **better data structure** for storing transactions when **recent entries need to be accessed or modified quickly**, and justify your choice.

**[4 marks]**
---

A singly linked list is inefficient for this type of operation since in order to modify elements in a singly linked list it takes an O(n)
time, unlike a more optimal data structure for this case, which would be an array since modifying and accessing elements in an array takes a constant
O(1) time. 

### **(c)**
Describe how the **stack** data structure follows the **LIFO principle**, and explain why this makes it **particularly suitable** for modeling **transaction undo systems** or **rollback operations** in point-of-sale software.

**[3 marks]**

---

A stack follows the LIFO principle since the last node inserted into the stack, is the first node to be popped from the stack whenever the pop(); method is used. 
This means that the stack data structure is particularly useful for transaction undo systems or rollback operations in point of sale software as the pop(); method can 
be used directly in these systems. 

### **(d)**
State **one disadvantage** of using a stack for this transaction system if the store also needs to **generate daily reports sorted by time** or **search for a customer by name**.

One disadvantage of using a stack is that there is no way to directly access any given element inside of it, and all popped nodes inside the stack
will have to be reinserted into the stack. 

**[2 marks]**

---



### **Task 1 (c): Binary Search Application**

The store now wants to **quickly find a customer by name** in a **separate sorted array** of customers (not the linked list). The array is sorted alphabetically by name.

Write a **binary search method** (not in the list class) that searches for a customer by name and returns the index, or -1 if not found.

Assume you are given:
```java
Customer[] sortedCustomers; // sorted by name
```

Write the method:
```java
public int binarySearchCustomer(Customer[] arr, String targetName)
```

You may assume `Customer` has a `getName()` method.

**[6 marks]**

> 🔎 *Note: This tests understanding of binary search preconditions (sorted data) and implementation.*

---

public int binarySearchCustomer(Customer[] arr, String targetName){
  int low = 0;
  int high = arr.length-1;
  while(low <= high){
    int mid = low + (high - low) / 2;
    int comparison = arr[mid].compareTo(targetName);
    if(comparison == 0){
      return mid;
    }
    if(comparison > 0){
      high = mid - 1;
    }
    else{
      low = mid + 1;
    }
    
  }
  return -1;
}

## **Question 2: Stack Applications**

### **Standard Stack Operation**

You are given a **stack of integers**. Write a method that **reverses the stack** using **only one queue** as auxiliary storage.

You may only use standard stack and queue operations (`push`, `pop`, `peek`, `enqueue`, `dequeue`, `isEmpty`).

Write the method:
```java
public void reverseStack(Stack<Integer> stack)
```

**[6 marks]**

> 💡 *Hint: Use the queue to temporarily store elements, then re-push them back.*

---

public void reverseStack(Stack<Integer> stack){
  Queue<Integer> queue1 = new LinkedList<>();
  while(!stack.isEmpty()){
    queue1.enqueue(stack.pop());
  }
  while(!queue1.isEmpty()){
    stack.push(queue1.dequeue());
  }
}