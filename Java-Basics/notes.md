# Variables

## 1. Variables in Java
A **variable** is a named memory location used to store data.

### Types of Variables
1. **Local Variables**
   - Declared inside methods, constructors, or blocks.
   - Created when the method is invoked, destroyed when the method ends.
   - Must be initialized before use.
  
   ```java
   public void methodExample() {
       int age = 20; // local variable
       System.out.println(age);
   }
   ```

2. **Instance Variables**
    - Declared inside a class but outside any method/constructor/block.
    - Created when an object is created and destroyed when the object is destroyed.
    - Default values are assigned (0, false, null).
  
```java
class Student {
    String name;  // instance variable
    int rollNo;   // instance variable
}
```

3. **Static Variables (Class Variables)**
    - Declared using the static keyword.
    - Shared among all objects of a class.
    - Stored in the method area, created only once.
  
```java
class Student {
    static String schoolName = "ABC School"; // static variable
}
```

# Data Types
Java is statically typed, so every variable must have a declared type.
Data types are divided into Primitive and Non-Primitive.

## Primitive Data Types
| Data Type | Size (bits)       | Default Value | Range                 |
| --------- | ----------------- | ------------- | --------------------- |
| `byte`    | 8                 | 0             | -128 to 127           |
| `short`   | 16                | 0             | -32,768 to 32,767     |
| `int`     | 32                | 0             | -2^31 to 2^31-1       |
| `long`    | 64                | 0L            | -2^63 to 2^63-1       |
| `float`   | 32                | 0.0f          | \~7 decimal digits    |
| `double`  | 64                | 0.0d          | \~15 decimal digits   |
| `char`    | 16                | '\u0000'      | 0 to 65,535 (Unicode) |
| `boolean` | 1 (JVM-dependent) | false         | true / false          |

```java
int age = 21;
long population = 7800000000L;
float pi = 3.14f;
double price = 99.99;
char grade = 'A';
boolean isStudent = true;
```

## Non-Primitive Data Types
  - Created by the programmer.
  - Can store multiple values or objects.
  - Examples: String, Array, Class, Interface, Collections.

```java
String name = "Arman";
int[] numbers = {1, 2, 3, 4, 5};
```

## Type Casting in Java
Converting one data type into another.
1. **Widening Casting (Implicit) – smaller type → larger type**
```java
int num = 10;
double d = num; // int to double
```

2. **Narrowing Casting (Explicit) – larger type → smaller type**
```java
double d = 9.8;
int num = (int) d; // double to int
```

## Best Practices
1. Use meaningful variable names (camelCase convention).
2. Always initialize local variables before use.
3. Prefer int for integers, double for decimals (default choice).
4. Use var (Java 10+) for type inference when obvious.

# Conditional Statements

## 1. What are Conditional Statements?
Conditional statements allow a program to make decisions based on conditions (true/false).  
In Java, these are used to control the flow of execution.

---

## 2. Types of Conditional Statements in Java

### 2.1 `if` Statement
- Executes a block of code **only if** the condition is true.
```java
int age = 20;
if (age >= 18) {
    System.out.println("You are eligible to vote.");
}
```

### 2.2 if-else Statement
- Provides two paths: one for true condition, another for false.
```java
int age = 16;
if (age >= 18) {
    System.out.println("Eligible to vote");
} else {
    System.out.println("Not eligible to vote");
}
```

### 2.3 if-else-if Ladder
- Used when you have multiple conditions.
```java
int marks = 85;

if (marks >= 90) {
    System.out.println("Grade: A");
} else if (marks >= 75) {
    System.out.println("Grade: B");
} else if (marks >= 60) {
    System.out.println("Grade: C");
} else {
    System.out.println("Grade: D");
}
```

### 2.4 Nested if Statement
An if inside another if.
```java
int num = 10;

if (num > 0) {
    if (num % 2 == 0) {
        System.out.println("Positive Even Number");
    }
}
```

### 2.5 switch Statement
- Better alternative to multiple if-else for equality checks.
- Works with byte, short, int, char, String, enum.

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Invalid day");
}
```

### 3. Ternary Operator
- Shorthand for simple if-else.
- Syntax: condition ? value_if_true : value_if_false

```java
int age = 20;
String result = (age >= 18) ? "Adult" : "Minor";
System.out.println(result);
```

### 4. Best Practices
- Use if-else for range conditions.
- Use switch for multiple equality checks.
- Always include a default case in switch.
- Ternary operator is good for short, simple conditions.

# Loops

## 1. What are Loops?
Loops allow us to execute a block of code repeatedly until a condition is true.  
They help reduce code duplication and improve efficiency.

---

### 2.1 `for` Loop
- Used when the number of iterations is known in advance.
- Syntax:
  ```java
  for (initialization; condition; update) {
      // code to be executed
  }
  ```

### 2.2 while Loop
- Used when the number of iterations is not known in advance,
- but depends on a condition.
- Syntax
  ```java
  while (condition) {
    // code to be executed
   }
  ```

### 2.3 do-while Loop
- Similar to while, but ensures the code runs at least once even if the condition is false.
- Condition is checked after executing the loop body.
- Example
  ```java
  int i = 1;
  do {
       System.out.println("Number: " + i);
       i++;
   } while (i <= 5);
  ```
### 2.4 Enhanced for Loop (for-each)
- Used for iterating over arrays and collections.
- Easier and cleaner than traditional for.
- Example
```java
int[] numbers = {10, 20, 30, 40};

