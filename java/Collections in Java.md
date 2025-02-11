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

### Iterator interface
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

## List Interface
List interface is the child interface of Collection interface. It inhibits a list type data structure in which we can store the ordered collection of objects. It can have duplicate values.

```
List <data-type> list1 = new ArrayList();
List <data-type> list2 = new LinkedList();  
List <data-type> list3 = new Vector();  
List <data-type> list4 = new Stack();  
```
### ArrayList
The ArrayList class implements the List interface. It uses **a dynamic array to store the duplicate element of different data types.** The ArrayList class **maintains the insertion order and is non-synchronized.** The elements stored in the ArrayList class **can be randomly accessed.**
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
    Iterator itr = vector.iteractor();
    while(itr.hasNext()){
    System.out.println(itr.next());
    }
  }
}
```
