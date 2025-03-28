# Java Cheat Sheet

## 1. Basics

### 1.1 Install Java
Download from [java](https://www.oracle.com/java/technologies/downloads/?er=221886) and verify installation:
```java
java -version
```
### 1.2 Variables & Data Types
```java
int x = 10;         // Integer
float y = 3.14f;    // Float
double z = 3.1415;  // Double
char c = 'A';       // Char
boolean flag = true;   // Boolean
String str = "Hello"; // String
```

### 1.3 Conditional Statements
```java
if (x > 5) {
    // code to execute
} else if (x == 5) {
    // code to execute
} else {
    // code to execute
}
```

### 1.4 Loops
```java
 // Basic for loop
for (int i = 0; i < n; ++i) {
    // code to execute
}

// Enhanced for loop
for (int elem : array) {
    // code to execute
}

// While loop
int n = 0;
while (n < 5) {
    // code to execute
}

// do while loop
do {
    // code to execute
} while (condition);
```

### 1.5 String, Char, Integer Conversion
```java
// Convert int to string
String s = Integer.toString(num);
// Convert string to int
int num = Integer.parseInt(s);
// Convert char to string
String s = Character.toString(ch);
// Convert char array to string
String s = new String(charArr);
```

## 2. Functions
### 2.1 Function Without Parameters
```java
void greet() {
    System.out.println("Hello, world!");
}

greet();  // Output: Hello, world!
```
### 2.2 Function With Parameters
```java
void greet(String name) {
    System.out.println("Hello, " + name + "!");
}

greet("Shreyas");  // Output: Hello, Shreyas!
```
### 2.3 Function With Return Value
```java
int add(int a, int b) {
    return a + b;
}

int result = add(5, 3);  // Output: 8
System.out.println(result);
```
### 2.4 Function With Default Parameters
```java
void greet() {
    greet("Guest");
}

void greet(String name) {
    System.out.println("Hello, " + name + "!");
}

greet();           // Output: Hello, Guest!
greet("Shreyas");  // Output: Hello, Shreyas!
```
### 2.5 Lambda Functions
```java
// Lambda expression
Function<Integer, Integer> square = x -> x * x;
System.out.println(square.apply(5));  // Output: 25

BiFunction<Integer, Integer, Integer> add = (x, y) -> x + y;
System.out.println(add.apply(3, 4));  // Output: 7
```
### 2.6 Function With Multiple Parameters
```java
int add(int a, int b, int c) {
    return a + b + c;
}

System.out.println(add(1, 2, 3));  // Output: 6
```

## 3. Data Structures
### 3.1 Arrays
### 1. Single-Dimensional Arrays
#### 3.1.1 Declaration and Initialization
```java
// Declaration
int[] arr;  // Declares an array of integers

// Initialization
arr = new int[5];  // Creates an array of size 5 (default values: 0 for int)

// Declaration and initialization in one line
int[] arr = {1, 2, 3, 4, 5};  // Creates and initializes an array

// Default values for arrays
int[] intArr = new int[5];  // [0, 0, 0, 0, 0]
double[] doubleArr = new double[3];  // [0.0, 0.0, 0.0]
boolean[] boolArr = new boolean[2];  // [false, false]
String[] strArr = new String[3];  // [null, null, null]
```

#### 3.1.2 Accessing Elements & Iterating Over Arrays
```java
int[] arr = {10, 20, 30, 40, 50};

// Access elements using index
int firstElement = arr[0];  // 10
int thirdElement = arr[2];  // 30

// Modify elements
arr[1] = 100;  // arr becomes [10, 100, 30, 40, 50]

int length = arr.length;  // 5

// Using a for loop
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}

// Using an enhanced for loop (for-each loop)
for (int elem : arr) {
    System.out.println(elem);
}
```

#### 3.1.3 Common Array Operations
```java
// Importing Arrays
import java.util.Arrays;

// Sorting
int[] arr = {5, 3, 1, 4, 2};
Arrays.sort(arr);  // Sorts the array in ascending order: [1, 2, 3, 4, 5]

// Searching
int index = Arrays.binarySearch(arr, 3);  // Returns the index of 3 (2)

// Filling an Array
int[] arr = new int[5];
Arrays.fill(arr, 10);  // Fills the entire array with 10: [10, 10, 10, 10, 10]

// Copying an Array
int[] arr = {1, 2, 3, 4, 5};
int[] copiedArr = Arrays.copyOf(arr, arr.length);  // Copies the entire array
int[] partialCopy = Arrays.copyOf(arr, 3);  // Copies the first 3 elements: [1, 2, 3]

// Comparing Arrays
int[] arr1 = {1, 2, 3};
int[] arr2 = {1, 2, 3};
boolean isEqual = Arrays.equals(arr1, arr2);  // Returns true if arrays are equal

// Converting Array to String
String arrStr = Arrays.toString(arr);  // Returns "[1, 2, 3, 4, 5]"
```

#### 3.1.4 Stream Operations (Java 8+)
```java
import java.util.Arrays;

int[] arr = {1, 2, 3, 4, 5};

// Sum of all elements
int sum = Arrays.stream(arr).sum();

// Average of all elements
double average = Arrays.stream(arr).average().orElse(0);

// Filter elements greater than 2
int[] filteredArr = Arrays.stream(arr).filter(x -> x > 2).toArray();
```

## 2. Multi-Dimensional Arrays
#### 3.1.5 Declaration and Initialization
```java
// 2D array (matrix)
int[][] matrix = new int[3][3];  // 3x3 matrix (default values: 0)

// Initialize with values
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Accessing Elements
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

int element = matrix[1][2];  // 6 (row 1, column 2)
```

#### 3.1.6 Iterating Over Multi-Dimensional Arrays
```java
// Using nested for loops
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}

// Using enhanced for loops
for (int[] row : matrix) {
    for (int elem : row) {
        System.out.print(elem + " ");
    }
    System.out.println();
}
```

#### 3.1.7 Common Operations
```java
// Sorting Rows
for (int[] row : matrix) {
    Arrays.sort(row);  // Sorts each row individually
}

// Copying a 2D Array
int[][] copiedMatrix = Arrays.copyOf(matrix, matrix.length);
for (int i = 0; i < matrix.length; i++) {
    copiedMatrix[i] = Arrays.copyOf(matrix[i], matrix[i].length);
}

// Converting 2D Array to String
String matrixStr = Arrays.deepToString(matrix);  // Returns "[[1, 2, 3], [4, 5, 6], [7, 8, 9]]"
```

### 3.2 Strings
#### 3.2.1 String Basics
- **Definition:** A sequence of characters. Strings are immutable in Java.
- **Library:** `java.lang.String` (automatically imported)
```java
// Create a string
String str = "Hello, World!";

// Get the length of the string
int length = str.length();  // Returns 13

// Access characters
char firstChar = str.charAt(0);  // Returns 'H'

// Substring
String sub = str.substring(0, 5);  // Returns "Hello"

// Concatenation
String newStr = str + " How are you?";  // Returns "Hello, World! How are you?"

// Check if a string contains a substring
boolean contains = str.contains("World");  // Returns true

// Check if a string starts/ends with a substring
boolean startsWith = str.startsWith("Hello");  // Returns true
boolean endsWith = str.endsWith("!");  // Returns true

// Replace characters or substrings
String replacedStr = str.replace("World", "Java");  // Returns "Hello, Java!"

// Convert to lowercase/uppercase
String lowerCaseStr = str.toLowerCase();  // Returns "hello, world!"
String upperCaseStr = str.toUpperCase();  // Returns "HELLO, WORLD!"

// Trim leading and trailing whitespace
String trimmedStr = "  Hello  ".trim();  // Returns "Hello"

// Split a string into an array
String[] parts = str.split(", ");  // Returns ["Hello", "World!"]

// Check if two strings are equal
boolean isEqual = str.equals("Hello, World!");  // Returns true

// Check if two strings are equal (case-insensitive)
boolean isEqualIgnoreCase = str.equalsIgnoreCase("hello, world!");  // Returns true

// Convert string to char array
char[] charArray = str.toCharArray();  // Returns ['H', 'e', 'l', 'l', 'o', ',', ' ', 'W', 'o', 'r', 'l', 'd', '!']

// Convert other data types to string
String intStr = Integer.toString(123);  // Returns "123"
String doubleStr = Double.toString(3.14);  // Returns "3.14"
```

#### 3.2.2 StringBuilder and StringBuffer
- **Definition:** Mutable sequences of characters. `StringBuilder` is not thread-safe, while `StringBuffer` is thread-safe.
- **Library:** `java.lang.StringBuilder`, `java.lang.StringBuffer`
```java
// Create a StringBuilder
StringBuilder sb = new StringBuilder("Hello");

// Append to the string
sb.append(", World!");  // sb becomes "Hello, World!"

// Insert into the string
sb.insert(5, " Java");  // sb becomes "Hello Java, World!"

// Delete characters
sb.delete(5, 10);  // sb becomes "Hello, World!"

// Replace characters
sb.replace(7, 12, "Java");  // sb becomes "Hello, Java!"

// Reverse the string
sb.reverse();  // sb becomes "!avaJ ,olleH"

// Convert to string
String result = sb.toString();  // Returns "!avaJ ,olleH"

// Get the length of the string
int length = sb.length();  // Returns 13

// Get the capacity of the StringBuilder
int capacity = sb.capacity();  // Returns the current capacity

// Set the length of the string
sb.setLength(5);  // sb becomes "!avaJ"

// Ensure minimum capacity
sb.ensureCapacity(20);  // Ensures the capacity is at least 20
```

#### 3.2.3 String Formatting
- **Definition:** Formatting strings using placeholders.
- **Library:** `java.lang.String`
```java
// Format a string
String formattedStr = String.format("Hello, %s! You have %d messages.", "Alice", 5);  // Returns "Hello, Alice! You have 5 messages."

// Format numbers
String numberStr = String.format("Value: %.2f", 3.14159);  // Returns "Value: 3.14"

// Format dates
import java.util.Date;
Date now = new Date();
String dateStr = String.format("Today is %tF", now);  // Returns "Today is 2023-10-05"
```

#### 3.2.4 Regular Expressions
- **Definition:** Pattern matching and manipulation using regular expressions.
- **Library:** `java.util.regex`
```java 
import java.util.regex.*;

// Check if a string matches a pattern
boolean matches = "Hello, World!".matches("Hello.*");  // Returns true

// Replace all occurrences of a pattern
String replacedStr = "Hello, World!".replaceAll("o", "0");  // Returns "Hell0, W0rld!"

// Split a string using a pattern
String[] parts = "Hello, World!".split("\\W+");  // Returns ["Hello", "World"]

// Find all matches of a pattern
Pattern pattern = Pattern.compile("\\d+");
Matcher matcher = pattern.matcher("There are 123 apples and 456 oranges.");
while (matcher.find()) {
    System.out.println(matcher.group());  // Prints "123" and "456"
}
```

### 3.3 Maps
#### 3.3.1 `HashMap`
- **Definition:** A hash table-based implementation of the `Map` interface. It stores key-value pairs and allows `null` keys and values.
- **Library:** `java.util.HashMap`
```java
// Create a HashMap
HashMap<Integer, String> map = new HashMap<>();

// Insert elements
map.put(1, "one");
map.put(2, "two");

// Access elements
String value = map.get(1);  // Returns "one"

// Check if a key exists
boolean containsKey = map.containsKey(1);  // Returns true

// Check if a value exists
boolean containsValue = map.containsValue("one");  // Returns true

// Remove an element
map.remove(1);  // Removes key=1

// Get the size of the map
int size = map.size();  // Returns the number of key-value pairs

// Check if the map is empty
boolean isEmpty = map.isEmpty();  // Returns false

// Iterate over the map
for (Map.Entry<Integer, String> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}

// Clear the map
map.clear();  // Removes all elements
```

#### 3.3.2 `TreeMap`
- **Definition:** A Red-Black tree-based implementation of the `Map` interface. It stores key-value pairs in sorted order.
- **Library:** `java.util.TreeMap`
```java
// Create a TreeMap
TreeMap<Integer, String> treeMap = new TreeMap<>();

// Insert elements
treeMap.put(1, "one");
treeMap.put(2, "two");

// Access elements
String value = treeMap.get(1);  // Returns "one"

// Get the first key
int firstKey = treeMap.firstKey();  // Returns 1

// Get the last key
int lastKey = treeMap.lastKey();  // Returns 2

// Get a submap
SortedMap<Integer, String> subMap = treeMap.subMap(1, 3);  // Returns entries with keys between 1 and 2

// Iterate over the map
for (Map.Entry<Integer, String> entry : treeMap.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}
```

#### 3.3.3 `LinkedHashMap`
- **Definition:** A hash table and linked list implementation of the `Map` interface. It maintains insertion order.
- **Library:** `java.util.LinkedHashMap`
```java
// Create a LinkedHashMap
LinkedHashMap<Integer, String> linkedMap = new LinkedHashMap<>();

// Insert elements
linkedMap.put(1, "one");
linkedMap.put(2, "two");

// Access elements
String value = linkedMap.get(1);  // Returns "one"

// Iterate over the map
for (Map.Entry<Integer, String> entry : linkedMap.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}
```

### 3.4 Sets
#### 3.4.1 `HashSet`
- **Definition:** A hash table-based implementation of the `Set` interface. It stores unique elements and allows `null`.
- **Library:** `java.util.HashSet`
```java
// Create a HashSet
HashSet<Integer> set = new HashSet<>();

// Add elements
set.add(1);
set.add(2);

// Check if an element exists
boolean contains = set.contains(1);  // Returns true

// Remove an element
set.remove(1);  // Removes element 1

// Get the size of the set
int size = set.size();  // Returns the number of elements

// Check if the set is empty
boolean isEmpty = set.isEmpty();  // Returns false

// Iterate over the set
for (int elem : set) {
    System.out.println(elem);
}

// Clear the set
set.clear();  // Removes all elements
```

#### 3.4.2 `TreeSet`
- **Definition:** A Red-Black tree-based implementation of the `Set` interface. It stores unique elements in sorted order.
- **Library:** `java.util.TreeSet`
```java
// Create a TreeSet
TreeSet<Integer> treeSet = new TreeSet<>();

// Add elements
treeSet.add(1);
treeSet.add(2);

// Get the first element
int first = treeSet.first();  // Returns 1

// Get the last element
int last = treeSet.last();  // Returns 2

// Get a subset
SortedSet<Integer> subSet = treeSet.subSet(1, 3);  // Returns elements between 1 and 2

// Iterate over the set
for (int elem : treeSet) {
    System.out.println(elem);
}
```

#### 3.4.3 `LinkedHashSet`
- **Definition:** A hash table and linked list implementation of the `Set` interface. It maintains insertion order.
- **Library:** `java.util.LinkedHashSet`
```java
// Create a LinkedHashSet
LinkedHashSet<Integer> linkedSet = new LinkedHashSet<>();

// Add elements
linkedSet.add(1);
linkedSet.add(2);

// Iterate over the set
for (int elem : linkedSet) {
    System.out.println(elem);
}
```

### 3.5 Lists
#### 3.5.1 `ArrayList`
- **Definition:** A resizable array implementation of the `List` interface.
- **Library:** `java.util.ArrayList`
```java
// Create an ArrayList
ArrayList<Integer> list = new ArrayList<>();

// Add elements
list.add(1);
list.add(2);

// Access elements
int elem = list.get(0);  // Returns 1

// Modify elements
list.set(0, 10);  // Sets the first element to 10

// Remove elements
list.remove(0);  // Removes the first element

// Get the size of the list
int size = list.size();  // Returns the number of elements

// Check if the list is empty
boolean isEmpty = list.isEmpty();  // Returns false

// Iterate over the list
for (int elem : list) {
    System.out.println(elem);
}

// Clear the list
list.clear();  // Removes all elements
```

#### 3.5.2 `LinkedList`
- **Definition:** A doubly-linked list implementation of the `List` interface.
- **Library:** `java.util.LinkedList`
```java
// Create a LinkedList
LinkedList<Integer> linkedList = new LinkedList<>();

// Add elements
linkedList.add(1);
linkedList.add(2);

// Add elements at the beginning
linkedList.addFirst(0);

// Add elements at the end
linkedList.addLast(3);

// Remove elements from the beginning
linkedList.removeFirst();

// Remove elements from the end
linkedList.removeLast();

// Iterate over the list
for (int elem : linkedList) {
    System.out.println(elem);
}
```

### 3.6 Queues
#### 3.6.1 `PriorityQueue`
- **Definition:** A priority heap-based implementation of the `Queue` interface.
- **Library:** `java.util.PriorityQueue`
```java
// Create a PriorityQueue
PriorityQueue<Integer> pq = new PriorityQueue<>();

// Add elements
pq.add(3);
pq.add(1);
pq.add(2);

// Access the head of the queue
int head = pq.peek();  // Returns 1

// Remove the head of the queue
int removed = pq.poll();  // Removes and returns 1

// Iterate over the queue
for (int elem : pq) {
    System.out.println(elem);
}
```

#### 3.6.2 `ArrayDeque`
- **Definition:** A resizable array implementation of the `Deque` interface.
- **Library:** `java.util.ArrayDeque`
```java
// Create an ArrayDeque
ArrayDeque<Integer> deque = new ArrayDeque<>();

// Add elements at the beginning
deque.addFirst(1);

// Add elements at the end
deque.addLast(2);

// Remove elements from the beginning
int first = deque.removeFirst();

// Remove elements from the end
int last = deque.removeLast();

// Iterate over the deque
for (int elem : deque) {
    System.out.println(elem);
}
```

### 3.7 Stacks
#### 3.7.1 `Stack`
- **Definition:** A last-in-first-out (LIFO) stack of objects.
- **Library:** `java.util.Stack`
```java
// Create a Stack
Stack<Integer> stack = new Stack<>();

// Push elements
stack.push(1);
stack.push(2);

// Access the top element
int top = stack.peek();  // Returns 2

// Remove the top element
int popped = stack.pop();  // Removes and returns 2

// Check if the stack is empty
boolean isEmpty = stack.isEmpty();  // Returns false

// Iterate over the stack
for (int elem : stack) {
    System.out.println(elem);
}
```

## 5. Object-Oriented Programming (OOP)

### 5.1 Classes and Objects
```java
class Person {
    String name;
    int age;

    Person(String n, int a) {
        name = n;
        age = a;
    }
    
    void greet() {
        System.out.println("Hello, my name is " + name + "!");
    }
}

Person p = new Person("Shreyas", 25);
p.greet();
```

### 5.2 Encapsulation 
```java
class BankAccount {
    private double balance;

    BankAccount(double initialBalance) {
        balance = (initialBalance >= 0) ? initialBalance : 0;
    }

    void deposit(double amount) { balance += amount; }
    void withdraw(double amount) { if (amount <= balance) balance -= amount; }
    double getBalance() { return balance; }
}

BankAccount account = new BankAccount(1000);
account.deposit(500);
account.withdraw(300);
System.out.println("Balance: $" + account.getBalance());  // Output: Balance: $1200
```
### 5.3 Inheritance 
```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks!");
    }
}

Dog myDog = new Dog();
myDog.eat();  // Inherited from Animal class
myDog.bark(); // Defined in Dog class
```
### 5.4 Polymorphism
**(i). Method Overloading**
```java
class Math {
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
}

Math obj = new Math();
System.out.println(obj.add(5, 3));     // Output: 8
System.out.println(obj.add(2.5, 1.5)); // Output: 4.0
```

**(ii). Method Overriding**
```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

Animal animal = new Dog();
animal.makeSound();  // Output: Dog barks (Polymorphism at runtime)
```

### 5.5 Abstraction
```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a Circle");
    }
}

class Rectangle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a Rectangle");
    }
}

Shape shape1 = new Circle();
Shape shape2 = new Rectangle();

shape1.draw();  // Output: Drawing a Circle
shape2.draw();  // Output: Drawing a Rectangle
```

### 5.6 Constructor 
```java
class Car {
    String brand;
    int speed;

    Car(String b, int s) {
        brand = b;
        speed = s;
        System.out.println("Car object created!");
    }

    void display() {
        System.out.println("Brand: " + brand + ", Speed: " + speed + " km/h");
    }
}

Car myCar = new Car("Toyota", 120);  // Constructor is automatically called
myCar.display();  
```

### 5.7 Destructor 
```java
class Car {
    Car() {
        System.out.println("Car is created!");
    }
    
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Car is destroyed!");
    }
}

Car myCar = new Car();  // Constructor is called automatically
myCar = null;  // Object is eligible for garbage collection
System.gc();  // Suggests garbage collection (not guaranteed)
```

## 6. Exception Handling
### 6.1 Try-Catch-Finally
```java
try {
    int result = 10 / 0; // Throws ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage()); // Error: / by zero
} finally {
    System.out.println("This always executes.");
}
```

### 6.2 Custom Exceptions
```java
class InvalidAgeException extends Exception {
    InvalidAgeException(String message) {
        super(message);
    }
}

void validateAge(int age) throws InvalidAgeException {
    if (age < 18) throw new InvalidAgeException("Age must be ≥ 18");
}

try {
    validateAge(15);
} catch (InvalidAgeException e) {
    System.out.println(e.getMessage()); // Age must be ≥ 18
}
```

## 7. File I/O (Basic Operations)
### 7.1 Read a File
```java
import java.io.*;

try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### 7.2 Write to a File
```java
try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
    bw.write("Hello, Java!");
} catch (IOException e) {
    e.printStackTrace();
}
```

### 7.3 List Files in a Directory
```java
File dir = new File("/path/to/dir");
for (File file : dir.listFiles()) {
    System.out.println(file.getName());
}
```

## 8. Generics
### 8.1 Generic Class
```java
class Box<T> {
    private T content;
    void setContent(T content) { this.content = content; }
    T getContent() { return content; }
}

