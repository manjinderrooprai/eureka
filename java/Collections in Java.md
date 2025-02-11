# Collections in Java

### What is Collection in Java?
> A Collection represents a single unit of objects, i.e., a group.

### What is a framework in Java?
> A framework provides a ready-made structure of classes and interfaces for building software applications efficiently.

### What is Collection framework
> The Collection framework represents a unified architecture for storing and manipulating a group of objects. It enhances code efficiency and readability by offering various data structures, including arrays, linked lists, trees, and hash tables, tailored to different programming needs.
### Advantages of the Java Collection Framework
1. **Reusability:** The framework provides a comprehensive set of common classes and utility methods applicable across various types of collections.
2. **Quality:** Leveraging the Java Collections Framework elevates the quality of programs.
3. **Speed:** Developers often report an increase in development speed when using the Collections Framework.
4. **Maintenance:** The open-source nature of the Java Collections Framework, coupled with readily available API documentation, facilitates easier code maintenance.
5. **Reduces Effort to Design New APIs:** An additional benefit is the reduced necessity for API designers and implementers to create new collection mechanisms for each new API.

### Hierarchy of Collection Framework
![Hierarchy of Collection Framework](diagrams/java-collection-hierarchy.png)
- **Class:** A class is a **blueprint from which individual objects are created.** It encapsulates data for objects through fields (attributes) and defines behavior via methods.
- **Interface:** An interface is a reference type in Java that can **contain constants and abstract methods (methods without a body).** Interfaces **specify what a class must do but not how it does it,** enforcing a set of methods that the class must implement.

### Methods of Collection interface
| No. | Method                                               | Description                                                                 |
| --- | ---------------------------------------------------- | --------------------------------------------------------------------------- |
| 1   | public boolean add(E e)                              | It is used to insert an element in this collection.                         |
| 2   | public boolean addAll(Collection<? extends E> c)     | It is used to insert the specified collection elements in the invoking collection. |
| 3   | public boolean remove(Object element)                | It is used to delete an element from the collection.                        |
| 4   | public boolean removeAll(Collection<?> c)            | It is used to delete all the elements of the specified collection from the invoking collection. |
| 5   | default boolean removeIf(Predicate<? super E> filter) | It is used to delete all the elements of the collection that satisfy the specified predicate. |
| 6   | public boolean retainAll(Collection<?> c)            | It is used to delete all the elements of invoking collection except the specified collection. |
| 7   | public int size()                                    | It returns the total number of elements in the collection.                 |
| 8   | public void clear()                                  | It removes the total number of elements from the collection.               |
| 9   | public boolean contains(Object element)              | It is used to search an element.                                           |
| 10  | public boolean containsAll(Collection<?> c)          | It is used to search the specified collection in the collection.           |
| 11  | public Iterator iterator()                           | It returns an iterator.                                                    |
| 12  | public Object[] toArray()                            | It converts collection into array.                                         |
| 13  | public <T> T[] toArray(T[] a)                        | It converts collection into array. Here, the runtime type of the returned array is that of the specified array. |
| 14  | public boolean isEmpty()                             | It checks if collection is empty.                                          |
| 15  | default Stream<E> parallelStream()                   | It returns a possibly parallel Stream with the collection as its source.   |
| 16  | default Stream<E> stream()                           | It returns a sequential Stream with the collection as its source.          |
| 17  | default Spliterator<E> spliterator()                 | It generates a Spliterator over the specified elements in the collection.  |
| 18  | public boolean equals(Object element)                | It matches two collections.                                                |
| 19  | public int hashCode()                                | It returns the hash code number of the collection.                         |

## Iterator interface
Iterator interface provides the facility of iterating the elements in a forward direction only. The Iterable interface is the root interface for all the collection classes. The Collection interface extends the Iterable interface and therefore all the subclasses of Collection interface also implement the Iterable interface.
```
It contains only one abstract method. i.e.
Iterator<T> iterator()
```
| No. | Method                  | Description                                                                 |
| --- | ----------------------- | --------------------------------------------------------------------------- |
| 1   | public boolean hasNext() | It returns true if the iterator has more elements otherwise it returns false. |
| 2   | public Object next()     | It returns the element and moves the cursor pointer to the next element.    |
| 3   | public void remove()     | It removes the last element returned by the iterator. It is less used.      |

# List Interface
List interface is the child interface of Collection interface. It inhibits a list type data structure in which we can store the ordered collection of objects. It can have duplicate values.

