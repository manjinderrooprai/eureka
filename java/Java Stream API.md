# Java Stream API

The Java Stream API is a powerful feature introduced in Java 8 that allows you to process collections of data in a functional style. Streams make operations like filtering, mapping, and reducing more concise and readable.

### What is a Stream?
A Stream is a sequence of elements that supports various operations to process data. It does not store data but instead operates on data from a source (like a List, Set, or Map).

**Key Characteristics of Streams:**
- ✅ Functional-style processing
- ✅ Lazily evaluated (operations are executed only when needed)
- ✅ Does not modify the original data
- ✅ Can be parallelized for performance improvements

### 1. Ways to Obtain a Stream:
- **From Collections:** All collections in Java (`List`, `Set`, `Queue`) have the `.stream()` method.
- **From Arrays:** Use `Arrays.stream()` or `Stream.of()`.
- **From File or I/O Channels:** You can create streams from files using `Files.lines()`.

### 2. **Intermediate Operations**
Intermediate operations **transform a stream into another stream**. They are **lazy**, meaning they do not execute until a terminal operation is invoked.

| Operation   | Description                          | Example                      |
|------------|-------------------------------------|-----------------------------|
| `filter()`  | Filters elements based on a condition | `stream.filter(s -> s.startsWith("A"))` |
| `map()`     | Transforms each element            | `stream.map(String::toUpperCase)` |
| `sorted()`  | Sorts elements                     | `stream.sorted()` |
| `distinct()`| Removes duplicate elements         | `stream.distinct()` |
| `limit(n)`  | Limits the number of elements      | `stream.limit(2)` |
| `skip(n)`   | Skips the first `n` elements       | `stream.skip(2)` |

### 3. **Terminal Operations**
Terminal operations **end the stream pipeline** and **trigger the actual data processing**.

| Operation       | Description                  | Example                   |
|----------------|-------------------------------|--------------------------|
| `collect()`    | Collects elements into a collection | `collect(Collectors.toList())` |
| `forEach()`    | Performs an action on each element | `forEach(System.out::println)` |
| `reduce()`     | Combines elements into a single result | `reduce(0, Integer::sum)` |
| `count()`      | Counts the elements         | `stream.count()` |
| `anyMatch()`   | Checks if any element matches | `stream.anyMatch(s -> s.startsWith("A"))` |
| `allMatch()`   | Checks if all elements match | `stream.allMatch(s -> s.length() > 3)` |
| `noneMatch()`  | Checks if no elements match  | `stream.noneMatch(s -> s.isEmpty())` |

### 🔑 **Summary**
- **Obtaining a Stream:** Get a stream from collections, arrays, or files.
- **Intermediate Operations:** Filter, transform, or sort the stream (lazy evaluation).
- **Terminal Operations:** Produce the final result like collecting, counting, or reducing
