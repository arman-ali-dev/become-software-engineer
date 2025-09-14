# Time and Space Complexity

## 1. What is Time Complexity?
Time complexity is a way to measure how much time an algorithm takes with respect to the size of input.
- Input size is usually represented as n.
- We do not calculate exact seconds, instead we calculate the growth rate (how fast the time increases as input grows).

### Common Time Complexities

#### 1. O(1) – Constant Time
- Execution time does not depend on input size.
- Example: Accessing an array element arr[5].

```java
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 20, 30, 40, 50};

    // Accessing an element directly (constant time operation)
    cout << "Element at index 2: " << arr[2] << endl;

    return 0;
}
```

#### 2. O(log n) – Logarithmic Time
- Time increases slowly even if input size grows a lot.
- Example: Binary Search.

```java
#include <iostream>
using namespace std;

// Binary Search function
int binarySearch(int arr[], int n, int target) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = (low + high) / 2;

        if (arr[mid] == target) {
            return mid; // Element found
        }
        else if (arr[mid] < target) {
            low = mid + 1; // Search in right half
        }
        else {
            high = mid - 1; // Search in left half
        }
    }
    return -1; // Element not found
}

int main() {
    int arr[] = {10, 20, 30, 40, 50, 60, 70};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 40;

    int result = binarySearch(arr, n, target);

    if (result != -1)
        cout << "Element found at index " << result << endl;
    else
        cout << "Element not found" << endl;

    return 0;
}
```

#### 3. O(n) – Linear Time
- Time grows directly proportional to input size.
- Example: Traversing an array.

```java
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Traversing the array (linear time operation)
    cout << "Array elements: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```

#### 4. O(n log n) – Linearithmic Time
- Better than quadratic but slower than linear.
- Example: Merge Sort, Quick Sort (average case).

```java
#include <iostream>
using namespace std;

// Function to merge two subarrays
void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    int L[n1], R[n2];

    // Copy data to temp arrays
    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int j = 0; j < n2; j++) R[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = left;

    // Merge the temp arrays back into arr[]
    while (i < n1 && j < n2) {
        if (L[i] <= R[j])
            arr[k++] = L[i++];
        else
            arr[k++] = R[j++];
    }

    // Copy remaining elements
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

// Merge Sort function
void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = (left + right) / 2;

        mergeSort(arr, left, mid);     // Sort left half
        mergeSort(arr, mid + 1, right); // Sort right half
        merge(arr, left, mid, right);   // Merge sorted halves
    }
}

int main() {
    int arr[] = {38, 27, 43, 3, 9, 82, 10};
    int n = sizeof(arr) / sizeof(arr[0]);

    mergeSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    return 0;
}
```

#### 5. O(n²) – Quadratic Time
- Time grows very fast with input size.
- Example: Nested loops (Bubble Sort, Insertion Sort).

```java
#include <iostream>
using namespace std;

int main() {
    int arr[] = {5, 1, 4, 2, 8};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Bubble Sort (quadratic time)
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap elements
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```


#### 6. O(2^n) – Exponential Time
- Extremely slow, doubles with each additional input.
- Example: Recursive Fibonacci without dynamic programming.

```java
#include <iostream>
using namespace std;

// Recursive Fibonacci (Exponential Time)
int fibonacci(int n) {
    if (n <= 1)
        return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n = 10;

    cout << "Fibonacci Series up to " << n << " terms: ";
    for (int i = 0; i < n; i++) {
        cout << fibonacci(i) << " ";
    }
    cout << endl;

    return 0;
}
```

#### 7. O(n!) – Factorial Time
- Worst growth rate.
- Example: Solving Traveling Salesman problem by brute force.

```java
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> nums = {1, 2, 3};

    cout << "All permutations: " << endl;

    // Generating all permutations using STL
    sort(nums.begin(), nums.end());
    do {
        for (int x : nums) {
            cout << x << " ";
        }
        cout << endl;
    } while (next_permutation(nums.begin(), nums.end()));

    return 0;
}
```

---

## 2. What is Space Complexity?
Space complexity measures how much memory (RAM) an algorithm needs while executing.
<br/>
<br/>

It includes:
1. Fixed Part – Memory for constants, program instructions.
2. Variable Part – Memory for variables, arrays, data structures.
3. Recursive Stack – Extra memory due to recursion calls.

### Common Space Complexities

#### 1. O(1) – Constant space
- No extra memory except a few variables.
- Example: Swapping two variables.

```java
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 20;

    // Swapping two variables using a temporary variable
    int temp = a;
    a = b;
    b = temp;

    cout << "After swapping: a = " << a << ", b = " << b << endl;

    return 0;
}
```

#### 2. O(n) – Linear space
- Memory grows with input size.
- Example: Storing an array, recursion depth = n.

```java
#include <iostream>
using namespace std;

int main() {
    int n = 5;
    int arr[n]; // Memory grows as n increases

    for (int i = 0; i < n; i++) {
        arr[i] = i + 1;
    }

    cout << "Array elements: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```

#### 3. O(log n) – Logarithmic space
- Memory grows slowly with input.
- Example: Recursive Binary Search.

```java
#include <iostream>
using namespace std;

// Recursive Binary Search
int binarySearch(int arr[], int low, int high, int target) {
    if (low > high)
        return -1; // Element not found

    int mid = (low + high) / 2;

    if (arr[mid] == target)
        return mid;
    else if (arr[mid] < target)
        return binarySearch(arr, mid + 1, high, target);
    else
        return binarySearch(arr, low, mid - 1, target);
}

int main() {
    int arr[] = {10, 20, 30, 40, 50, 60, 70};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 40;

    int result = binarySearch(arr, 0, n - 1, target);

    if (result != -1)
        cout << "Element found at index " << result << endl;
    else
        cout << "Element not found" << endl;

    return 0;
}
```

### 3. Why Do We Use Complexity Analysis?
- To predict performance before coding.
- To compare two algorithms solving the same problem.
- To avoid code that becomes too slow or memory-heavy for large inputs.

### 4. Quick Table
| Complexity | Name         | Example                     |
| ---------- | ------------ | --------------------------- |
| O(1)       | Constant     | Accessing array element     |
| O(log n)   | Logarithmic  | Binary Search               |
| O(n)       | Linear       | Array Traversal             |
| O(n log n) | Linearithmic | Merge Sort, Quick Sort      |
| O(n²)      | Quadratic    | Bubble Sort, Insertion Sort |
| O(2^n)     | Exponential  | Recursive Fibonacci         |
| O(n!)      | Factorial    | Traveling Salesman (brute)  |

