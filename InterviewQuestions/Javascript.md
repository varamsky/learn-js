1. List the datatypes available in JS?
	- There are 8 datatypes in JS:-
	1. String
	2. Number (includes integers, floats, `Infinity`, `NaN`)
	3. Bigint
	4. Boolean
	5. Undefined
	6. Null (note: even though `typeof null === 'object'`, null is a still primitive value)
	7. Symbol
	8. Object

2. map vs object

| Map | Object |
|---|---|
| A Map does not contain any keys by default. It only contains what is explicitly put into it. | An Object has a prototype, so it contains default keys that could collide with your own keys if you're not careful. Note: This can be bypassed by using ```Object.create(null)``` |
| The keys in Map are ordered in a simple, straightforward way: A Map object iterates entries, keys, and values in the order of entry insertion. | Although the keys of an ordinary Object are ordered now, this was not always the case, and the order is complex. As a result, it's best not to rely on property order. |
| A Map is an iterable, so it can be directly iterated. | An Object is not directly iterable. |
| Keys in a map can be of any datatype. | Keys in an object must be a string or Symbol(anything else if used is coerced into a string). |

3. Major EcmaScript versions
	- `ES3` -> This is the version of ECMAScript that most browsers support today.
	- `ES4` -> Never released
	- `ES5` -> 
		- strict mode -> It enforces stricter parsing and error handling on the code at runtime.
		- JSON support
		- Improved array manipulation
	- `ES6` -> 
		- let and const
		- Arrow functions
		- Template literals
		- Classes
		- Template strings
		- Destructuring
		- Default Parameters + Rest Parameters + Spread Operator
		- Symbols
		- Promises
		- Enhanced object literals
		- Generators and so on..
		- ```javascript
			// Example of let and const in ES6
			let name = "John Doe";
			const age = 30;

			// Example of arrow function in ES6
			let add = (a, b) => a + b;
			console.log(add(1, 2)); // Output: 3

			// Example of template literals in ES6
			let message = `Hello, ${name}!`;
			console.log(message); // Output: "Hello, John Doe!"

			// Example of class in ES6
			class Person {
    			constructor(name, age) {
        			this.name = name;
        			this.age = age;
    			}

    			greet() {
        			return `Hello, ${this.name}!`;
    			}
			}
			let john = new Person("John Doe", 30);
			console.log(john.greet()); // Output: "Hello, John Doe!"

			// Example of default parameters in ES6
			function f(x, y=12) {
  				// y is 12 if not passed (or passed as undefined)
  				return x + y;
			}
			f(3) == 15

			// Example of Rest Parameters in ES6
			function f(x, ...y) {
  				// y is an Array
  				return x * y.length;
			}
			f(3, "hello", true) == 6

			// Example of Spread operator in ES6
			function f(x, y, z) {
  				return x + y + z;
			}
			// Pass each elem of array as argument
			f(...[1,2,3]) == 6
			```
	- `ES7` -> EcmaScript after ES6 have been named by the year they are released in like `ECMAScript 2016(ES7)`

4. What are Polyfills in JS?
	- Polyfills are snippets of code that can add missing features to older browsers. They are often used to implement new JavaScript features or to provide support for older versions of APIs.
	- For example, the `Array.prototype.includes()` method was added to JavaScript in `ES7`. However, older browsers do not support this method. A polyfill can be used to add this method to older browsers, so that developers can use it in their code.
	- Example of a polyfill for `Array`:-
		- ```javascript
			let arr = [1,2,3];

			Array.prototype.myTrue = function myTrue() {
				// any implementation we might want
    			return true;
			}

			// we can also add the property to Array later as shown here
			// Array.prototype.myTrue = myTrue;

			console.log(arr.myTrue()); // true
			```

5. `require` vs `import`

| require | import |
| --- | --- |
| The `require()` function can be called from anywhere within the program | `import()` cannot be called conditionally. It always runs at the beginning of the file. |

6. What are closures in JS?
	- A pure function is one which depends only on local variables.
	```javascript
	// pure function
	function sum(a,b){
		/**
		 * 1. When the function is called it is added to the call-stack
		 * 2. And these variables are added to the stack-memory
		 * 3. When the function ends it is moved out of the call-stack and variables are removed from the stack-memory
		 */
		return a + b;
	}
	```
	- An impure function is one which depends on variables which are not local.
	```javascript
	// impure function
	const a = 5, b = 6;
	function sum(){
		// a and b are not local to the function
		// As it is a global variable it is kept in the heap-memory and it exists there even when this function ends and is removed from the call-stack
		// And thus this is a CLOSURE
		return a + b;
	}
	```
	- A `closure` is a function combined with it's outer scope or lexical environment.
	- We use closures all the time and we might not even know, for example,
	```javascript
	function query(url){
		fetch(url).then(()=>{
			// This is a function inside of the query function.
			// And this access to the url variable is only possible because of closures.
			console.log(url);
		});
	}
	```

7. Differentiate between pure and impure functions?
	- ```javascript
		// more on pure and impure functions
		function pure(a,b){
			return a+b;
		}

		function impure(a,b){
			// as this function depends on the implementation of another function whose definition might change anytime.
			// Therefore, this function is impure.
			console.log(a+b);
			return a+b;
		}
		// The deterministic nature of pure functions help in memoization
		```

8. What is var hoisting in JS?
	- When we use a variable with the `var` keyword regardless of it being used in the global or block scope it will be hoisted to the global scope.
	- For example, in the following code, the variable counter is hoisted to the top of the function, even though it is used before it is declared:
	```javascript
	function increment() {
  		console.log(counter); // undefined
		// var is hoisted to global state which is why we don't get an error stating that the variable doesn't exist or is not declared
  		counter = 1;
	}

	increment();
	```
	When the code is executed, the JavaScript engine will move the declaration of counter to the top of the function, so the code will be equivalent to the following:
	```javascript
	function increment() {
  		var counter;
  		console.log(counter); // undefined
  		counter = 1;
	}

	increment();
	```
	This means that the code will print undefined to the console, because the variable counter has not yet been initialized.

9. What is `let` and `const` hoisting?
	- Hoisting in JavaScript with `let` and `const` are hoisted WITHOUT a default initialization.
	- So accessing them before the line they were declared throws `ReferenceError: Cannot access 'variable' before initialization`
	- But variables declared with `var` are hoisted WITH a default initialization of `undefined`.

10. What is the output of these programs in JS?
	- ```javascript
		const func = () => console.log(letVar);
		let letVar = 3;
		func();

		/**
		 * Answer:
		 * Output is 3
		 * letVar is already initialized by the time func() is called
		 */
		```
	- ```javascript
		func();
		const func = () => console.log(letVar);
		let letVar = 3;

		/**
		 * Answer:
		 * Output is Error => ReferenceError: Cannot access 'letVar' before initialization
		 * Because, letVar is not initialized by the time func() is called
		 */
		```
	- ```javascript
		const func = () => console.log(letVar);
		func();
		let letVar = 3;

		/**
		 * Answer:
		 * Output is Error => ReferenceError: Cannot access 'letVar' before initialization
		 * Because, letVar is not initialized by the time func() is called
		 */
		```

11. What is a callback in JS?
	- Any function that is passed as an argument to another function so that it can be executed in that other function is called as a callback function.
	- Callback is called when a task gets completed and is the asynchronous equivalent of a function.