# JavaScript
## Menu
* [Functions](#Functions)
* [Types, Values, and Variables](#types-values-variables)


## <a name="types-values-variables"></a>Types, Values, and Variables
* primative types
	* numbers
	* strings
	* booleans
	* null
	* undefined
* object types
	* object
	* array
	* function

### Numbers
All numbers in JavaScript are represented as floating-point values.
> * 64-bit floating-point format
> * numeric literal

> base-10: 123
> base-16: 0x123
> base-8: 0123   *⭕️ECMAScript standard does not support them*

larger than largest: **Infinity** **-Infinity**
**Underflow**: 0, -0
Division by zero is not an error in JavaScript: it simply returns infinity or negative infinity.
0 divide 0 prints **NaN**
> Nan cannot be compared to anything, including itself

**Date** object

### Text
A string is an ==immutable== ordered sequence of ==16-bit values==, each of which typically represents a ==Unicode character==—strings are JavaScript’s type for representing text.

Double-quote characters may be contained within strings delimited by single-quote characters, and single-quote characters may be contained within strings delimited by double quotes.

==\\== is used to break a string into multiple lines

**RegExp()** constructor is defined for creating objects that represent textual patterns.

### Boolean Values
The following values convert to, and therefore work like, false:

```javascript
undefined 
null
```
All other values, including all objects (and arrays) convert to, and work like, true.

### null and undefined
* typeof null returns object
* typeof undefined returns undefined

```javascript
null == undefined;  // true
null === undefined; // false
```

### Variable Scope
JavaScript does not have **block scope**, instead, JavaScript uses **function scope**.
> ❗️JavaScript’s function scope means that all variables declared within a function are visible throughout the body of the function.
>> ==Variables are even visible before they are declared==. **hoisting**

```javascript
var scope = "global"; 
function f() {
  console.log(scope);  // Prints "local"
```
#### The Scope Chain
Every chunk of Java- Script code (global code or functions) has a scope chain associated with it.

* In top-level JavaScript code (i.e., code not contained within any function definitions), the scope chain consists of ==a single object, the global object==.

```javascript
var a = 1;
```

* In a **non-nested function**, the scope chain consists of ==two objects==. The first is the object that defines the ==function’s parameters and local variables==, and the second is the ==global object==.

```javascript
var b = function () {
}
```

* In a **nested function**, the scope chain has ==three or more objects==. 
	* When a function is defined, it stores the scope chain then in effect. 
	* When that function is invoked, it creates a new object to store its local variables, and adds that new object to the stored scope chain to create a new, longer, chain that represents the scope for that function invocation.

```javascript
```
![](http://js8.in/uploads/2011/10/10-25_155941-300x211.png)
![](http://images.cnitblog.com/i/466822/201407/131142125046160.png)


## <a name="functions"></a>Functions
In JavaScript, functions are objects, and they can be manipulated by programs.

```javascript
// Function expressions are sometimes defined and immediately invoked: 
var tensquared = (function(x) {return x*x;}(10));
```
> If a function definition expression includes a name, the local function scope for that function will include a binding of that name to the function object.
>> ==In effect, the function name becomes a local variable within the function.❓==

Variable declarations are hoisted, but assignments to those variables are not hoisted, so **functions defined with expressions cannot be invoked before they are defined**.

### Invoking functions
#### Function Invocation

```javascript
// Define and invoke a function to determine if we're in strict mode. 
var strict = (function() { return !this; }());
```

#### Method Invocation
In a method invocation expression like this, ==the object o becomes the invocation context==, and the function body can refer to that object by using the keyword **this**.

> ❗️If a nested function is invoked as a method, its this value is the object it was invoked on. If a nested function is invoked as a function then its this value will be either the global object (non-strict mode) or undefined (strict mode).

#### Constructor Invocation

#### Indirect Invocation
*call()*: uses its own argument list as arguments to the function
*apply()*: expects an array of values to be used as arguments
> Both methods allow you to explicitly specify the this value for the invocation, which means you can invoke any function as a method of any object, even if it is not actually a method of that object.

### Function Arguments and Parameters
Within the body of a function, the identifier ==**arguments**== refers to the Arguments object for that invocation.
> arguments object is an array-like object
> Remember that arguments is not really an array

*callee*: refers to the currently running function
*caller*: gives access to the call stack

### Functions As Values
* The function can be assigned to another variable and still work the same way.
* Functions can also be assigned to object properties rather than variables.
* Functions don’t even require names at all, as when they’re assigned to array elements

```javascript
var a = [function(x) { return x*x; }, 20]; // An array literal 
a[0](a[1]); // => 400
```
❗️==Function can have properties!==

```javascript
// Compute factorials and cache results as properties of the function itself. 
function factorial(n) {
    if (!(n in factorial)) {                    // If no cached result
      return factorial[n];                      // Return the cached result
    }
    else return NaN;                            // If input was bad
  }
  factorial[1] = 1; // Initialize the cache to hold this base case.
```

### Functions As Namespaces
variables declared within a function are visible throughout the function
❗️变量声明提升（hoisting），变量在方法内部声明，无论在方法内部哪儿都可以访问。

### Closures
```javascript
function counter() { 
  var n = 0;
  // ❗️the two methods share access to the private variable n
      return n++; 
    }, 
    reset: function() { 
      n = 0; 
    }
}

// ❗️each invocation of counter() creates a new scope chain and 
// a new private variable.
c.count() // => 0
d.count() // => 1: d was not reset
```

* set get 方法
* 方法的参数也是其private variable

```javascript
// This function returns a function that always returns v 
// v是constfunc()的私有变量
function constfunc(v) { return function() { return v; }; }
funcs[5]() // => 5

// 与下面的代码比较
// constfuncs()只被调用了一次，i是公有变量，所以funcs是共享i的。
// Return an array of functions that return the values 0-9 
function constfuncs() {
  return funcs;
```

### Function Properties, Methods, and Constructor
**bind()** is to bind a function to an object.

```javascript
function f(y) { return this.x + y; } // This function needs to be bound
var g = f.bind(o); // An object we'll bind to
g(2) // => 3

var sum = function(x,y) { return x + y }; // Return the sum of 2 args
var succ = sum.bind(null, 1);
var g = f.bind({x:1}, 2); // Bind this and y
```

### The Function() Constructor
```javascript
// The Function() constructor expects any number of string arguments. 
// The last argument is the text of the function body; it can contain arbitrary 
// JavaScript statements, separated from each other by semicolons.
var f = new Function("x", "y", "return x*y;");
```
❗️==Function() constructor永远将其视为top-level。==

### Functional Programming
**Higher-Order** Functions: 基于函数操作，将一个或多个函数作为参数传入，并返回一个新函数。

```javascript
// This higher-order function returns a new function that passes its
function not(f) {
    var result = f.apply(this, arguments); // that calls f
  };
  return x % 2 === 0;
var odd = not(even); // A new function that does the opposite 
[1,1,3,5,5].every(odd); // => true: every element of the array is odd
```