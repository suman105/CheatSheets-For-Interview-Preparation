# <img src="https://upload.wikimedia.org/wikipedia/commons/6/6a/JavaScript-logo.png" alt="JavaScript Logo" width="25" height="25">  JavaScript Cheat Sheet  


## 1. Basics

### 1.1 Variables
```js
// Declare variables
let x = 10;         // Block-scoped variable
const y = 20;       // Block-scoped constant
var z = 30;         // Function-scoped variable (avoid using in modern JS)

// Reassigning values
x = 15;             // Valid
// y = 25;          // Error: Cannot reassign a constant
z = 35;             // Valid
```

### 1.2 Data Types
```js
// Primitive Data Types
let num = 42;               // Number
let str = "Hello";          // String
let bool = true;            // Boolean
let nothing = null;         // Null
let notDefined = undefined; // Undefined
let sym = Symbol("id");     // Symbol (unique identifier)

// Non-Primitive Data Types
let obj = { name: "John", age: 30 }; // Object
let arr = [1, 2, 3];                 // Array
let func = function() {};             // Function
```

### 1.3 Type Conversion
```js
// Convert to String
let numToString = String(123); // "123"
let boolToString = String(true); // "true"

// Convert to Number
let strToNum = Number("123"); // 123
let boolToNum = Number(true); // 1

// Convert to Boolean
let numToBool = Boolean(1); // true
let strToBool = Boolean(""); // false
```

### 1.5 Conditional Statements
```js
// If-Else
if (x > 10) {
    console.log("x is greater than 10");
} else if (x === 10) {
    console.log("x is 10");
} else {
    console.log("x is less than 10");
}

// Ternary Operator
let result = x > 10 ? "Greater" : "Less or Equal";
```

### 1.6 Loops
```js
// For Loop
for (let i = 0; i < 5; i++) {
    console.log(i);
}

// While Loop
let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}

// Do-While Loop
let j = 0;
do {
    console.log(j);
    j++;
} while (j < 5);

// For-Of Loop (Arrays, Strings)
let arr = [1, 2, 3];
for (let val of arr) {
    console.log(val);
}

// For-In Loop (Objects)
let obj = { a: 1, b: 2 };
for (let key in obj) {
    console.log(key, obj[key]);
}
```

## 2. Functions

### 2.1 Function Declaration
```js
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet("John")); // Hello, John!
```

### 2.2 Function Expression
```js
const greet = function(name) {
    return `Hello, ${name}!`;
};
console.log(greet("Jane")); // Hello, Jane!
```

### 2.3 Arrow Functions
```js
const greet = (name) => `Hello, ${name}!`;
console.log(greet("Alice")); // Hello, Alice!
```

### 2.4 Default Parameters
```js
function greet(name = "Guest") {
    return `Hello, ${name}!`;
}
console.log(greet()); // Hello, Guest!
```

### 2.5 Rest Parameters
```js
function sum(...numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
}
console.log(sum(1, 2, 3)); // 6
```

### 2.6 Higher-Order Functions
```js
function createGreeting(greeting) {
    return function(name) {
        return `${greeting}, ${name}!`;
    };
}
const sayHello = createGreeting("Hello");
console.log(sayHello("John")); // Hello, John!
```

## 3. Arrays

### 3.1 Array Methods
```js
let arr = [1, 2, 3];
let emptyArr = [];   // Empty array

// Add/Remove Elements
arr.push(4);        // [1, 2, 3, 4]
arr.pop();          // [1, 2, 3]
arr.unshift(0);     // [0, 1, 2, 3]
arr.shift();        // [1, 2, 3]

// Iterate Over Array
arr.forEach((val) => console.log(val));

// Map (Transform Array)
let doubled = arr.map((val) => val * 2); // [2, 4, 6]

// Filter (Select Elements)
let evens = arr.filter((val) => val % 2 === 0); // [2]

// Reduce (Accumulate Values)
let sum = arr.reduce((acc, val) => acc + val, 0); // 6

// Find (First Match)
let found = arr.find((val) => val > 1); // 2

// Sort
let sorted = arr.sort((a, b) => b - a); // [3, 2, 1]

//Index
let index = arr.findIndex((val) => val === 2); // Index of 2: 1
```
### 3.2 Searching and Sorting 
```js
let found = list.find(x => x > 1); // 99
let index = list.findIndex(x => x === 99); // 1
let sorted = list.sort((a, b) => b - a); // [99, 3, 1]
let reversed = list.reverse(); // [1, 3, 99]
```

### 3.3 Other Useful Methods
```js
let sliced = arr.slice(1, 3); // Subarray: [2, 3]
arr.splice(1, 1, 99); // Replace 1 element at index 1: [1, 99, 3]
let includes = arr.includes(2); // Check if array contains 2: true
let merged = list.concat([4, 5]); // [1, 3, 99, 4, 5]
let joined = arr.join("-"); // Join elements: "1-99-3"
```

