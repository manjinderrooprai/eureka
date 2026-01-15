# Strings in Heap and String Constant Pool (SCP) 
Below is a **memory-level explanation** of your program, focusing strictly on the **Heap** and the **String Constant Pool (SCP)** and why each comparison evaluates the way it does.

## Key JVM Memory Concepts (Required to Understand This)

### 1. String Constant Pool (SCP)

* A **special area inside the Heap**.
* Stores **string literals** (e.g., `"you"`, `"yo"`).
* JVM ensures **only one instance per unique literal**.
* Reused across the application.

### 2. Heap (Non-Pool Area)

* Stores **objects created using `new`**.
* Each `new String("you")` creates a **new object**, even if the value already exists in SCP.

### 3. `==` vs `.equals()`

* `==` → **reference comparison** (memory address)
* `.equals()` → **content comparison**
* Your code uses `==`, so **only memory references matter**.

## Program Execution: Step-by-Step Memory Analysis

```java
public class App {
    public static void main(String[] args) throws Exception {
        System.out.println("Spring Constant Pool!");

        String s1 = new String("you");
        String s2 = new String("you");

        //1. 
        System.out.println(s1 == s2 );

        //2. 
        String s3 = "you";
        System.out.println(s1 == s3 );

        //3. 
        String s4 = "you";
        System.out.println(s2 == s4 );

        //4.
        String s5 = "yo" + "u";
        System.out.println(s5 == s3);

        //5. 
        String s6 = "yo";
        String s7 = s6 + "u";
        System.out.println(s7 == s4);

        //6.
        final String s8 = "yo";
        String s9 = s8 + "u";
        System.out.println(s4 == s9 ); 

    }
}
```

### JVM Startup

```java
System.out.println("Spring Constant Pool!");
```

* `"Spring Constant Pool!"` → Stored in **SCP**

---

## Object Creation Phase

### Step A: `new String("you")`

```java
String s1 = new String("you");
String s2 = new String("you");
```

**What happens internally:**

1. `"you"` literal → stored **once** in SCP
2. `new String("you")` → creates a **new Heap object**
3. Two separate Heap objects are created

**Memory:**

```
SCP:
  "you"  (1 object)

Heap:
  s1 → new String("you")  (Object #1)
  s2 → new String("you")  (Object #2)
```

---

## Output Analysis (Line by Line)

---

```java
System.out.println(s1 == s2);
```

* `s1` → Heap Object #1
* `s2` → Heap Object #2
* Different memory addresses

**Output:**

```text
false
```

---

```java
String s3 = "you";
System.out.println(s1 == s3);
```

* `s3` → points directly to `"you"` in SCP
* `s1` → Heap object

**Memory:**

```
SCP:
  "you" ← s3

Heap:
  s1 → Object
```

**Output:**

```text
false
```

---

```java
String s4 = "you";
System.out.println(s2 == s4);
```

* `s4` → same SCP object as `s3`
* `s2` → Heap object

**Output:**

```text
false
```

---

### (Compile-Time Concatenation)

```java
String s5 = "yo" + "u";
System.out.println(s5 == s3);
```

**Important rule:**

> **String literals concatenated at compile time are interned**

* `"yo" + "u"` → JVM computes this **at compile time**
* Result `"you"` is looked up in SCP
* No new object is created

**Memory:**

```
SCP:
  "yo"
  "u"
  "you" ← s3, s4, s5
```

**Output:**

```text
true
```

---

### (Runtime Concatenation)

```java
String s6 = "yo";
String s7 = s6 + "u";
System.out.println(s7 == s4);
```

**Key rule:**

> If **any operand is a variable**, concatenation happens at **runtime**

* `s6` is a variable → runtime operation
* JVM creates a **new String object in Heap**
* Interning does **not** happen automatically

**Memory:**

```
Heap:
  s7 → new String("you")

SCP:
  "you" ← s4
```

**Output:**

```text
false
```

---

### (Final Variable Optimization)

```java
final String s8 = "yo";
String s9 = s8 + "u";
System.out.println(s4 == s9);
```

**Critical rule:**

> `final` variables with constant values are treated as compile-time constants

* `s8` is `final` and initialized with a literal
* JVM treats `"yo" + "u"` as **compile-time**
* Result `"you"` reused from SCP

**Memory:**

```
SCP:
  "you" ← s3, s4, s5, s9
```

**Output:**

```text
true
```

---

## Final Output Summary

| Statement  | Result  |
| ---------- | ------- |
| `s1 == s2` | `false` |
| `s1 == s3` | `false` |
| `s2 == s4` | `false` |
| `s5 == s3` | `true`  |
| `s7 == s4` | `false` |
| `s4 == s9` | `true`  |

---

## One-Line Mental Model (Interview Gold)

* **Literals → SCP**
* **`new String()` → Heap**
* **Compile-time concatenation → SCP**
* **Runtime concatenation → Heap**
* **`final` enables compile-time folding**
* **`==` checks reference, not value**


---

## 1. After JVM Loads Literals

```text
String Constant Pool (inside Heap)
---------------------------------
"Spring Constant Pool!"
"you"
"yo"
"u"
```

---

## 2. After `new String("you")`

```java
String s1 = new String("you");
String s2 = new String("you");
```

```text
String Constant Pool (SCP)           Heap (Non-Pool)
--------------------------          -------------------------
"you"                               s1 ──▶ String@A ("you")
                                    s2 ──▶ String@B ("you")
```

* Two **different heap objects**
* Both copy value from SCP `"you"`

---

## 3. After Literal Assignments

```java
String s3 = "you";
String s4 = "you";
```

```text
String Constant Pool (SCP)           Heap
--------------------------          -------------------------
"you" ◀── s3                        s1 ──▶ String@A ("you")
  ▲                                 s2 ──▶ String@B ("you")
  └── s4
```

* `s3` and `s4` point to **same SCP object**
* `s1`, `s2` still separate

---

## 4. Compile-Time Concatenation

```java
String s5 = "yo" + "u";
```

```text
String Constant Pool (SCP)
--------------------------
"yo"
"u"
"you" ◀── s3, s4, s5
```

* `"yo" + "u"` resolved **at compile time**
* No new object created

---

## 5. Runtime Concatenation

```java
String s6 = "yo";
String s7 = s6 + "u";
```

```text
String Constant Pool (SCP)           Heap
--------------------------          -------------------------
"yo" ◀── s6                         s7 ──▶ String@C ("you")
"u"
"you" ◀── s3, s4, s5
```

* Runtime operation → **new Heap object**
* Not interned automatically

---

## 6. `final` Enables Compile-Time Folding

```java
final String s8 = "yo";
String s9 = s8 + "u";
```

```text
String Constant Pool (SCP)
--------------------------
"yo" ◀── s6, s8
"u"
"you" ◀── s3, s4, s5, s9
```

* `final` makes `s8` a compile-time constant
* JVM reuses `"you"` from SCP

---

## 🔍 Reference Comparison Summary

```text
s1 == s2  → false  (Heap vs Heap)
s1 == s3  → false  (Heap vs SCP)
s2 == s4  → false  (Heap vs SCP)
s5 == s3  → true   (SCP vs SCP)
s7 == s4  → false  (Heap vs SCP)
s9 == s4  → true   (SCP vs SCP)
```

---

## Interview-Ready One-Sentence Explanation

> **Heap objects created using `new` are always distinct, while compile-time string literals and constant expressions are stored and reused from the String Constant Pool.**