for (int num : numbers) {
    System.out.println(num);
}
```

### 3. Loop Control Statements
1. **break** – exits the loop immediately.
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) break;
    System.out.println(i);
}
// Output: 1, 2
```

2. **continue** – skips the current iteration and jumps to the next.
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    System.out.println(i);
}
// Output: 1, 2, 4, 5
```

3. **nested loops** – loop inside another loop.
```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        System.out.println("i = " + i + ", j = " + j);
    }
}
```

### 4. Best Practices
- Use for loop when you know the number of iterations.
- Use while/do-while when iterations depend on runtime conditions.
- Use enhanced for for arrays/collections (cleaner code).
- Avoid infinite loops unless required (while(true) for servers, event listeners, etc.).
- Always ensure loop condition updates to prevent infinite loops.

# Arrays

## 1. What is an Array?
- An **array** is a collection of elements of the same type stored in a contiguous memory location.
- Arrays in Java are **objects**.
- Array size is fixed (cannot grow or shrink).
- Indexing starts from **0**.

---

## 2. Declaring and Initializing Arrays

### 2.1 Declaration
```java
int[] arr;      // preferred way
int arr2[];     // also valid
```

### 2.2 Memory Allocation
```java
arr = new int[5];   // array of size 5, default values = 0
```

### 2.3 Declaration + Initialization
```java
int[] numbers = {10, 20, 30, 40, 50};
```

### 3. Accessing Array Elements
```java
int[] marks = {95, 85, 76, 64};
System.out.println(marks[0]); // Output: 95
marks[2] = 80;                // update element
```

### 4. Array Length
```java
int[] arr = {1, 2, 3, 4, 5};
System.out.println(arr.length);  // Output: 5
```

## 5. Iterating Through Arrays
### 5.1 Using for loop
```java
int[] arr = {1, 2, 3, 4, 5};
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

### 5.2 Using Enhanced for loop (for-each)
```java
for (int num : arr) {
    System.out.println(num);
}
```

## 6. Types of Arrays
### 6.1 One-Dimensional Array
```java
int[] arr = new int[5];
```

### 6.2 Multi-Dimensional Array
```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

System.out.println(matrix[0][2]); // Output: 3
```

### 7. Common Array Methods (via Arrays class)
```java
import java.util.Arrays;

int[] arr = {5, 2, 8, 1};

// Sorting
Arrays.sort(arr);

// Searching
int index = Arrays.binarySearch(arr, 8);

// Filling
Arrays.fill(arr, 0);
```

### 8. Limitations of Arrays
- Fixed size (cannot resize after creation).
- Only stores elements of the same type.
- For dynamic arrays, use ArrayList or other collections.


# Strings

## 1. What is a String?
- A **String** in Java is a sequence of characters.
- Strings are **immutable** (once created, they cannot be changed).
- Stored in **String Pool** (special memory area inside Heap).

---

## 2. Creating Strings

### 2.1 Using String Literal (preferred way)
```java
String str1 = "Hello";
```
- Stored in the String Pool.
- If the same literal is reused, JVM does not create a new object.

### 2.2 Using new keyword
```java
String str2 = new String("Hello");
```
- Always creates a new object in Heap, even if the same value exists.

### 3. Common String Methods
```java
String s = "Java Programming";

// 1. Length
System.out.println(s.length()); // 16

// 2. Character at index
System.out.println(s.charAt(0)); // J

// 3. Substring
System.out.println(s.substring(5));     // Programming
System.out.println(s.substring(0, 4));  // Java

// 4. Concatenation
String s1 = "Java";
String s2 = "Rocks";
System.out.println(s1 + " " + s2);      // Java Rocks

// 5. Contains
System.out.println(s.contains("Pro"));  // true

// 6. Equals vs ==
String a = "Hello";
String b = "Hello";
String c = new String("Hello");

System.out.println(a == b);      // true (same pool object)
System.out.println(a == c);      // false (different object)
System.out.println(a.equals(c)); // true (content check)

// 7. Ignore Case Comparison
System.out.println("java".equalsIgnoreCase("JAVA")); // true

// 8.Replace
System.out.println(s.replace("Java", "C++")); // C++ Programming

// 9. Split
String data = "apple,banana,grapes";
String[] fruits = data.split(",");

// 10. Trim (remove spaces)
String s3 = "   Hello World   ";
System.out.println(s3.trim());  // "Hello World"
```

### 4. StringBuilder and StringBuffer
- Since String is immutable, repeated modifications create new objects.
- **StringBuilder** (faster, not thread-safe) and **StringBuffer** (thread-safe) are used for mutable strings.

### Example with StringBuilder:
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
System.out.println(sb); // Hello World
```

### 5. Best Practices
- Use String literals for reuse and efficiency.
- Use StringBuilder for heavy modifications inside loops.
- Always prefer equals() for comparison, not ==.
- Remember: Strings are immutable.

# Exception Handling

## 1. What is an Exception?
- An **exception** is an unwanted event that disrupts the normal flow of a program.  
- Exceptions occur during **runtime** (not compile time).  
- Java provides a robust **exception handling mechanism** using `try-catch-finally`.

---