### 3.4 Spread and Rest with Arrays
```js
// Spread Operator
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

// Rest Operator
let [first, ...rest] = arr1;
console.log(first); // 1
console.log(rest);  // [2, 3]
```

## 4. Sets
### 4.1 Definition and Initialization
```js
let set = new Set([1, 2, 3, 3]); // Set(3) {1, 2, 3} (duplicates removed)
```

### 4.2 Set Methods
```js
// Adding/Removing Elements
set.add(4); // Add element: Set(4) {1, 2, 3, 4}
set.delete(2); // Remove element: Set(3) {1, 3, 4}
set.clear(); // Clear all elements: Set(0) {}

// Checking Elements
set.has(3); // Check if element exists: true

// Iterating Over Sets
set.forEach((val) => console.log(val)); // Iterate

// Other Useful Methods
let size = set.size; // Number of elements: 3
```
### 4.3 Multi-Sets (Nested Sets)
```js
let multiSet = new Set();
multiSet.add(new Set([1, 2, 3]));
multiSet.add(new Set([4, 5, 6]));

for (let set of multiSet) {
    console.log([...set]); // [1, 2, 3], [4, 5, 6]
}
``` 

## 5. Maps
### 5.1 Definition and Initialization
```js
let map = new Map([["name", "John"], ["age", 30]]); // Map(2) {"name" => "John", "age" => 30}
```

### 5.2 Map Methods
```js
// Adding/Removing Elements
map.set("city", "New York"); // Add key-value pair
map.delete("age"); // Remove key-value pair
map.clear(); // Clear all key-value pairs

// Checking Elements
map.has("name"); // Check if key exists: true

// Iterating Over Maps
map.forEach((val, key) => console.log(key, val)); // Iterate
```

### 5.3 Other Useful Methods
```js
let size = map.size; // Number of key-value pairs: 2
let keys = map.keys(); // Iterator of keys
let values = map.values(); // Iterator of values
let entries = map.entries(); // Iterator of key-value pairs
```

### 5.4 Multi-Maps (Nested Maps)
```js
let multiMap = new Map();
multiMap.set("user1", new Map([["name", "John"], ["age", 30]]));
multiMap.set("user2", new Map([["name", "Jane"], ["age", 25]]));

console.log(multiMap.get("user1").get("name")); // John
```

## 6. Objects
### 6.1 Object Methods
```js
let obj = { name: "John", age: 30 };

// Access Properties
console.log(obj.name); // John
console.log(obj["age"]); // 30

// Add/Remove Properties
obj.city = "New York";
delete obj.age;

// Iterate Over Object
for (let key in obj) {
    console.log(key, obj[key]);
}

// Object.keys(), Object.values(), Object.entries()
let keys = Object.keys(obj); // ["name", "city"]
let values = Object.values(obj); // ["John", "New York"]
let entries = Object.entries(obj); // [["name", "John"], ["city", "New York"]]
```

### 6.2 Spread and Rest with Objects
```js
// Spread Operator
let obj1 = { a: 1, b: 2 };
let obj2 = { ...obj1, c: 3 }; // { a: 1, b: 2, c: 3 }

// Rest Operator
let { a, ...rest } = obj1;
console.log(a);    // 1
console.log(rest); // { b: 2 }
```

## 7. Classes and OOP
### 7.1 Class Declaration
```js
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }
}

let person = new Person("John", 30);
person.greet(); // Hello, my name is John
```

### 7.2 Inheritance
```js
class Student extends Person {
    constructor(name, age, grade) {
        super(name, age);
        this.grade = grade;
    }

    study() {
        console.log(`${this.name} is studying`);
    }
}

let student = new Student("Jane", 20, "A");
student.greet(); // Hello, my name is Jane
student.study(); // Jane is studying
```

### 7.3 Getters and Setters
```js
class Circle {
    constructor(radius) {
        this.radius = radius;
    }

    get diameter() {
        return this.radius * 2;
    }

    set diameter(value) {
        this.radius = value / 2;
    }
}

let circle = new Circle(5);
console.log(circle.diameter); // 10
circle.diameter = 14;
console.log(circle.radius); // 7
```

### 7.4 Abstraction
```js
class Car {
    // Private field (ES2022)
    #mileage;

    constructor(make, model) {
        this.make = make;
        this.model = model;
        this.#mileage = 0; // Private property
    }

    drive(distance) {
        this.#mileage += distance;
        console.log(`Driving ${distance} km...`);
    }

    getMileage() {
        return this.#mileage;
    }
}

let car = new Car("Toyota", "Corolla");
car.drive(100);
console.log(car.getMileage()); // 100
// console.log(car.#mileage); // Error: Private field cannot be accessed outside the class
```

