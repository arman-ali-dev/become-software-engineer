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