**Key Methods of List:**
- **add(E e):** Adds the specified element to the end of the list.
- **get(int index):** Returns the element at the specified index.
- **set(int index, E element):** Replaces the element at the specified index with the given element.
- **remove(int index):** Removes the element at the specified index.
- **remove(Object o):** Removes the first occurrence of the specified element (if it exists).
- **size():** Returns the number of elements in the list.
- **isEmpty():** Returns true if the list contains no elements.
- **contains(Object o):** Returns true if the list contains the specified element.
- **clear():** Removes all elements from the list.
- **indexOf(Object o):** Returns the index of the first occurrence of the specified element.
- **toArray():** Converts the ArrayList to an array.

```
List <data-type> list1 = new ArrayList();
List <data-type> list2 = new LinkedList();  
List <data-type> list3 = new Vector();  
List <data-type> list4 = new Stack();  
```
### ArrayList
ArrayList is a **resizable array** implementation of the List interface. It is part of the **java.util package** and allows for the storage of **ordered elements** that can be **accessed by index**.

**Key Characteristics of ArrayList:**
- **Dynamic Size:** Unlike arrays, an ArrayList can resize itself automatically as elements are added. It grows dynamically as needed.
- **Indexed Access:** Elements in an ArrayList are ordered, and you can access them directly using an index. Indexing starts from 0.
- **Allows Duplicates:** ArrayList allows duplicate elements, meaning that multiple occurrences of the same object can be stored.
- **Maintains Insertion Order:** Elements are stored in the order they are added, and this order is maintained when iterating over the ArrayList.
- **Not Synchronized:** ArrayList is not thread-safe. If multiple threads are accessing and modifying an ArrayList concurrently, external synchronization is required.

**Performance:**

**Time Complexity:**
- **Accessing elements:** get(index) and set(index, element) have O(1) time complexity (constant time).
- **Adding elements:** Adding an element at the end of the list is generally O(1), but occasionally resizing the array (when it is full) can cause O(n) time complexity.
- **Inserting or removing elements:** Inserting or removing elements at a specific index requires shifting elements, which takes O(n) time.
- **Searching for an element:** Searching for an element (using contains()) takes O(n) time since it involves iterating over the list.

**Space Complexity:**
- The space complexity of an ArrayList is proportional to the number of elements stored in it. It is backed by an array, so the list consumes more memory than an equivalent array.

```
Class ArrayListExample{
  public static void main(String ...){
    ArrayList<String> list = new ArrayList<>();
    list.add("Manjinder Singh Rooprai");
    Iterator itr = list.iteractor();
    while(itr.hasNext()){
      System.out.println(itr.next());
    }
  }
}
```
### LinkedList
LinkedList implements the **Collection interface.** It uses a **doubly linked list** internally to store the elements. It can **store the duplicate elements.** It **maintains the insertion order and is not synchronized.** In LinkedList, the **manipulation is fast** because no shifting is required.
```
Class LinkedListExample{
  public static void main(String ...){
    LinkedList<String> list = new LinkedList<>();
    list.add("Manjinder Singh Rooprai");
    Iterator itr = list.iteractor();
    while(itr.hasNext()){
      System.out.println(itr.next());
    }
  }
}
```

### Vector
Vector uses a **dynamic array** to store the data elements. It is similar to ArrayList. However, it **is synchronized** and **contains many methods that are not the part of Collection framework.**
```
Class VectorExample{
  public static void main(String ...){
    Vector<String> vector = new Vector<>();
    vector.add("Manjinder Singh Rooprai");
    Iterator itr = vector.iteractor();
    while(itr.hasNext()){
      System.out.println(itr.next());
    }
  }
}
```

### Stack
The stack is the **subclass of Vector.** It implements the **last-in-first-out data structure, i.e., Stack.** The stack **contains all of the methods of Vector class** and also provides its methods like **boolean push(), boolean peek(), boolean push(object o), which defines its properties.**
```
Class StackExample{
  public static void main(String ...){
    Stack<String> stack = new Stack<>();
    stack.push("Manjinder Singh Rooprai");
    stack.pop
    Iterator itr = stack.iteractor();
    while(itr.hasNext()){
      System.out.println(itr.next());
    }
  }
}
```

# Queue Interface
Queue interface maintains the **first-in-first-out order.** It can be defined as an **ordered list** that is used to hold the elements which are **about to be processed.** There are various classes like **PriorityQueue, Deque, and ArrayDeque which implements the Queue interface.**
```
Queue<String> queue = new PriorityQueue<>();
```