### 7.5 Encapsulation
```js
class BankAccount {
    // Private field (ES2022)
    #balance;

    constructor(initialBalance) {
        this.#balance = initialBalance;
    }

    deposit(amount) {
        if (amount > 0) {
            this.#balance += amount;
            console.log(`Deposited ${amount}. New balance: ${this.#balance}`);
        }
    }

    withdraw(amount) {
        if (amount > 0 && amount <= this.#balance) {
            this.#balance -= amount;
            console.log(`Withdrew ${amount}. New balance: ${this.#balance}`);
        } else {
            console.log("Insufficient funds");
        }
    }

    getBalance() {
        return this.#balance;
    }
}

let account = new BankAccount(1000);
account.deposit(500); // Deposited 500. New balance: 1500
account.withdraw(200); // Withdrew 200. New balance: 1300
console.log(account.getBalance()); // 1300
// console.log(account.#balance); // Error: Private field cannot be accessed outside the class
```

### 7.6 Polymorphism
**(i). Overriding (Run-time Polymorphism):**
```js
class Animal {
    makeSound() {
        console.log("Animal makes a sound");
    }
}

class Dog extends Animal {
    makeSound() {
        console.log("Dog barks");
    }
}

class Cat extends Animal {
    makeSound() {
        console.log("Cat meows");
    }
}

let animal = new Animal();
let dog = new Dog();
let cat = new Cat();

animal.makeSound(); // Animal makes a sound
dog.makeSound();    // Dog barks
cat.makeSound();    // Cat meows
```
**(ii). Overloading (Compile-time Polymorphism):**
```js
class MathOperations {
    add(a, b, c) {
        if (c !== undefined) {
            return a + b + c;
        } else {
            return a + b;
        }
    }
}

let math = new MathOperations();
console.log(math.add(2, 3));       // 5
console.log(math.add(2, 3, 4));    // 9
```

## 8. Promises and Async/Await
### 8.1 Promises
```sh
let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("Done!"), 1000);
});

promise.then((result) => console.log(result)); // Done!
```

### 8.2 Async/Await
```js
async function fetchData() {
    let response = await fetch("https://api.example.com/data");
    let data = await response.json();
    console.log(data);
}

fetchData();
```

## 9. DOM Manipulation
### 9.1 Selecting Elements
```js
let element = document.getElementById("myId");
let elements = document.querySelectorAll(".myClass");
```

### 9.2 Modifying Elements
```js
element.textContent = "New Text";
element.innerHTML = "<strong>Bold Text</strong>";
element.style.color = "red";
```

### 9.3 Event Listeners
```js
element.addEventListener("click", () => {
    console.log("Element clicked!");
});
```

## 10. Error Handling
### 10.1 Try-Catch
```js
try {
    throw new Error("Something went wrong");
} catch (error) {
    console.log(error.message); // Something went wrong
}
```

### 10.2 Finally
```js
try {
    // Code that may throw an error
} catch (error) {
    console.log(error);
} finally {
    console.log("This will always run");
}
```

## 11. Modules
### 11.1 Exporting
```sh
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;
```

### 11.2 Importing
```js
// main.js
import { add, subtract } from "./math.js";
console.log(add(2, 3)); // 5
```

## 12. ES6+ Features
### 12.1 Template Literals
```js
let name = "John";
console.log(`Hello, ${name}!`); // Hello, John!
```

### 12.2 Destructuring
```js
let [a, b] = [1, 2];
let { x, y } = { x: 10, y: 20 };
```

### 12.3 Optional Chaining
```js
let user = { name: "John" };
console.log(user.address?.city); // undefined (no error)
```

### 12.4 Nullish Coalescing
```js
let value = null;
console.log(value ?? "Default"); // Default
```

## 13. JSON
### 13.1 JSON.stringify
```js
let obj = { name: "John", age: 30 };
let json = JSON.stringify(obj); // {"name":"John","age":30}
```

### 13.2 JSON.parse
```js
let obj = JSON.parse(json); // { name: "John", age: 30 }
```

## 14. Regular Expressions
### 14.1 Basic Usage
```js
let regex = /hello/;
console.log(regex.test("hello world")); // true
```

### 14.2 Flags
```js
let regex = /hello/i; // Case-insensitive
console.log(regex.test("Hello world")); // true
```

### 14.3 Matching and Replacing
```js
let str = "Hello world";
console.log(str.match(/hello/i)); // ["Hello"]
console.log(str.replace(/world/, "JavaScript")); // Hello JavaScript
```

## 15. Browser APIs
### 15.1 Fetch API
```js
fetch("https://api.example.com/data")
    .then((response) => response.json())
    .then((data) => console.log(data));
```

### 15.2 Local Storage
```js
localStorage.setItem("name", "John");
console.log(localStorage.getItem("name")); // John
localStorage.removeItem("name");
```

## 15. Debugging
### 15.1 Console Methods
```js
console.log("Log");
console.warn("Warning");
console.error("Error");
console.table([{ name: "John", age: 30 }]);
```

## 16. Some Tips 
- Use `let` and `const` instead of `var`.
  
- Always use `===` for equality checks.

- Use arrow functions for concise syntax.

- Avoid global variables.

- Use template literals for string concatenation.

- Always handle errors using `try-catch`.