Box<String> stringBox = new Box<>();
stringBox.setContent("Hello");
System.out.println(stringBox.getContent()); // Hello
```

### 8.2 Generic Methods
```java
<T> void printArray(T[] array) {
    for (T item : array) {
        System.out.println(item);
    }
}

printArray(new Integer[]{1, 2, 3}); // Works with any type
```

### 8.3  Bounded Generics (`extends`)
```java
class NumberBox<T extends Number> { // Only accepts Number types
    private T number;
    // ...
}

NumberBox<Integer> intBox = new NumberBox<>(); // Right way
NumberBox<String> strBox = new NumberBox<>(); // (String Input Won't Be Accepted) (Compile error)
```

## 9. Stream API (Java 8+)
### 9.1 Filter, Map, Reduce
```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);

// Filter even numbers, square them, then sum
int sum = nums.stream()
              .filter(n -> n % 2 == 0)
              .map(n -> n * n)
              .reduce(0, Integer::sum);

System.out.println(sum); // 20 (4 + 16)
```

### 9.2 Collect to List/Set
```java
List<Integer> evenNumbers = nums.stream()
                                .filter(n -> n % 2 == 0)
                                .collect(Collectors.toList());
```

## 9.3 Parallel Streams
```java
long count = nums.parallelStream() // Faster for large datasets
                 .filter(n -> n > 2)
                 .count();
```