### PriorityQueue
The PriorityQueue class **implements the Queue interface.** It holds the elements or objects which are **to be processed by their priorities.** PriorityQueue **doesn't allow null values** to be stored in the queue.
The elements in a PriorityQueue **are ordered according to their natural ordering (e.g., numeric or lexicographical order) or by a custom comparator** provided at the time of creation.

**Key Features of PriorityQueue:**
- **Order of Elements:** The elements are ordered according to their priority, with the highest priority element being at the front of the queue.
- **Not FIFO:** Unlike a regular queue (which follows FIFO—First In, First Out), the PriorityQueue orders elements based on their priority, not the order they were inserted.
- **Efficient Operations:** Operations like add(), poll(), and peek() are efficient, typically logarithmic in time complexity (O(log n)).
- **Heap-based Implementation:** Internally, PriorityQueue uses a binary heap, which ensures that both insertion and removal of the highest-priority element are fast.
```
Class PriorityQueueExample{
  public static void main(String ...){
    PriorityQueue<String> priorityQueue = new PriorityQueue<>();
    priorityQueue.add("Manjinder Singh Rooprai");

    System.out.println(priorityQueue.element());
    System.out.println(priorityQueue.peek());

    Iterator itr = priorityQueue.iteractor();
    while(itr.hasNext()){
      System.out.println(itr.next());
    }
    priorityQueue.remove();
    priorityQueue.poll();
  }
}
```

**Important Methods:**
- **add(E e):** Inserts the element into the priority queue.
- **offer(E e):** Similar to add(), but it returns false if the element cannot be added (useful when capacity is limited).
- **poll():** Removes and returns the highest-priority element. If the queue is empty, it returns null.
- **peek():** Returns the highest-priority element without removing it. If the queue is empty, it returns null.
- **remove(Object o):** Removes a specific element from the queue.
- **size():** Returns the number of elements in the queue.

**Performance Considerations:**
- Insertion (add(), offer()): **O(log n)**
- Removal (poll()): **O(log n)**
- Peek (peek()): **O(1)**

# Deque Interface
Deque interface **(short for Double-Ended Queue)** is a part of the **java.util package** and **extends the Queue interface**. It represents a **linear collection** that allows elements **to be added or removed from both ends—front and back—providing** more flexibility than a regular queue.

**Key Characteristics of Deque:**
- **Double-Ended:** A Deque allows you to insert and remove elements from both the front and the back of the queue, unlike a standard FIFO (First-In-First-Out) queue that only allows insertions at the rear and removals from the front.
- **Interfaces in Java Collections:** It extends the Queue interface, meaning it **inherits the methods from Queue, such as offer(), poll(), and peek().** Additionally, it **provides extra methods for operations at both ends, such as addFirst(), addLast(), removeFirst(), and removeLast().**
- **Versatile:** You can use it as **both a queue and a stack (Last-In-First-Out)**. This versatility makes it ideal for many **use cases, such as undo/redo operations, task scheduling, or windowed operations.**

### ArrayDeque
ArrayDeque class implements the Deque interface. It facilitates us to use the Deque. Unlike queue, we can add or delete the elements from both the ends.

**Key Features of ArrayDeque:**
- **Resizable Array:** Internally, ArrayDeque uses a **dynamic array** to store the elements. This allows it to grow or shrink as needed, providing **better space efficiency compared to LinkedList** for most use cases.
- **No Capacity Limitation:** Unlike a regular array, the underlying array in ArrayDeque resizes automatically when needed (when elements are added or removed).
- **Faster than LinkedList for Most Operations:** Since ArrayDeque uses an array, operations at both ends (like adding/removing elements) are typically faster and use less memory than operations in a LinkedList (which requires pointer manipulation).
- **Not Thread-Safe:** ArrayDeque is not thread-safe, meaning that if multiple threads access the deque concurrently, external synchronization is required.
- **No Capacity Limit (unless specified):** By default, ArrayDeque does not have a fixed size, and its size dynamically adjusts based on the number of elements.

**Key Methods of ArrayDeque:**
**Adding elements:**
- **addFirst(E e):** Inserts the specified element at the front of the deque.
- **addLast(E e):** Inserts the specified element at the end of the deque.
- **offerFirst(E e):** Inserts the specified element at the front of the deque, returns true if successful, or false if the deque is full.
- **offerLast(E e):** Inserts the specified element at the end of the deque, returns true if successful, or false if the deque is full.

**Removing elements:**
- **removeFirst():** Removes and returns the first element from the deque.
- **removeLast():** Removes and returns the last element from the deque.
- **pollFirst():** Removes and returns the first element from the deque, or returns null if the deque is empty.
- **pollLast():** Removes and returns the last element from the deque, or returns null if the deque is empty.

