# JavaScript Fundamentals for Working with APIs

## 1. Variables and Data Types

In JavaScript, we use variables to store data. There are several ways to declare variables:

```javascript
let name = "John"; // Can be reassigned
const age = 30; // Cannot be reassigned
var city = "New York"; // Old way, try to avoid
```

Common data types include:

- Strings: `"Hello, World!"`
- Numbers: `42` or `3.14`
- Booleans: `true` or `false`
- Arrays: `[1, 2, 3, 4]`
- Objects: `{ name: "John", age: 30 }`

## 2. Functions

Functions are reusable blocks of code:

```javascript
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet("Alice")); // Outputs: Hello, Alice!
```

Arrow functions are a more concise way to write functions:

```javascript
const greet = (name) => `Hello, ${name}!`;
```

## 3. Objects and Arrays

Objects store data in key-value pairs:

```javascript
const person = {
  name: "John",
  age: 30,
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

console.log(person.name); // Outputs: John
person.greet(); // Outputs: Hello, my name is John
```

Arrays are ordered lists:

```javascript
const fruits = ["apple", "banana", "orange"];
console.log(fruits[0]); // Outputs: apple
fruits.push("grape"); // Adds "grape" to the end of the array
```

## 4. Array Methods

JavaScript has many useful array methods:

```javascript
const numbers = [1, 2, 3, 4, 5];

// map: transforms each element
const doubled = numbers.map(num => num * 2);
console.log(doubled); // Outputs: [2, 4, 6, 8, 10]

// filter: keeps elements that pass a test
const evens = numbers.filter(num => num % 2 === 0);
console.log(evens); // Outputs: [2, 4]

// forEach: performs an action for each element
numbers.forEach(num => console.log(num));
```

## 5. Promises and Asynchronous Programming

Promises represent the eventual completion (or failure) of an asynchronous operation:

```javascript
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data fetched successfully");
    }, 2000);
  });
};

fetchData()
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

## 6. Async/Await

Async/await is syntactic sugar for working with promises:

```javascript
const fetchData = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve("Data fetched"), 2000);
  });
};

const getData = async () => {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
};

getData();
```

## 7. Fetch API

The Fetch API is used for making HTTP requests:

```javascript
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

## 8. Working with APIs

When working with APIs, you often need to:

1. Make HTTP requests (usually GET or POST)
2. Handle the response (usually JSON)
3. Process the data
4. Handle errors

Here's a complete example:

```javascript
const API_KEY = 'your_api_key';
const BASE_URL = 'https://api.example.com';

const fetchPopularMovies = async () => {
  try {
    const response = await fetch(`${BASE_URL}/movies/popular?api_key=${API_KEY}`);
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    const data = await response.json();
    
    return data.results.map(movie => ({
      id: movie.id,
      title: movie.title,
      rating: movie.vote_average
    }));
  } catch (error) {
    console.error("Error fetching popular movies:", error);
    return [];
  }
};

// Usage
fetchPopularMovies()
  .then(movies => {
    movies.forEach(movie => {
      console.log(`${movie.title} - Rating: ${movie.rating}`);
    });
  })
  .catch(error => console.error(error));
```

This example brings together many of the concepts we've discussed:

- Asynchronous programming with `async/await`
- Error handling with try/catch
- Working with the Fetch API
- Processing data with array methods like `map`
- Using template literals for string interpolation

Understanding these fundamentals will give you a solid foundation for working with APIs in JavaScript.