**Peeking elements:**
- **getFirst():** Returns the first element without removing it.
- **getLast():** Returns the last element without removing it.
- **peekFirst():** Returns the first element without removing it, or null if the deque is empty.
- **peekLast():** Returns the last element without removing it, or null if the deque is empty.

```
Class ArrayDequeExample{
  public static void main(String ...){
    Deque<String> deque = new ArrayDeque<>();
    deque.addFirst("Manjinder Singh Rooprai");
    deque.addLast("Manjinder");

    System.out.println(deque.peekLast());
    System.out.println(deque.peekFirst());
    deque.removeFirst();
    deque .clear();
  }
}
```
# Set Interface
The Set Interface in Java represents a collection of **unique elements**, where **duplicate elements are not allowed.** It **extends the Collection Interface** and provides methods for handling sets. The most common implementing classes of the Set interface are **HashSet, LinkedHashSet, and TreeSet.** We can store at **most one null** value in Set.

### HashSet
HashSet is a collection class that **implements the Set interface** and is part of the **java.util package.** It is a collection that **does not allow duplicate elements** and **does not guarantee any specific order** of the elements. This class is **backed by a hash table (actually a HashMap instance)**, which allows for **constant-time performance (O(1))** for basic operations like **add(), remove(), and contains().**

**Key Characteristics of HashSet:**
- **No Duplicates:** A HashSet ensures that each element is unique. If you attempt to add a duplicate element, it will simply not be added.
- **Unordered:** The elements in a HashSet are unordered, meaning they are not stored in any specific order. The order of elements may change over time.
- **Null Elements:** HashSet allows one null element to be stored, but only one null value is allowed because duplicates are not permitted.
- **Backed by Hashing:** It uses a hash table for storing the elements, which provides very fast look-up times.
- **Not Synchronized:** HashSet is not thread-safe. If multiple threads access the HashSet concurrently and at least one thread modifies it, it must be synchronized externally.

**Basic Operations in HashSet:**
- **add(E e):** Adds the specified element to the set if it is not already present. Returns true if the element was added, false if it was already in the set.
- **remove(Object o):** Removes the specified element from the set if it exists. Returns true if the element was removed, false if it wasn't found.
- **contains(Object o):** Returns true if the set contains the specified element.
- **size():** Returns the number of elements in the set.
- **isEmpty():** Returns true if the set is empty.
- **clear():** Removes all elements from the set.
- **iterator():** Returns an iterator over the elements in the set.

```
Class HashSetExample{
  public static void main(String ...){
    HashSet<String> hashSet = new HashSet<>();
    hashSet.add("Manjinder Singh Rooprai");
    Iterator itr = hashSet.iteractor();
    while(itr.hasNext()){
      System.out.println(itr.next());
    }
  }
}
```

### LinkedHashSet
LinkedHashSet is a Set implementation that **combines the properties of a HashSet and a LinkedList.** It is part of the **java.util package** and provides a set that **guarantees the insertion order** of elements while maintaining the **unique elements property (like a HashSet)**. This means that the **elements in a LinkedHashSet are stored in the order they were added**, and **no duplicates are allowed.**

**Key Characteristics of LinkedHashSet:**
- **Unique Elements:** Like a HashSet, a LinkedHashSet does not allow duplicate elements.
- **Maintains Insertion Order:** It preserves the order in which elements were inserted into the set. This means that when you iterate through a LinkedHashSet, the elements will be returned in the same order they were added.
- **Uses a Linked Hash Map:** Internally, it uses a hash table combined with a linked list to maintain the order of insertion. This provides faster access than a LinkedList, while still maintaining order.
- **Not Thread-Safe:** LinkedHashSet is not thread-safe, so if multiple threads are modifying it, external synchronization is needed.
- **Allows null:** Just like HashSet, a LinkedHashSet allows one null element, but only one null element is allowed since duplicates are not permitted.

**Performance:**
- **Time Complexity:** The basic operations (**add(), remove(), contains()) generally have O(1) time complexity**, just like a HashSet. However, since it maintains insertion order, **iteration over elements is done in O(n) time.**
- **Space Complexity:** Slightly **higher than HashSet because it uses an additional linked list to maintain the order of insertion.**

```
Class LinkedHashSetExample{
  public static void main(String ...){
    LinkedHashSet<String> linkedHashSet = new LinkedHashSet<>();
    linkedHashSet.add("Manjinder Singh Rooprai");
    Iterator itr = linkedHashSet.iteractor();
    while(itr.hasNext()){
      System.out.println(itr.next());
    }
  }
}
```
